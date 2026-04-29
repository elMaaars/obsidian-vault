# Pipeline de Parcelación Geodésica (GeoSP) — HCP

## Descripción General

- Método de parcelación cortical basado en geodésicas que divide cada hemisferio en **500 subregiones** por hemisferio, con etiquetas `1001-1500`.
- Utiliza las regiones del atlas DK (Desikan-Killiany, 35 regiones por hemisferio) como base para la subdivisión.
- La región subcortical se identifica con la etiqueta `-1` en los datos crudos y se preserva como `0` en la salida final.
- Se trabaja con una cohorte de **700+ sujetos** con edades entre 36 y 100 años.

---

## Preprocessing 0: Resampling de Etiquetas a Espacio 32k

- Adaptación del script de resampling por vecino más cercano.
- Flujo del código:
  - Carga del mesh nativo por sujeto (`lh.aparc.annot`, mesh nativo `.surf.gii`).
  - Carga del mesh 32k por sujeto (`sub_id.L.midthickness.32k_fs_LR.surf.gii`).
  - Para cada vértice del mesh 32k, se busca el vértice nativo más cercano usando un KDTree sobre las coordenadas 3D.
  - Se asigna al vértice 32k la etiqueta DK del vértice nativo más cercano.
  - Guardado de las etiquetas remuestreadas a disco.

> [!info]+
> Todos los sujetos tienen meshes nativos con diferente número de vértices, lo que hace que los índices de vértices no sean comparables entre sujetos en espacio nativo. El resampling a 32k garantiza que todos los sujetos compartan exactamente **32.492 vértices por hemisferio**, haciendo los índices comparables entre sujetos.

> [!note]+
> Se usa vecino más cercano (k=1) en lugar de interpolación baricéntrica. Esto introduce algo de ruido en los bordes de región (~40% de vértices con más de una etiqueta a lo largo de los sujetos), pero es suficiente para los pasos posteriores. Una alternativa más precisa requeriría `wb_command -label-resample` con esferas de registro, que no estaban disponibles.

> [!warning]+
> Algunos archivos `.gii` de mesh 32k pueden estar duplicados (contenido repetido en el archivo). Se detectan por su tamaño doble y se corrigen truncando el archivo en el primer tag `</GIFTI>`.

- Flujo de datos:
  - **INPUT:** *Mesh nativo L/R por sujeto*, *Etiquetas DK nativas L/R por sujeto* (`.aparc.annot`), *Mesh 32k L/R por sujeto*.
  - **OUTPUT:** *Etiquetas DK 32k L/R por sujeto* (`lh_labels_32k.txt`, `rh_labels_32k.txt`).
- Se ejecuta una vez por sujeto.

---

## Preprocessing 1: Construcción del K-File

- Adaptación del script de construcción de k-files.
- Flujo del código:
  - Para cada sujeto, carga el mesh 32k y las etiquetas DK 32k.
  - Calcula el área de cada región DK usando los triángulos del mesh (`MT.get_ID_tri`, `MT.calcular_area_regiones`).
  - Acumula el área por región DK a lo largo de todos los sujetos y calcula la media.
  - Define un tamaño medio de subregión objetivo: `mean_size = area_total_media / 500`.
  - Asigna a cada región DK un número de subregiones `k = ceil(area_region / mean_size)`.
  - Ajusta iterativamente las asignaciones para que la suma total sea exactamente **500 subregiones por hemisferio**, añadiendo subregiones a las regiones más grandes primero.
  - Construye k-files simétricos (mismo k para L y R en cada región DK).
  - Añade `L_-1: 1` y `R_-1: 1` para la región subcortical (k=1, no se subdivide).
  - Guardado a disco en formato JSON.

> [!info]+
> El k-file se construye en espacio 32k para que las áreas sean comparables entre sujetos. La suma de todos los valores del k-file es **501 por hemisferio** (500 corticales + 1 subcortical).

> [!note]+
> El k-file es simétrico — ambos hemisferios reciben el mismo número de subregiones para cada región DK homóloga. Esto facilita comparaciones interhemisféricas.

> [!warning]+
> **Bug conocido:** `Lk.update(Rk)` en `ab_parcellation_homogeneous_regions` muta el diccionario `Lk` en lugar de crear una copia. Si la función se llama múltiples veces en el mismo proceso (e.g. en un notebook), los valores del k-file se corrompen. Solución: recargar el k-file desde disco antes de cada uso, o reemplazar `Lk.update(Rk)` por `Lk = {**Lk, **Rk}`.

- Flujo de datos:
  - **INPUT:** *Mesh 32k L/R por sujeto*, *Etiquetas DK 32k L/R por sujeto*.
  - **OUTPUT:** *Archivo único de k-file L/R* (`Lk_full.txt`, `Rk_full.txt`) en formato JSON.
- Se ejecuta una vez para todos los sujetos.

---

## Preprocessing 2: Parcelación con Centros Aleatorios

- Adaptación de `main_regiones_homogeneas_HCP.py` con `geo_kmeans.py`.
- Flujo del código:
  - Carga del mesh 32k y etiquetas DK 32k por sujeto.
  - Construcción de la matriz de adyacencia ponderada por distancias euclidianas entre vértices (`create_matrix`).
  - Para cada región DK, extracción de la submatriz dispersa correspondiente.
  - Inicialización de centros con KMeans++ (`initialize`) restringida a vértices conectados dentro de la región.
  - Ejecución del kmeans geodésico (`create_groups` via Dijkstra + `recalc_center` via closeness centrality) por hasta 20 iteraciones o hasta convergencia.
  - Guardado de etiquetas a disco.

> [!important]+
> La restricción a vértices conectados en `initialize` evita que vértices aislados (sin aristas en la submatriz) sean seleccionados como centros, lo que causaría grupos vacíos y subregiones faltantes. En meshes 32k no hay vértices desconectados, pero la restricción se mantiene por robustez.

> [!note]+
> El proceso se ejecuta en paralelo por región DK usando `multiprocessing.Pool`, lo que hace que fijar una semilla global no garantice reproducibilidad. Para reproducir resultados de una región específica se puede fijar la semilla dentro de `parallel_kmeans_ab` con un condicional por etiqueta de región.

> [!warning]+
> **Bug original (corregido):** En la versión nativa, `for c, matrix in dist_matrices.items()` sobreescribía el parámetro `matrix` de la función con un array numpy, corrompiendo cualquier uso posterior de `matrix` en el mismo scope. Corregido renombrando la variable del loop a `dists`.

- Flujo de datos:
  - **INPUT:** *Mesh 32k L/R por sujeto*, *Etiquetas DK 32k L/R por sujeto*, *K-file L/R*.
  - **OUTPUT:** *Etiquetas de parcelación L/R por sujeto* (`Llabels.txt`, `Rlabels.txt`) en `random_centers/`.
- Se ejecuta una vez por sujeto.

---

## Processing 3 Fixed Centers (Centros Fijos)

- Adaptación de `main_fixed_centers.py`.
- Flujo del código:
  - Carga de meshes y etiquetas DK por sujeto.
  - Construcción de índices por región DK (`get_indices`), excluyendo la región subcortical (`L_-1`, `R_-1`) antes del kmeans.
  - Ejecución del kmeans geodésico con centros fijos (`parallel_kmeans_ab_fixed_centers`):
    - Si el centroide no está dentro de la región, hace snap al vértice más cercano dentro de la misma región.
    - `create_groups` asigna cada vértice a su centro más cercano via Dijkstra.
  - Construcción del mapa de subparcelas (`create_subparcels`).
  - Escritura de etiquetas y subparcelas a disco.

> [!important]+
> Los vértices subcorticales (`-1`) se excluyen del kmeans y se inicializan con `0` en `create_labels_ab`. Algunos vértices corticales de frontera (~6 por sujeto) también quedan con etiqueta `0` por un **descarte silencioso** en `create_groups` — ocurre cuando un vértice no tiene aristas dentro de su región en la submatriz dispersa, por lo que Dijkstra nunca lo alcanza.

> [!note]+
> Este comportamiento es conocido y aceptado. Se maneja correctamente en el paso de alineación.

- Flujo de datos:
  - **INPUT:** *Mesh L/R por sujeto*, *Etiquetas DK L/R por sujeto*, *Centroides L/R (mostcommon sampled)*.
  - **OUTPUT:** *Etiquetas L/R por sujeto* (`Llabels.txt`, `Rlabels.txt`), *Subparcelas L/R por sujeto* (`Lsparcels.txt`, `Rsparcels.txt`) en `labels_regados_sampled/`.
- Se ejecuta una vez por sujeto.

---

## Processing 4 Most Common Centroids

- Adaptación de `centroides_mostcommon_GeoSP_HCP.py`.
- Flujo del código:
  - Definición del método `centroides_per_DK_region` (lógica sin cambios).
  - Aplicación del método sobre los sujetos para obtener los centroides por región DK.
  - Búsqueda del centroide más cercano usando un KDTree.
  - Obtención de etiquetas y verificación de múltiples etiquetas en vértices.
  - Selección del centroide más común por región. Si no se encuentra ninguno, se asigna uno aleatorio.
  - Guardado a disco.

> [!info]+
> Puede ejecutarse sobre todos los sujetos o solo una muestra. **Se usaron 100 sujetos aleatorios** para generar los centroides de referencia.
> Se agregó una verificación de seguridad en los límites (`p >= len(centers_count_ord)`) para prevenir crashes en casos donde no se encuentra ningún centroide.

- Flujo de datos:
  - **INPUT:** *Mesh L/R por sujeto*, *Etiquetas L/R por sujeto*, *Etiquetas de parcelación L/R por sujeto*.
  - **OUTPUT:** *Archivo único de centroides más comunes L/R* (`mostcommon_centroids_lh_sampled.txt`, `mostcommon_centroids_rh_sampled.txt`).
- Se ejecuta una vez para todos los sujetos.

---

## Processing 5: Alineación (Alignment)

- Adaptación de la función `alinear_labels`.
- Flujo del código:
  - Carga de meshes, etiquetas y subparcelas desde `labels_regados_sampled` por sujeto.
  - Carga de centroides mostcommon (sampled) para ambos hemisferios.
  - Construcción del diccionario cortical excluyendo `-1` (subcortical) y `'0'` (vértices contaminados por descarte silencioso).
  - Para cada región DK, busca cada centroide **solo dentro de las subparcelas de la misma región DK**.
  - Si el centroide no se encuentra (fallback), hace snap a la subparcela **no visitada más cercana** dentro de la misma región DK.
  - Registro de subparcelas visitadas para garantizar exactamente **500 etiquetas únicas** (`1001-1500`) por hemisferio.
  - Guardado de etiquetas y subparcelas a disco.

> [!important]+
> **El cambio clave es la restricción regional** — los centroides solo pueden coincidir con subparcelas de su propia región DK, evitando el robo de subparcelas entre regiones y las subparcelas huérfanas.

> [!note]+
> **Dos casos requieren el fallback:**
> 1. El vértice centroide tiene etiqueta `'0'` por el descarte silencioso de `create_groups`.
> 2. El vértice centroide aterrizó en una región DK diferente por variabilidad anatómica entre sujetos.

> [!warning]+
> **Problema original:** Sin la restricción regional, un centroide de `L_29` podía aterrizar en una subparcela de `L_25` (por variabilidad anatómica), robándola y dejando subparcelas huérfanas. Además, los vértices subcorticales podían ser reetiquetados por centroides corticales, destruyendo la región subcortical.

- Flujo de datos:
  - **INPUT:** *Mesh L/R por sujeto*, *Etiquetas L/R de `labels_regados_sampled` por sujeto*, *Subparcelas L/R de `labels_regados_sampled` por sujeto*, *Centroides mostcommon (sampled)*.
  - **OUTPUT:** *Etiquetas L/R alineadas por sujeto* (`Llabels.txt`, `Rlabels.txt`), *Subparcelas L/R alineadas por sujeto* (`Lsparcels.txt`, `Rsparcels.txt`) en `alineacion_sampled/`.
- Se ejecuta una vez por sujeto.

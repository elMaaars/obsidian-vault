- Parcelación del atlas de Schaefer está disponible en formato cifti (más o menos como 2D).
- Parcelación de Tian está disponible en formato nifti (volumen, 3D).
### Eligiendo las parcelaciones para combinar
- Naturalmente, al tener muchas resoluciones para la parcelación de Schaefer, el tamaño de las parcelas se reduce conforme se hacen más divisiones.
- Existen 10 escalas de Schaefer (100 a 1000 parcelas) y solo 4 para Tian (16, 32, 50, 54).
- Una forma de decidir cuál parcelación de subcortical acoplar a la parcelación cortical es revisar el tamaño promedio de las parcelas para intentar obtener una parcelación de similar tamaño.
> [!info]-
> De forma natural las estructuras subcorticales son de menor tamaño que las corticales.
- Los atlas de Schaefer y Tian viven en espacios distintos:
	- **Schaefer** se define sobre la superficie cortical (archivo `.dlabel.nii`, formato CIFTI). Las parcelas son conjuntos de vértices sobre una malla triangular. Su tamaño se mide en **área superficial (mm²)**.
	- **Tian** se define en el volumen cerebral (archivo `.nii`, formato NIfTI). Las parcelas son conjuntos de vóxeles en un espacio 3D. Su tamaño se mide en **volumen (mm³)**.
>[!important]-
>No se pueden comparar mm² con mm³ directamente.

- Para solucionarlo convertimos cada medida a una escala lineal común:
	- Para parcelas corticales: **√(área promedio)** → mm
	- Para parcelas subcorticales: **∛(volumen promedio)** → mm
- Ambos valores ahora representan una extensión espacial en milímetros y son directamente comparables.

**Cómo se computa el área de una parcela cortical**:
1. Se carga la superficie (`midthickness.32k_fs_LR.surf.gii`) de cada sujeto, que contiene las coordenadas de los vértices y las caras triangulares.
2. Se calcula el área de cada triángulo (producto cruz de sus aristas) y se reparte 1/3 del área a cada uno de sus 3 vértices.
3. Se carga el atlas de Schaefer (`.dlabel.nii`), que asigna una etiqueta de parcela a cada vértice.
4. Se suman las áreas de los vértices que pertenecen a cada parcela → área de la parcela en mm².

**Cómo se computa el volumen de una parcela subcortical**:
1. Se carga el archivo NIfTI de Tian, que es un volumen 3D donde cada vóxel tiene una etiqueta.
2. Se cuentan los vóxeles por etiqueta.
3. Se multiplica por el volumen de cada vóxel (obtenido del header del NIfTI, e.g., 2mm isótropo → 8 mm³ por vóxel).

>[!note]-
>**Nota técnica:** El cálculo de áreas por vértice es matemáticamente idéntico al que realiza `wb_command -surface-vertex-areas` de Connectome Workbench.
### Pasos generales:
1. Tomar la división cerebral de Schaefer, unirla con la de Tian para generar una división que incluya corteza y subcorteza.
2. Usar esa división para generar matrices de conectividad:
	1. En el caso estructural usar eso para intersectar con las fibras.
	2. En el caso funcional usr eso para "intersectar" con las señales BOLD.

### Consideraciones estructurales
- El proceso no es tan simple. Para la intersección de las fibras se requiere de una división cerebral volumétrica (para ver bien por dónde pasa, algo así).
- Por lo tanto necesitamos que la parcelación Schaefer+Tian esté en formato nifti.
- Para lograr esto tomamos los labels entregados por Schaefer y junto a la imágen T1w del sujeto (que es un volúmen), podemos *craftear* un nifti para la parcelación cortical.
- Ese nifti junto al nifti subcortical permiten hacer un volumétrico del cerebro completo para usar con las fibras.

### Consideraciones funcionales
- El proceso no es tan simple. Se necesita un archivo de etiquetas que unifique la etiquetas de Schaefer y de Tian (ambos a la resolución deseada).
- El "*workbench*" tiene un comando que es capaz de hacer este trabajo. Igualmente en el repositorio de Tian hay algunos merges ya realizados (100, 200, 400 parcelas con cada una de las de Tian).
- Con estas nuevas etiquetas y las señales se aplica nuevamente el "*workbench*" para hacer las matrices.
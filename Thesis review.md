# Sugerencias de mejora — Propuesta de Tesis

**"Evaluación del efecto de la parcelación cerebral multiescala en modelos predictivos"** Bruno Andrés Arce Rodríguez · Magíster en Ciencias de la Computación · UdeC

---

## Comentarios generales antes de entrar por capítulo

Antes de las sugerencias específicas, hay tres tensiones transversales en el documento que conviene resolver porque atraviesan todos los capítulos:

### 1. Inconsistencia entre título, hipótesis y objetivos

- El **título** habla de "modelos predictivos" en general.
- La **introducción** habla casi exclusivamente de **clasificación de género**.
- El **objetivo general** menciona "predicción de edad **y** clasificación de género".
- Los **objetivos específicos 3 y 4** sólo mencionan clasificación de género.
- La **hipótesis** sólo habla de clasificación de género.

Esto debe alinearse. Hay dos caminos limpios:

- **(A)** Eliminar la mención a predicción de edad del objetivo general (es la opción más coherente con el resto del documento). El título "modelos predictivos" queda igual porque clasificación es un tipo de modelo predictivo.
- **(B)** Mantener ambas tareas (regresión de edad + clasificación de género) y reescribir hipótesis, objetivos específicos 3-4 y metodología para incorporarlas explícitamente. Es más ambicioso y más interesante científicamente porque permitiría contrastar si el "rango óptimo de escala" depende de la tarea.

Recomiendo **(B)** porque el dataset HCP-A es ideal para edad (rango 36-100 años, tu cita Bookheimer 2019) y porque ya hay literatura previa tuya en eso (Arce et al. 2025). Pero hay que comprometerse explícitamente.

### 2. El término "género" vs "sexo"

A lo largo del texto se usa "género" cuando lo que se predice es **sexo biológico al nacer** (lo dices explícitamente en Metodología: _"utilizando como ground truth el sexo reportado para cada sujeto"_). Esto es una inexactitud terminológica importante y los revisores neurocientíficos la marcarán. En neuroimagen contemporánea la distinción es relevante: género es identidad/construcción social, sexo es la variable biológica registrada al nacer. Reemplazar sistemáticamente "clasificación de género" → "clasificación de sexo" o "clasificación de sexo biológico". La referencia Sapuan et al. (2026) que ya usas literalmente se titula _"sex classification in neuroimaging"_, lo que refuerza el cambio.

### 3. Errores de formato de citas BibTeX

Hay varias citas que aparecen sin formatear porque la clave BibTeX no está bien escrita o falta:

- `ritchie2018sex` / `Ritchie2018` (página 4 y 15) — aparece en crudo
- `basser1994mr` (página 9) — aparece en crudo
- `tournier2007robust` (página 10) — aparece en crudo
- `jeurissen2014multi` (página 10) — aparece en crudo
- `Hansen2020`, `Golbeck2013`, `NetworkX`, `Latora2001`, `Eppstein2013`, `Rodrigue2024`, `Clauset-Newman-Moore`, `Smith2013`, `Friston1994`, `PankajTibrewal2023`, `scikit-learn`, `Koehrsen2017` (páginas 19-23) — todas en crudo
- `armstrong2016graph` y otras en bibliografía aparecen pero nunca se citan

Hay que hacer una pasada completa de saneado de BibTeX. Es un detalle de forma pero da mala impresión al comité.

---

## Capítulo 1 — Introducción

### Lo que funciona bien

La introducción tiene una estructura argumentativa fuerte: parte del problema general (parcelación es metodológicamente arbitraria), lo aterriza en el problema específico (clasificación de sexo es sensible a esa arbitrariedad), identifica el vacío en la literatura (no hay trabajos que combinen multimodal + multiescala + subcortical + interpretabilidad) y propone el enfoque. La cita estratégica a Sapuan et al. (2026) como motivación es muy efectiva.

### Lo que necesita mejorarse

**Párrafo 1 (página 1)** — La frase _"Esta variabilidad representa una fuente sistemática de sesgo"_ es fuerte y correcta, pero el párrafo no aterriza qué consecuencia _concreta_ tiene esa variabilidad. Sugiero agregar una oración cerrando el párrafo del tipo: _"En la práctica, esto significa que dos estudios que usan parcelaciones distintas pueden llegar a conclusiones contradictorias sobre el mismo fenómeno neurobiológico, comprometiendo la replicabilidad — un problema documentado por X en Y."_ Aquí Botvinik-Nezer et al. (2020, _Nature_, "Variability in the analysis of a single neuroimaging dataset by many teams") sería una referencia ideal y de mucho peso: 70 equipos analizando los mismos datos llegan a conclusiones distintas. La incluyes y tu introducción gana un anclaje empírico muy potente.

**Párrafo 2 (página 1-2)** — Bien estructurado pero hay un detalle: cuando citas a Litwińczuk et al. (2024) diciendo _"ninguna parcelación única es universalmente óptima para todas las tareas predictivas"_ esto contradice levemente tu hipótesis (que postula que existe un "rango óptimo"). Conviene aclarar: tu hipótesis no es que exista UNA parcelación óptima, sino un _rango_ de escalas dentro del cual la robustez es máxima. Ese matiz debería explicitarse aquí o más adelante.

**Párrafo 3 (página 2, "Este trade-off refleja un dilema inherente...")** — La frase _"el número de características crece explosivamente, conduciendo a la conocida maldición de la dimensionalidad"_ es correcta pero te falta cuantificar. En una matriz N×N de conectividad, el número de aristas únicas es N(N-1)/2: con 200 regiones son ~20.000 features, con 1000 son ~500.000. Agregar este cálculo concreto hace el problema mucho más palpable. Bellman 1961 es la referencia clásica si quieres anclar "maldición de la dimensionalidad" formalmente.

**Párrafo 4 (página 2, sobre clasificación de género)** — Aquí entras al problema específico. Bien, pero hay redundancia con el párrafo anterior. Considera fusionarlos o separar más claramente: _párrafo A = problema general de parcelación; párrafo B = por qué clasificación de sexo es un caso de prueba ideal_. Como referencia adicional útil aquí: **Joel et al. (2015, PNAS, "Sex beyond the genitalia: The human brain mosaic")** — argumenta que las diferencias estructurales son distribuidas y no permiten clasificación binaria limpia. Citarla muestra que conoces el debate, no sólo los trabajos que reportan diferencias.

**Párrafo 5 (página 3, sobre subcorticales)** — _"emparejar parcelas corticales finas con estructuras subcorticales de baja resolución introduce un desequilibrio topológico significativo"_. Este argumento es el más débil de la introducción porque está apoyado sólo en Zalesky 2010. Reforzar con Tian et al. (2020) que ya citas en el marco teórico — el atlas subcortical de Tian fue diseñado _específicamente_ para resolver este desbalance, así que mencionarlo aquí da continuidad. También: **Pauli, Nili & Tyszka (2018, Scientific Data, "A high-resolution probabilistic in vivo atlas of human subcortical brain nuclei")** es otra referencia útil para parcelación subcortical de alta resolución.

**Párrafo final (página 5)** — La promesa metodológica (_"contribuir una metodología rigurosa y replicable"_) es genérica. Reemplazar por algo más específico: ¿qué deliverable concreto produce esta tesis que un investigador podría usar? Por ejemplo: _"Como contribución concreta, este trabajo entregará (i) un pipeline reproducible de extracción de features multiescala-multimodal con parcelaciones cortico-subcorticales balanceadas, y (ii) un mapa empírico del rango de escalas donde las firmas de sexo son más estables, que podrá servir como guía metodológica para estudios futuros."_

### Referencias que faltan y que mejorarían el capítulo

- **Botvinik-Nezer et al. (2020)** — replicabilidad en neuroimagen
- **Joel et al. (2015)** — debate sobre el "cerebro sexuado"
- **Pauli, Nili & Tyszka (2018)** — atlas subcortical
- **Eickhoff, Yeo & Genon (2018, Nature Reviews Neuroscience, "Imaging-based parcellations of the human brain")** — revisión autoritativa de métodos de parcelación, te ahorraría varias citas y daría peso
- **Marek et al. (2022, Nature, "Reproducible brain-wide association studies require thousands of individuals")** — este paper sacudió el campo y argumenta que los tamaños de muestra típicos en neuroimagen son insuficientes para hallazgos reproducibles. Tu N=721 es relativamente grande pero igual conviene citar y discutir.

### Imágenes sugeridas para la introducción

- Una **figura conceptual de apertura** que muestre el mismo cerebro parcelado en 3-4 resoluciones distintas (ej. 100, 400, 800 regiones del atlas de Schaefer) lado a lado, con un panel adicional mostrando cómo cambia la matriz de conectividad. Esto comunica visualmente en 2 segundos el problema central de la tesis.
- Un **esquema del "vacío en la literatura"**: una matriz 2×2 (multimodal sí/no × multiescala sí/no) con puntos para los trabajos relevantes (Liu 2023, Shehzad 2025, He 2025, etc.) y tu casilla vacía marcada. Visualmente potente.

---

## Capítulo 2 — Marco Teórico

### Lo que funciona bien

La cobertura es completa: anatomía → MRI → modalidades específicas → parcelación → conectividad → grafos → ML. Es la secuencia correcta. Las figuras incluidas (2.1, 2.3, 2.4) son apropiadas. La sección 2.6 sobre parcelación está particularmente bien desarrollada.

### Problemas estructurales

**El marco teórico es demasiado largo y desbalanceado.** Tienes ~20 páginas con descripciones de cosas que un comité de Magíster en Ciencias de la Computación ya conoce (qué es accuracy, qué es SVM) y demasiado poco sobre lo que es realmente novedoso para tu propuesta (multiescala, integración multimodal, interpretabilidad SHAP).

**Sugerencia de re-balanceo:**

- **Recortar drásticamente** las secciones 2.9 (ML básico) y 2.9.1 (métricas básicas). Un par de párrafos cada una, citando bibliografía estándar (Hastie, Tibshirani & Friedman; o Bishop). No necesitas redefinir accuracy con su fórmula en una tesis de Magíster. Lo mismo aplica a la descripción de SVM, RF y LR — un párrafo conjunto basta.
- **Expandir** la sección 2.6.5 (Enfoque multiescala) que es la más relevante para tu trabajo y sin embargo es la más corta. Debería ser de las más largas, no la más breve.
- **Agregar** una sección 2.10 sobre **interpretabilidad y SHAP** que actualmente no existe pero es central a tu propuesta. Lundberg & Lee (2017) está citado en la introducción y metodología pero nunca explicado.

### Sección 2.1 (Anatomía cerebral)

Está bien para abrir, pero la subsección 2.1.1 (Materia gris) menciona estructuras subcorticales (tálamo, putamen, etc.) sin imagen. Una **figura anatómica** que muestre dónde están estas estructuras subcorticales sería muy útil aquí, especialmente porque la inclusión subcortical es un eje central de tu propuesta. Sugiero una vista coronal o axial con anotaciones.

### Sección 2.2-2.5 (MRI y modalidades)

Bien cubiertas. Algunos detalles:

**Sección 2.3.1** — La oración _"En secuencias ponderadas en T1 (T1w), la materia blanca aparece hiperintensa respecto a la materia gris"_ es correcta pero invertirlo para que diga primero qué se observa en T1 y T2 lo hace más legible.

**Sección 2.4.1** — Los modelos de difusión están bien explicados pero la transición DTI → CSD → MSMT-CSD se beneficiaría de una figura comparativa. Mostrar, para un mismo vóxel con cruce de fibras, qué estima cada modelo (un solo vector vs FOD vs FOD multi-tejido) clarifica enormemente la progresión. Estas figuras existen en Jeurissen et al. 2014 y son reutilizables con cita.

**Sección 2.4.2** — La Figura 2.2 sobre tractografía determinística vs probabilística es buena. Pero la descripción de los criterios de detención (_"hasta alcanzar ciertos criterios de detención definidos por el objetivo del análisis"_) es vaga. Mencionar criterios concretos: umbral de FA, ángulo máximo de curvatura, longitud máxima/mínima, etc.

**Sección 2.5 (fMRI)** — Te falta mencionar que la rs-fMRI requiere un preprocesamiento específico no trivial (corrección de movimiento, regresión de señales de ruido, scrubbing) que es ALTAMENTE relevante para tu hipótesis. Sapuan et al. (2026) que tanto citas argumenta justamente que diferencias de movimiento entre sexos pueden ser un confundidor mayor. Conviene anticiparlo aquí. Referencia: **Power et al. (2014, NeuroImage, "Methods to detect, characterize, and remove motion artifact in resting state fMRI")**.

### Sección 2.6 (Parcelación cerebral) — la más importante

Esta sección está bien pero puede pulirse:

**2.6.1** — Sólido. Podría mencionarse explícitamente HCP-MMP (Glasser et al. 2016, _Nature_) como otro ejemplo de parcelación basada en superficie multimodal, aunque no la uses. Da contexto.

**2.6.2 (Schaefer)** — Bien explicado. La Figura 2.3 es informativa. Vale la pena agregar una oración sobre la **limitación**: Schaefer es funcional, derivado de un grupo grande de sujetos, lo que significa que las fronteras están "promediadas" y pueden no respetar la organización funcional individual. Esto motiva métodos individualizados como Kong et al. (2021) que ya citas (la figura es de ellos) pero no integras al texto.

**2.6.3 (Prieto et al. 2023)** — Aquí hay un problema sutil. Dices que el método de Prieto es "puramente geométrico". Correcto. Pero el contraste con Schaefer ("funcional") no es del todo justo porque Schaefer también es resultado de un proceso geométrico de agrupamiento sobre la superficie, sólo que con un criterio diferente. Reformular: _"A diferencia del atlas de Schaefer, que define las fronteras donde la conectividad funcional cambia bruscamente, este método utiliza únicamente la geometría de la superficie cortical, agrupando vértices que son geodésicamente cercanos..."_. La distinción es: criterio de homogeneidad funcional vs criterio de proximidad geométrica.

**2.6.4 (Parcelación subcortical)** — Mencionas Tian et al. (2020) brevemente pero no profundizas. Esta debería ser una subsección más desarrollada porque es metodológicamente clave para tu propuesta. Explicar:

- Qué hace Tian 2020 distinto (gradientes de conectividad funcional aplicados al subcórtex)
- Disponibilidad en múltiples escalas (Scale I, II, III, IV con 16/32/50/54 regiones por hemisferio)
- Por qué emparejar Tian con Schaefer es metodológicamente ventajoso (ambos derivados de gradientes funcionales, ambos multiescala)

**2.6.5 (Multiescala)** — Demasiado corta para ser el corazón conceptual de tu tesis. Expandir con:

- Definición operacional clara de "multiescala" (¿es solo varios niveles? ¿integración jerárquica? ¿concatenación de features?)
- Distinguir entre **multiescala paralela** (extraer features a varias escalas, concatenar y predecir) vs **multiescala jerárquica** (modelar la jerarquía explícitamente como en MAHGCN de Liu 2023). Tu propuesta parece ser la primera y conviene explicitarlo.
- **Betzel & Bassett (2017)** ya está citado pero su argumento sobre redes jerárquicas merece más espacio.
- Referencia adicional muy útil: **Akiki & Abdallah (2019, Scientific Reports, "Determining the Hierarchical Architecture of the Human Brain Using Subject-Level Clustering of Functional Networks")**.

### Sección 2.7 (Conectividad cerebral)

La diferencia SC/FC está bien explicada. Una **figura conceptual** que muestre lado a lado: tractos → matriz SC vs series temporales → matriz FC, ayudaría mucho. Estas figuras existen abundantemente en la literatura (Sporns 2013 tiene una clásica).

Falta mencionar un tema importante: la **correspondencia limitada entre SC y FC**. La conectividad estructural pesada no garantiza conectividad funcional pesada (regiones pueden estar funcionalmente correlacionadas sin conexión directa, vía caminos polisinápticos). Esto motiva tu integración multimodal: ambas capturan información complementaria. Referencias: **Honey et al. (2009, PNAS, "Predicting human resting-state functional connectivity from structural connectivity")**, **Suárez et al. (2020, Trends in Cognitive Sciences, "Linking Structure and Function in Macroscale Brain Networks")**.

### Sección 2.8 (Teoría de grafos)

La sección es exhaustiva pero también está desbalanceada: lista 13 métricas con la misma profundidad sin priorizar cuáles son más relevantes para tu trabajo.

**Sugerencias:**

- Agrupar las métricas en una **tabla** en lugar de lista, con columnas: Nombre / Escala (local/mesoscala/global) / Aspecto que captura (integración/segregación/centralidad) / Referencia. Hace la sección mucho más legible y útil como referencia.
- Saneado de citas (mencionado antes — `Hansen2020`, `NetworkX`, etc. están sin formatear).
- Mencionar que las métricas dependen del **umbralizado** y la **densidad** del grafo: una decisión metodológica adicional que también introduce variabilidad. ¿Vas a usar grafos densos? ¿Aplicar threshold? ¿Cuál? Anticiparlo aquí o en metodología.
- **Imagen sugerida**: un diagrama con un grafo pequeño (10-15 nodos) ilustrando visualmente qué mide cada métrica (qué nodo tiene mayor centralidad, dónde está el clique, etc.). Muy pedagógico.

### Sección 2.9 (ML)

**Recortar agresivamente.** Una versión propuesta:

> _"Para la tarea de clasificación de sexo se emplearán tres algoritmos supervisados de aprendizaje automático tradicional: Support Vector Machine (SVM), Random Forest (RF) y Logistic Regression (LR). La elección de algoritmos tradicionales sobre Deep Learning responde a tres criterios: (i) el tamaño moderado del dataset (N=721) hace innecesarias arquitecturas con millones de parámetros; (ii) la interpretabilidad mediante SHAP es más directa sobre estos modelos; (iii) la comparabilidad con literatura previa en clasificación de sexo basada en grafos (Chiêm et al. 2018; He et al. 2025) se preserva. Las implementaciones provienen de scikit-learn (Pedregosa et al. 2011)."_

Eso reemplaza ~2 páginas. La fórmula de accuracy, precision, recall y F1 puede ir en un apéndice o simplemente omitirse — el comité las conoce.

### Sección faltante: 2.10 Interpretabilidad

Debe crearse. Contenido sugerido:

- Definición de interpretabilidad en ML (intrínseca vs post-hoc; global vs local).
- **SHAP** (Lundberg & Lee 2017): fundamento en valores de Shapley de teoría de juegos, qué entrega (importancia por feature por instancia), por qué es preferible a importancias nativas de los modelos.
- **Permutation Feature Importance** (Breiman 2001): qué mide, ventajas y limitaciones (sensible a features correlacionadas).
- **Estabilidad de rankings de importancia** entre escalas como criterio de validación neurobiológica. Esta es la pieza conceptual más original de tu propuesta y necesita argumento teórico — no sólo metodológico — aquí. Idea clave: si una feature es importante en escala N=200 y también lo es en N=300 y N=400, probablemente refleja un fenómeno biológico real; si sólo es importante en N=200, probablemente es un artefacto de esa parcelación específica.

### Referencias que faltan en marco teórico

- **Glasser et al. (2016)** — atlas HCP-MMP
- **Pauli, Nili & Tyszka (2018)** — atlas subcortical alternativo
- **Power et al. (2014)** — movimiento en fMRI
- **Honey et al. (2009)** — SC-FC
- **Suárez et al. (2020)** — SC-FC review reciente
- **Pedregosa et al. (2011)** — scikit-learn (cita formal)
- **Breiman (2001)** — Random Forest y permutation importance
- **Akiki & Abdallah (2019)** — jerarquía cerebral
- **Hastie, Tibshirani & Friedman (2009)** — Elements of Statistical Learning (cita estándar para ML básico)

### Imágenes adicionales sugeridas para el marco teórico

- Vista anatómica de estructuras subcorticales (sección 2.1)
- Comparación visual DTI / CSD / MSMT-CSD para mismo vóxel con cruce de fibras (sección 2.4.1)
- Diagrama SC vs FC: tracto y serie temporal → dos matrices (sección 2.7)
- Pequeño grafo ilustrativo con cada métrica resaltada visualmente (sección 2.8)
- Diagrama conceptual de multiescala: mismo cerebro a 200, 400, 800 regiones con la matriz de conectividad correspondiente (sección 2.6.5) — esto es CRÍTICO porque comunica el corazón de tu trabajo

---

## Capítulo 3 — Estado del Arte

### Lo que funciona bien

Identificas correctamente los tres trabajos centrales con los que competirás (Liu 2023, Shehzad 2025, He 2025) y articulas el vacío. La referencia a Tang et al. (2023) como marco taxonómico es estratégicamente buena.

### Problemas

**El capítulo es corto y no exhibe el panorama completo.** Sólo discutes ~6-7 trabajos. Para un Magíster se esperan 15-20 trabajos cubriendo:

- Clasificación de sexo en neuroimagen (varios)
- Predicción multimodal (varios)
- Predicción multiescala (varios)
- Crítica metodológica / replicabilidad (Sapuan 2026, Messé 2020 — bien)
- Interpretabilidad en clasificación cerebral (faltan)

### Trabajos específicos que deberías incluir

**Clasificación de sexo específica:**

- **Zhang et al. (2018)** — ya en bibliografía pero usar más en este capítulo. Documenta diferencias funcionales por sexo.
- **Weis et al. (2020, Cerebral Cortex, "Sex Classification by Resting State Brain Connectivity")** — uno de los benchmarks de referencia.
- **Ebel et al. (2023) o trabajos recientes en sex classification con grafos** — verificar literatura 2024-2025.
- **Chekroud et al. (2016, NeuroImage)** o **Anderson et al. (2019)** — trabajos clásicos.

**Multimodal en neuroimagen:**

- **Calhoun & Sui (2016, Biological Psychiatry, "Multimodal fusion of brain imaging data")** — review autoritativa.
- **Sui et al. (2023)** o reviews más recientes de multimodal fusion.

**Multiescala más allá de lo que tienes:**

- **Akiki & Abdallah (2019)** — ya mencionado, multiescala funcional.
- **Bassett & Sporns (2017, Nature Neuroscience)** — "Network neuroscience" review que conecta multiescala con conectómica.

**Interpretabilidad en clasificación cerebral:**

- **Eitel et al. (2019, NeuroImage)** o trabajos similares — SHAP/LRP aplicado a neuroimagen.
- **He et al. (2025)** que ya citas hace análisis de importancia — discútelo más a fondo.

### Estructura sugerida

Reorganizar en subsecciones temáticas en lugar de un flujo narrativo continuo:

```
3.2 Clasificación de sexo basada en neuroimagen
   3.2.1 Enfoques unimodales tempranos
   3.2.2 Aproximaciones con Deep Learning
   3.2.3 Métodos basados en grafos
3.3 Integración multimodal
   3.3.1 Estrategias de fusión
   3.3.2 Aplicaciones en clasificación
3.4 Análisis multiescala
   3.4.1 Multiescala paralelo
   3.4.2 Multiescala jerárquico
3.5 Críticas metodológicas y replicabilidad
3.6 Síntesis: el vacío que aborda esta tesis
```

Esta estructura permite que **al final del capítulo** una **tabla comparativa** muestre tu propuesta vs los trabajos previos en columnas: Modalidad / Escalas / Subcortical / Interpretabilidad / Tarea / Dataset. Es la mejor manera de hacer visible tu vacío y se convierte en la figura más citable del capítulo.

### Comentarios sobre la discusión actual

**Sobre Liu et al. (2023) y Shehzad et al. (2025)** — los criticas correctamente por no incluir subcorticales y por ser unimodales. Pero falta mencionar que **usan accuracies altas (88.9%, etc.) que justamente Sapuan 2026 cuestiona**. Conectar explícitamente: _"Notablemente, estos trabajos reportan accuracies superiores al 88%, en un rango que Sapuan et al. (2026) identifica como sospechoso de explotar confundidores metodológicos. Ninguno de los dos trabajos realiza un análisis de estabilidad o validación de invarianza para descartar esta posibilidad."_ Eso amarra muy fuerte tu motivación.

**Sobre Hu et al. (2019)** — accuracy de 98.06% en clasificación de sexo es justamente el tipo de resultado que Sapuan critica. Discútelo críticamente, no neutralmente.

### Imágenes sugeridas

- **Tabla comparativa de trabajos previos** (mencionada arriba) — es la figura más importante del capítulo.
- La Figura 3.1 (taxonomía de Tang) está bien. Mantenerla.
- La Figura 3.2 (BrainMGT) está bien. Mantenerla pero quizás complementar con un esquema simplificado de tu propio enfoque al lado, para contraste visual.
- Considerar un **diagrama de Venn** o **matriz 2×2** mostrando dónde se ubica cada trabajo previo en términos de los ejes multimodal/multiescala/subcortical/interpretable. Visualmente muy efectivo.

---

## Capítulo 4 — Propuesta

### Lo que funciona bien

La estructura clásica hipótesis → objetivo general → objetivos específicos → metodología está bien. El diseño ablativo 2×2 es excelente y es lo más fuerte de tu propuesta metodológica.

### Problemas y sugerencias específicas

**4.2 Hipótesis** — Tu hipótesis tiene dos cláusulas:

1. Existe un rango óptimo de escalas que maximiza accuracy.
2. La integración multiescala-multimodal permite identificar features invariantes.

Estas son dos hipótesis distintas. Considera reformular como **H1** y **H2** separadas, y agregar una **H3** opcional sobre la contribución sinérgica:

- **H3**: La combinación de multiescala y multimodalidad produce ganancias en accuracy y estabilidad de features mayores que la suma de sus aportes individuales (interacción sinérgica detectable por el diseño ablativo 2×2).

Tres hipótesis claras y testables son más rigurosas que una hipótesis compuesta.

**4.3 Objetivo General** — Como mencioné al principio, hay que decidir si incluye predicción de edad o no. Si la incluyes, el objetivo se enriquece y permite preguntas adicionales valiosas. Si no, eliminar la mención.

**4.4 Objetivos Específicos** — Los OEs 1 y 2 son metodológicos (generar conectomas, extraer features) y los OEs 3 y 4 son analíticos (evaluar impacto, analizar interpretabilidad). Bien estructurado. Pero:

- **OE 1** debe mencionar explícitamente la **incorporación de regiones subcorticales** porque es uno de tus pilares conceptuales y actualmente queda implícito.
- **OE 4** menciona "estabilidad entre escalas de parcelación" pero esto merece ser un objetivo independiente, ya que es central a H2 y H3. Considera un **OE 5**:
    
    > _"Identificar el rango de escalas de parcelación donde las características discriminativas son más estables, mediante análisis de correlación de rankings de importancia entre escalas adyacentes."_
    

### 4.5 Metodología — sección por sección

**Datos**

- Bien descrito técnicamente. Algunos detalles a agregar:
    - **Distribución por sexo** en los 721 sujetos (¿está balanceada?). Si está desbalanceada, anticipar cómo lo manejarás (stratified split, class weights, SMOTE).
    - **Distribución de edad**. Histograma sería deseable.
    - Mencionar los **criterios de exclusión** además de "datos faltantes": ¿calidad de imagen? ¿movimiento excesivo? ¿esto es relevante específicamente por Sapuan 2026?
    - **Imagen sugerida**: histograma de edades estratificado por sexo y un diagrama del flujo de inclusión/exclusión (tipo CONSORT).

**Preprocesado y parcelación cerebral multiescala**

- Aquí hay una omisión importante: el **preprocesamiento de las dMRI y fMRI**. Sólo mencionas la parcelación, pero antes de eso hay un pipeline largo: corrección de campo B0, susceptibilidad, movimiento, eddy currents, registro a anatómica, etc. para dMRI; corrección de movimiento, registro, regresión de ruido, smoothing, etc. para fMRI. Mencionar al menos qué herramientas usarás (FSL, MRtrix, fMRIPrep, QSIPrep, etc.).
- **Niveles de parcelación**: dices "200 a 1000". ¿En qué pasos? ¿Cada 100? ¿En escalas logarítmicas? Definir explícitamente: por ejemplo {200, 300, 400, 500, 600, 700, 800, 900, 1000} → 9 escalas. Esto importa porque el número de configuraciones experimentales se multiplica.
- **Integración subcortical**: no especificas qué atlas subcortical usarás ni cómo balancearás. La opción metodológicamente más coherente es **Tian et al. (2020)** porque está disponible en 4 escalas (~16, 32, 50, 54 regiones por hemisferio) que pueden emparejarse con las escalas corticales de Schaefer/Prieto. Esto resuelve el problema topológico que mencionaste en la introducción y debes explicitarlo aquí.
- **Imagen sugerida**: diagrama del pipeline de preprocesamiento → parcelación → matriz de conectividad, con una rama para dMRI y otra para fMRI, convergiendo en el sujeto.

**Construcción de grafos y extracción de características**

- Falta especificar:
    - ¿Cómo se umbraliza el grafo, si se umbraliza? ¿Grafos completos? ¿Top-K? ¿Threshold absoluto?
    - ¿Cómo manejas correlaciones negativas en FC? (Tomar valor absoluto, eliminar negativas, o tratarlas separado — cada opción tiene implicancias).
    - ¿Cómo normalizas las matrices de SC entre sujetos? (SIFT2 está mencionado en marco teórico, repetir aquí).
- **Cuántas features por escala**: con ~30 métricas y N regiones, en una escala de 400 regiones tienes ~30 features globales + ~30×400 features locales = ~12.000 features por sujeto por modalidad por escala. Multiplica por 2 modalidades × 9 escalas y estás en ~216.000 features por sujeto. Discutir manejo de dimensionalidad: PCA, selección de features, regularización L1, etc.
- **Imagen sugerida**: tabla de features por nivel (local/mesoscala/global) con el número que se extrae por sujeto en cada escala.

**Modelado predictivo y diseño ablativo**

- El diseño 2×2 está muy bien planteado. Algunos puntos a reforzar:
    - **Configuración (i) baseline**: ¿cuál escala única? Hay que justificarlo. Lo más defendible es elegir la escala más usada en literatura comparable, ej. Schaefer 400 (es el estándar de facto). Mencionarlo explícitamente.
    - **Configuración (ii) multiescala unimodal**: ¿cómo se integran las features de múltiples escalas? Concatenación simple, late fusion con voting, stacking? Definir.
    - **Configuración (iii) escala única multimodal**: misma pregunta de fusión entre modalidades.
    - **Configuración (iv) multiescala multimodal**: ¿cómo se combinan ambas? Esto es no trivial. ¿Concatenas todo en un único vector y entrenas un solo modelo, o tienes modelos especializados por escala/modalidad y haces ensemble?
- **Validación cruzada**: dices 10-fold stratified. Bien, pero conviene también:
    - Mantener un **held-out test set** separado (ej. 15-20% de sujetos nunca vistos durante CV) para reportar accuracy final no sesgada.
    - **Anidar la búsqueda de hiperparámetros** (nested CV) para no sobreestimar performance. Mencionarlo.
    - **Tests estadísticos** para comparar configuraciones: McNemar, corrected resampled t-test (Nadeau & Bengio 2003) o tests de permutación.
- **Imagen sugerida**: el diagrama 2×2 del diseño ablativo. Esta es la figura conceptual más importante de tu propuesta y debe estar ahí.

**Interpretabilidad y análisis de características**

- Bien planteado. Para fortalecer:
    - Especificar que SHAP será **TreeSHAP para Random Forest** (exacto y rápido) y **KernelSHAP para SVM/LR** (aproximado).
    - Análisis a tres niveles: (a) features más importantes globalmente; (b) cómo cambian entre escalas; (c) cómo cambian entre modalidades. Cada uno responde una pregunta distinta.
    - Mencionar que reportarás **mapas de importancia en superficie cortical** — esto es lo que conecta features (que son números abstractos) con neurobiología (regiones cerebrales). Es enormemente más interpretable visualmente. Herramientas: nilearn, surfplot.
- **Imagen sugerida**: mockup de un mapa cortical de importancia SHAP por región — comunica visualmente qué entregará la tesis al final.

**Análisis de estabilidad entre escalas**

- Esta subsección es breve y debería expandirse porque es lo más innovador de tu propuesta.
- Especificar:
    - ¿Correlación de Spearman entre qué exactamente? Entre los rankings de importancia de features comunes entre escalas (pero las features NO son las mismas entre escalas si dependen del número de regiones). Esto necesita más cuidado conceptual. Una opción: agregar las features a métricas globales (un valor por sujeto por métrica) para que sean comparables entre escalas.
    - Definir operacionalmente "rango óptimo": ¿el rango donde la correlación inter-escala excede un threshold? ¿Donde una métrica de estabilidad muestra un plateau?
    - Considerar análisis adicionales: **bootstrap por sujeto** para estimar variabilidad, **comparación con un baseline aleatorio** (parcelación random) como hizo Messé 2020 para descartar que la estabilidad observada sea trivial.
- **Imagen sugerida**: mockup de una curva de "estabilidad vs escala" con un rango sombreado marcando el óptimo predicho por tu hipótesis. Muy comunicativo.

### Algo importante que falta en metodología

**Manejo de confundidores**. Sapuan 2026 es tu referencia más fuerte para motivar el trabajo, pero no abordas su crítica metodológicamente. Para responder a esa crítica deberías:

1. **Controlar por tamaño intracraneal total (TIV)** explícitamente como covariable o normalizando volúmenes. Sapuan demuestra que sin esto, los modelos exploran TIV como proxy de sexo.
2. **Controlar por movimiento en cabeza** (FD media) en fMRI, que difiere por sexo.
3. **Validación en dataset externo** idealmente, aunque sea como análisis exploratorio. Si HCP-A es tu dataset principal, podrías reservar un subconjunto o usar HCP-YA o UKBiobank como validación externa.

Agregar una subsección explícita "Control de confundidores" demuestra que has internalizado la crítica de Sapuan y no estás simplemente citándola decorativamente.

### Referencias adicionales para metodología

- **Nadeau & Bengio (2003)** — corrected resampled t-test para comparar modelos en CV
- **Pedregosa et al. (2011)** — scikit-learn formal
- **Esteban et al. (2019)** — fMRIPrep
- **Cieslak et al. (2021)** — QSIPrep
- **Smith et al. (2013)** — SIFT (ya mencionado pero sin cita formal)

---

## Capítulo 5 — Plan de Trabajo

### Lo que funciona bien

Las tareas están bien desagregadas por objetivo específico. La trazabilidad objetivo → tareas es clara.

### Problemas

**Falta una carta Gantt o cronograma.** Un plan de trabajo sin cronograma no es realmente un plan. Debe haber:

- Estimación temporal por tarea (semanas o meses)
- Diagrama de Gantt mostrando paralelismos y dependencias
- Hitos (milestones): ej. "Conectomas completos para todos los sujetos", "Primer modelo baseline entrenado", "Análisis de interpretabilidad completo", "Borrador de tesis listo"
- Distinción entre tareas ya completadas y tareas pendientes

**Falta gestión de riesgos.** Un plan de trabajo de Magíster debería anticipar qué puede salir mal y cómo mitigarlo. Por ejemplo:

- ¿Y si la adaptación del método de Prieto a HCP-A no produce parcelaciones jerárquicas razonables? Plan B: usar solo Schaefer.
- ¿Y si la integración subcortical con Tian no se logra dentro del cronograma? Plan B: usar aseg de FreeSurfer reconociendo la limitación.
- ¿Y si los recursos computacionales son insuficientes para procesar 721 sujetos × 9 escalas × 2 modalidades? Plan B: subset estratificado.

**Considera agregar tareas de diseminación**: redacción de paper, presentación en congreso, preparación de código reproducible (GitHub).

### Imagen sugerida

- **Carta Gantt completa** del proyecto. Es la imagen estándar y obligatoria para un plan de trabajo.

---

## Capítulo 6 — Avances

Está vacío en el documento actual. Si tienes avances reales (parcelaciones ya generadas, baseline ya entrenado, features ya extraídas en alguna escala), este capítulo debe poblar con resultados preliminares, gráficos y discusión inicial. Si es así, los avances que reportes deben:

- Validar que el pipeline funciona end-to-end aunque sea en un subset.
- Mostrar resultados del baseline (escala única unimodal) — esto demuestra factibilidad técnica.
- Si tienes preliminares en multiescala, mostrar tendencias incluso si son anecdóticas.

Si no tienes avances aún, declararlo explícitamente y mover el capítulo a una sección de "trabajo en curso" en el plan.

---

## Bibliografía — Revisión

### Problemas detectados

1. **Citas en crudo en el texto** que no resuelven con la bibliografía: `Ritchie2018`, `basser1994mr`, `tournier2007robust`, `jeurissen2014multi`, `Smith2013`, `Friston1994`, `Hansen2020`, `NetworkX`, `Latora2001`, `Eppstein2013`, `Rodrigue2024`, `PankajTibrewal2023`, `scikit-learn`, `Koehrsen2017`, `Golbeck2013`, `Clauset-Newman-Moore`. Hay que agregarlas a la .bib o reformatear citas.
    
2. **Referencias en bibliografía que no se citan en el texto**: Armstrong 2016, Baecker 2021, Baghernezhad 2024, Boss & Seegmiller 1981, Chang 2023, Chen 2020, Franke 2013, 2019, Grady 2012, Hedderich 2021, Huang 2022, Jenkinson 2012, Khazaee 2015, Krampe 2002, Kumari 2024, Marcus 2011, More 2023, Mori 1999, Uddin 2008. Muchas de éstas parecen ser de tu trabajo previo en age prediction. Decisión: si mantienes age prediction en el objetivo general, citarlas en el lugar relevante; si no, eliminarlas para no contaminar la bibliografía.
    
3. **Fuentes "blog" o no académicas**: `Koehrsen2017` (parece ser un blog post de Towards Data Science), `PankajTibrewal2023` (idem probable). Para una tesis de Magíster es preferible citar libros o papers en lugar de blogs. Alternativas: Hastie, Tibshirani & Friedman para SVM/RF; Bishop "Pattern Recognition and Machine Learning"; Goodfellow, Bengio & Courville para deep learning.
    

### Referencias clave que faltan y son altamente recomendables

**Replicabilidad y crítica metodológica (refuerza tu motivación junto a Sapuan):**

- Botvinik-Nezer et al. (2020). _Variability in the analysis of a single neuroimaging dataset by many teams_. Nature 582, 84-88.
- Marek et al. (2022). _Reproducible brain-wide association studies require thousands of individuals_. Nature 603, 654-660.
- Poldrack et al. (2017). _Scanning the horizon: towards transparent and reproducible neuroimaging research_. Nature Reviews Neuroscience 18, 115-126.

**Parcelación (complementa Schaefer y Prieto):**

- Glasser et al. (2016). _A multi-modal parcellation of human cerebral cortex_. Nature 536, 171-178.
- Eickhoff, Yeo & Genon (2018). _Imaging-based parcellations of the human brain_. Nature Reviews Neuroscience 19, 672-686.
- Pauli, Nili & Tyszka (2018). _A high-resolution probabilistic in vivo atlas of human subcortical brain nuclei_. Scientific Data 5, 180063.

**Diferencias por sexo en neuroimagen (más allá de Ingalhalikar y Zhang):**

- Joel et al. (2015). _Sex beyond the genitalia: The human brain mosaic_. PNAS 112, 15468-15473.
- Weis et al. (2020). _Sex Classification by Resting State Brain Connectivity_. Cerebral Cortex 30, 824-835.
- Ritchie et al. (2018). _Sex Differences in the Adult Human Brain_. Cerebral Cortex 28, 2959-2975.

**Conectividad SC-FC:**

- Honey et al. (2009). _Predicting human resting-state functional connectivity from structural connectivity_. PNAS 106, 2035-2040.
- Suárez et al. (2020). _Linking Structure and Function in Macroscale Brain Networks_. Trends in Cognitive Sciences 24, 302-315.

**Movimiento en fMRI (crítico por Sapuan):**

- Power et al. (2014). _Methods to detect, characterize, and remove motion artifact in resting state fMRI_. NeuroImage 84, 320-341.

**Pipelines de preprocesamiento estándar:**

- Esteban et al. (2019). _fMRIPrep: a robust preprocessing pipeline for functional MRI_. Nature Methods 16, 111-116.
- Cieslak et al. (2021). _QSIPrep: an integrative platform for preprocessing and reconstructing diffusion MRI data_. Nature Methods 18, 775-778.

**ML y comparación de modelos:**

- Pedregosa et al. (2011). _Scikit-learn: Machine Learning in Python_. JMLR 12, 2825-2830.
- Nadeau & Bengio (2003). _Inference for the generalization error_. Machine Learning 52, 239-281.
- Breiman (2001). _Random forests_. Machine Learning 45, 5-32.
- Hastie, Tibshirani & Friedman (2009). _The Elements of Statistical Learning_. Springer.

**Multiescala adicional:**

- Akiki & Abdallah (2019). _Determining the Hierarchical Architecture of the Human Brain Using Subject-Level Clustering of Functional Networks_. Scientific Reports 9, 19290.
- Bassett & Sporns (2017). _Network neuroscience_. Nature Neuroscience 20, 353-364.

**Multimodal:**

- Calhoun & Sui (2016). _Multimodal fusion of brain imaging data: A key to finding the missing link(s) in complex mental illness_. Biological Psychiatry: Cognitive Neuroscience and Neuroimaging 1, 230-244.

---

## Resumen ejecutivo de cambios prioritarios

Si tuvieras que ordenar los cambios por impacto/esfuerzo, los priorizaría así:

### Alta prioridad (cambios estructurales que mejoran sustancialmente el documento)

1. Resolver inconsistencia título/hipótesis/objetivos sobre predicción de edad vs sexo.
2. Cambiar sistemáticamente "género" por "sexo".
3. Sanear bibliografía: citas rotas + referencias huérfanas + agregar las clave que faltan.
4. Expandir sección 2.6.5 (Multiescala) y crear sección 2.10 (Interpretabilidad/SHAP).
5. Reorganizar Capítulo 3 en subsecciones temáticas con tabla comparativa final.
6. En metodología: agregar subsección explícita de control de confundidores (TIV, movimiento).
7. Especificar qué atlas subcortical se usará y cómo (Tian 2020 es la elección natural).
8. Agregar carta Gantt al plan de trabajo.

### Media prioridad (refuerzan rigor)

9. Definir explícitamente cómo se combinan features en cada configuración del 2×2.
10. Agregar tests estadísticos para comparación entre configuraciones.
11. Mencionar held-out test set y nested CV.
12. Definir operacionalmente "rango óptimo" y "estabilidad".
13. Recortar secciones 2.9 y 2.9.1 (ML básico) que están sobre-explicadas.

### Baja prioridad (pulido)

14. Agregar las figuras sugeridas a lo largo del documento (preferentemente conceptuales hechas por ti, no solo extraídas).
15. Reemplazar citas a blogs por referencias académicas.
16. Tabla resumen de métricas de grafo en lugar de lista enumerada.

---

## Sobre las imágenes — recomendación general

A lo largo del documento sólo hay 4 figuras y todas son extraídas de otros papers. Para una propuesta de Magíster se esperan **figuras conceptuales propias** que comuniquen visualmente las ideas centrales del trabajo. Las que más impacto tendrían:

1. **Figura conceptual de apertura** (Capítulo 1): el mismo cerebro a 3 escalas con sus matrices de conectividad.
2. **Diagrama 2×2 del vacío en la literatura** (Capítulo 3): trabajos previos vs tu propuesta.
3. **Pipeline completo** (Capítulo 4): desde imágenes crudas hasta predicción, mostrando todas las decisiones metodológicas.
4. **Diagrama 2×2 del diseño ablativo** (Capítulo 4): las 4 configuraciones experimentales.
5. **Mockup de mapa cortical de importancia SHAP** (Capítulo 4): qué entregará la tesis.
6. **Mockup de curva de estabilidad vs escala** (Capítulo 4): cómo se verá la respuesta a H1.
7. **Carta Gantt** (Capítulo 5).

Estas 7 figuras propias, sumadas a las extraídas que ya tienes, elevarían sustancialmente la calidad visual del documento y harían el argumento mucho más fácil de seguir para el comité evaluador.
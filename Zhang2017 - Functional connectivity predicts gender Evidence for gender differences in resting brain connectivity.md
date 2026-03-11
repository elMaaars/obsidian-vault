
# Abstract
- Sintomas de patologías varían entre hombres y mujeres.
- 820 sujetos sanos de HCP.
- Uso de rs-fMRI y modelo de regresión de minimos cuadrados (?)
- Accuracy del 87%, resultados muestran influencia de regiones de la *default mode network*.
- **Importancia**: El genero es un elemento clave en estudios con imágenes cerebrales.

# Intro
- "*Males on average tended to exhibit more intra-hemispheric connectivity whereas females appeared to exhibit more inter-hemispheric connectivity (Ingalhalikar et al. 2014)*"
- Un trabajo previo de los mismos autores mostró que los hombres tenían mejore *local clustering*, mientras que las mujeres tenían mejor *global clustering* (en medidas de grafo).

# Mat y Met
- Se usan 160 regiones. (Dosenbach atlas)
- Utilizan solo la triangular (12720 valores de conectividad).
- Tiene 4 tomas para los sujetos, esto les permite probar:
	- Promedio entre las 4 tomas.
	- Unir las 4 tomas en una y sacar conectividad.
	- Sacar 4 conectividades y concatenar.
- Usan *partial least squares* para abordar problemas de dimensionalidad. Se usa también *10 fold cross validation* y normalización (z-transform).
- Las features terminan siendo nodos, asociados a alguna "zona funcional" del cerebro.

# Disc y conclusión
- Accuracy sobre 85% en múltiples experimentos.
- La conectividad dentro de la DMN mostró las mayor importancia para la clasificación. 
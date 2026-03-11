# Intro
- BrainMGT incluye mutliples escalas espaciales y también temporales. Naturalmente esto es solo para fMRI.
- Teoría de grafos es clave. Sirve para estudiar AD o ASD identificando anomalías en la conectividad.
- Normalmente se usa un atlas y la correlación de Pearson. Usar una escala es una limitación.
- Los métodos multiescala suelen usar diferentes atlases. Esto es un problema porque la data no está integrada entre las escalas. Además solo usan una escala temporal.
- Prueban en 3 bases de datos.

# Mat y Met
- Una escala no captura las dinámicas complejas de la conectividad.
- Otros trabajos como el de Yao integran información multiescala con algoritmos de aprendizaje sobre grafos. Otros han tenido avances pero fallan en capturar completamente las interacciones entre escalas.
- GNNs fallan con contexto, GT usan atención para abordar toda la info de los nodos, local y globalmente.
- BrainMGT tiene dos componentes:
	- Uno crea las conectividades a diferente escala.
	- Otro aprende de los grafos generados. Este es el transformer.
- El primer componente realiza un preprocesamiento, antes de cada una de las escalas:
	- La microescala usa Schaefer 7-module con 1000 nodos.
	- La mesoescala usan 500 comunidades definidas desde la microescala. Se mapean luego a los 7 modulos de Schaefer.
	- La macroescala agrega las 500 comunidades en 100 comunidades grandes. También se mapean.
	- Trabajan con frecuencias BOLD rápidas, intermedias y lentas. La primera es para procesamiento local, segunda para funciones cognitivas e interacciones regionales y la última para comunicación larga distancia ya coordinación a gran escala.
	- Existen conexiones dentro de cada escala y entre módulos funcionales:
		- Intra módulo son conexiones entre nodos pertenecientes al mismo módulo funcional (bloques diagonales de la matriz).
	     - Inter módulo son  conexiones entre nodos de distintos módulos funcionales (bloques fuera de la diagonal).
- El segundo es el transformer en si compuesto de *embeddings de entrada*, *encodings de posición, intra escala e inter escala*.
- Se usan 3 datasets, cantidad de sujetos aproximada de 1850.

# Resultados
- Comparan con otros benchmarks de modelos convencionales. **REMARCAN QUE OPERAN EN REDES DE UNA SOLA ESCALA A PARTIR DE FMRI**. Sacan features y usan ajuste de parametros con gridsearch.



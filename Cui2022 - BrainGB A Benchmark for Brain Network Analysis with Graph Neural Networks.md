# Intro
- Interacciones entre regiones son clave para el desarrollo neuronal y análisis de ciertos desordenes. Grafos pueden describir estas interacciones.
- Esfuerzos previos han estudiado modelos basados en grafos y *tensor factorization* enfocandose en medidas de grafo útiles neurobiológicamente. Algunas que ya se han establecido son **modularidad**, la **jerarquia**, **centralidad** y **distribución de los *network hubs***.
- Brain GB es un framework unificado, modular y escalable, además proveen sugerencias para nuevos estudios.

# Preliminares (Intro 2?)
- Abordan el analisis de redes cerebrales en función de los conectomas definidos como matrices. Menciona la dificultad de la existencia de diferentes métodos para la obtención de conectomas. Aborda también las GNNs y su funcionamiento, con enfasis en las diferencias de los grafos de redes cerebrales con grafos normales. También se mencionan problemáticas asociadas a la privacidad de los datasets.

# Mat y Met (?)
- Usan redes derivadas de MRI (fMRI y dMRI). Se enfatiza dificultad en cantidad y compatibilidad de softwares. 
- Al abordar el procesamiento de los datos para obtención de conectomas funcionales mencionan la transformada de Fisher. En conectoma estructural recalcan la robustez de la tractografía probabilística. 
- Para las caracterísitcas consideran (solo 1 a la vez):
	- Identity: Matriz que tiene un 1 por fila represetando cada nodo. Es como una identidad.
	- Eigen: Calculan los *k* mejores eigenvectors para generar un vector *k*-dimensional para cada nodo.
	- Degree: El grado de los nodos.
	- Degree profile: Medidas de tendencia central de un nodo en una vecindad de 1 de distancia.
	- Connection profile: La columna de cada nodo en la matriz se utiliza como feature.
- Luego se discuten los mecanismos de actualización de la GNN desde los más básicos a algunos más elaborados. Junto a esto se abordan distintos métodos de atención y *pooling*.
- Consideran 4 datasets: *HIV*, *PNC*, *PPMI* y *ABCD*.
- **Normalizan estructurales, dividen por el valor máximo en un _sample_**, así quedan entre 0 y 1. 
- **Para funcionales remueven los negativos para GNNs que no los soportan y los dejan en aquellas que si**.

# Resultados
- *Connection profile* resulta ser la mejor feature. *Node concat* y *node edge concat* son los mejores para actualización (ver con más detalle en paper) y mejoran al incluir atención. Finalmente para el *pooling*, *concat pooling* supera a los demás métodos. 
- Aclaran que los niveles de densidad impactan los hiperparametros en las GNNs. Así, modifican la arquitectura.

# Conclusiones
- La efectividad puede verse limitada por el tamaño de los datasets. Se desconoce qué tipo de estructuras en grafos son efectivas más allá de la conexión entre pares.
- Proponen agregar neurología y pre entrenamiento.



# Abstract
- Usan *"Multi-layer 3D convolution extreme learning machine (MCN-ELM)"*.
- Eso se aplica sobre MRI estructurales.
- BD es HCP con 876 sujetos sanos.
- Accuracy de 98%, 10 fold cross validation.
- **Importancia:** Entender diferencias entre cerebros de hombres y de mujeres.

# Intro
- Existen diferencias conocidas en funciones o comportamientos. Ej: tareas visuoespaciales o reconocimiento de emociones.
- Joel. et al concluye que no existen cerebros de hombre y de mujer. Este trabajo afirma lo contrario en base a sus resultados.
- Reconocen limitaciones del enfoque de *deep learning* (muchos datos, tiempo).

# Mat y Met
- 876 sujetos sanos de HCP.
- Utilizan espacio MNI. El input de la red es la data de la materia gris.
- Se utilizan 3 redes. Una pequeña enfocada en información detallada, una mediana enfocada en información local y una grande enfocada en información global. 
- Las 3 redes dan un vector cada una. Cada uno va a un clasificador ELM separado que arroja un resultado. 
- Estos resultados pasan por una votación (al ser 3 siempre habrá un resultado mayoritario) para el output final.

# Resultados
- Aumentar la cantidad de nodos ocultos sobre 9000 lleva precisiones sobre el 90% de manera consistente.
- El método propuesto se compara con SVM, KNN y LDA, con mejores resultados.
- Se realizan comparaciones de métodos de reducción de dimensionalidad, con el método propuesto superando a *t-test* y *PCA*.

# Disc y conclusión
- Trabajo futuro puede centrarse en una mejor inicialización de los pesos del ELM, pues se muestra que es sensible a eso.
- El método *outpeforms* otros en el nivel del SOTA.
- Se sugiere que el tratamiento psiquiátrico puede tener mejores resultados al abordarse por género.
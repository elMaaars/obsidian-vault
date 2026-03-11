- En problemas con demasiadas variables usualmente se requiere de una reducción de dimensionalidad.
- Generalmente se usa PCA pero esto solo se enfoca en reducir la dimensionalidad lo mejor posible, sin importar si esta reducción es útil para la predicción. Busca maximizar la reducción.
- PSL hace algo parecido a PCA (sigue creando componentes nuevas basadas en combinaciones lineales de las componentes originales) pero asegurándose que estas tengan relación con el valor a predecir.
- **PCA maximiza la varianza en X mientras que PSL incorpora una maximización de la covarianza entre X e Y.**

# PSL Regression
- Cuando se aplica PSL se obtiene un set vector de nuevas componentes que describen los datos originales, un nuevo conjunto de características creado a partir de las características originales.
- Estas nuevas features se pueden utilizar para predecir una variable continua. Así, para clasificación binaria, se pueden establecer umbrales que nos permitan diferenciar cuando se está en presencia de qué clase. 
- En el caso particular 
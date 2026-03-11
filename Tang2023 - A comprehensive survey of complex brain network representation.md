
# Intro
- Neuroimágenes permiten estudio de patrones de funcionamiento internos del cerebro.
- Métodos tradicionales = No Deep Neural Networks. Extraen features predefinidas para propósitos especificos:
	- Heterogeneidad topológica usando *betweenness centrality*
	- Similaridad de las redes usando medidas de distancia o *kernels*
	- Frecuencia mediante *spectrum feature analysys*.
- PCA suele usarse para dimensionalidad. Estos modelos pueden ser subóptimos pues no logran utilizar toda la información de la red.
- 4 tipos principales:
	- Multimodal brain network: integrar multiples modalidades.
	- Multiscale brain network: integrar multiples escalas.
	- Dynamic brain network: integrar tiempo y dinámica de señales.
	- Interpretable brain network: priorizar interpretación.

# Marco teórico (?)
- Definiciones de red cerebral con grafos, tipos de redes e importancia de parcelación. Definen redes estructurales, funcionales, morfológicas y efectivas.
- Se abordan datasets y herramientas para la tarea.
- Medidas topóligicas (más detalles en **Rubinov and Sporns** y en BCT-Toolbox hay implementaciones y la tabla 3 da más info):
	- Degree y strenght.
	- Node density y *Rentian scaling*.
	- Clustering coeff., *mularity* y transitivity.
	- *Rich club coeff.* y *core/periphery* structure.
	- Path lenght y *cycle probabilty*.
	- Global/local efficiency y *diffusion eficiency*.
	- Betweenness centrality y *within module degree z score*.
- Los métodos de kernel en grafos computan similaridad entre dos grafos. Estas similaridades pueden ser features.
- Spectral graph analysis no nos interesa xd.
- Varios análisis estadísticos pueden ser aplicados (t-test, ANOVA para significancia).
- Tabla 5 = resultados de modelos multimodales y multiescala en género en HCP.
- Insights de dificultades incluye poco estudio mediante grafos dirigidos, pocos datos en algunos subgrupos, interpretabilidad, falta de validación clinidca real.


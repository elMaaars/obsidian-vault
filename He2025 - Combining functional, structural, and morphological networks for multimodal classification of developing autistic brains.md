#multimodal #multiscale #autism
# Intro

- Uso de fMRI, DTI y sMRI para construcción de matrices. 97 sujetos, 50 autistas.
- Accuracy de 82% al combinar, mejor que por separado.
- Features más importantes:
	- Temporal, parietal y occipital en DTI.
	- Prefrontal y parietal en fMRI.
	- Temporal en sMRI.
- Verificado que la conectividad estructural soporta la conectividad funcional. Conectividad funcional sigue la plasticidad de la conectividad funcional. Similitud entre conectividaes.
- Importancia de estudios multimodales.
- Para autismo, la combinación ha mejorado los resultados.

# Mat y Met
- Datos del ABIDE 2. Imágenes de alta calidad, edades 5 a 18. Criterios de adquisición detallados.
- Sujetos diagnosticados usando DSM-4.
- Se detalla el preprocesamiento de las 3 modalidades.
- Construyen 3 redes:
	- Morfometría similar: 45 nodos por hemisferio. Cortical y subcortical del AAL. Es más probabilístico. Usan el volumen de GM.
	- Conectividad estructural: 90 regiones, en base a anisotropía fraccional y el AAL. La arista es el promedio de la FA de todas las fibras conectando los nodos. Es simétrica.
	- Conectividad funcional: 90 regiones, en base al AAL. Correlación de Pearson. Normalizados con Fisher.
- Tomaron las matrices completas y las unieron para todos los sujetos. Para reducir la redundancia, ocuparon *recursive feature elimination* con validación cruzada. También tenían edad, género, full-scale IQ y el promedio del *frame wise displacement* (????)
- Usan un SVM (dicen que es bueno a pesar del N y de la cantidad de features). Usan LOO para validación cruzada.
- Usan un SVR para validar igual.
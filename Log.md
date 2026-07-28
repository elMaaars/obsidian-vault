## July 28th
- Long time no see.
- Bueno, resumen y al punto:
	- SIPAIM paper listo.
	- AC3E abstract para poster listo.
	- Nos cambiamos a XGBoost como modelo.
	- Usamos features basadas en Yeo7 en GeoSP para SIPAIM.
- Ahora lo importante y que merece ser documentado
`````
subject_set  n_subjects  n_folds  bacc_mean  bacc_std
       full         718        8   0.812481  0.039214
  no_age100         706        8   0.814369  0.033334
no_outliers         707        8   0.823443  0.029689

set_a  set_b  bacc_mean_a  bacc_mean_b  wilcoxon_stat  p_value  significant_p05
full   no_age100  0.812481  0.814369    15.0  0.742188   False
full   no_outlrs  0.812481  0.823443     8.0  0.195312   False
no_100 no_outlrs  0.814369  0.823443    11.0  0.382812   False

`````
- Lo relevante de esto es que no hay diferencias significativas (dentro de lo que cabe obviamente, con los *folds* que hacemos) al remover el grupo de sujetos marcados como de 100 años. 
## June 8th
- Peleando todo el día con visualizar un sujeto en las 3 escalas.
- Al final lo hago con `mrview`, cargo el `.nodes.nii.gz` junto con el LUT y un .obj generado con `label2mesh`. Hay que cargar una imagen también!!!!
- Al fin tengo las imagenes. 
- También corregí las desalineaciones para todos los de SchaeferTian. EL problema eran las estructurales.
- En lo respectivo a los NaNs, eran señales que "no estaban", pero no pasaban como 0s sino como NaNs lo que es bueno.
- Poco avance.
## June 5th
- Terminados los SchaeferTian.
- Todos los datos listos!
- Hay unos misalignments que hay que corregir. 
- Además se pasan unos NaNs en el proceso, pero parece que son 0s.
- Revisr en detalle.
- Avances con propuesta, sección Avances casi lista *badum tss*.
- Faltan imagenes.
## June 4th
- Propuesta principalmente, conectividad y SchaeferTian en el escrito.
- Arreglé citas, pusé pipeline de la memoria como imagen.
- Además comparé densidades en SC para GeoSP y SchaeferTian:
`````
parcellation level  count  mean_%  std_%  min_%  max_%                           
GeoSP        200    720.0   55.56   7.76  19.06  68.04
             500    720.0   31.85   5.26  10.14  40.94
             800    720.0   20.88   3.58   6.76  26.51
SchaeferTian 200    720.0   58.68   8.36  18.39  71.61
             500    720.0   32.06   5.26   9.83  40.85
             800    720.0   21.26   3.61   6.85  27.43
`````
- Son similares por lo que debe estar bien, dos fuentes diferentes, densidades similares.
- Ahora están corriendo los FC en Tian 200. 
- En la noche empiezan los Tian 500 y para el viernes en la noche están los finales.
## June 3th
- Nada, descanso en casa.
- *Psych*, escribí como 1 parrafo y una imagen en la propuesta. (Tian S1 y S2, MarcoTeórico).
- Pipeline de fMRI para Schaefer estaba problemático.
	- Se hacía una conversión de MNI a nativo para SC, pero después para FC había que ir de vuelta a MNI.
	- Eso rompía algunas cosas.
	- Solución, quedarse en MNI para FC.
## June 2st
## June 1st
- Reu con la profe en la mañana:
	- Volumenes listos, esta semana se sacan todos los datos!!
	- Profe pidio validación de que datos están bien.
	- Intentar hacer pipeline minimo para validar. 
	- Testear tiempo de métricas con pocos sujetos.
	- Pensar en como hacer análisis de edad también.
	- Revisar metodología.
- Volviendo al asunto de las densidades:
	- Yarelis dice que son 3 millones pero que tiene que confirmar.
	- De todas maneras no le parece extraño. Dijo revisara la suma de las fibras en un sujeto sin normalización por inverso del volumen. Se pierde casi la mitad de las fibras.
	- Jorge dijo que podía estar desalineado. 
	- Revisamos en mriview con el volumen y la tractografía y están bien.
- Probé el pipeline de extracción con un sujeto de 850 de parcelación.
	- Extraje 24 métricas en 15 segundos.
- Terminé sección de GeoSP en avances. Tentativamente.
- Ahora veo sección de decidir las escalas.
- También reorganicé las carpetas. Schaefer estaba muy desordenado.
## May 29th
- Resulta que hay diferencias entre brainstorm y FSL.
	- Tuve que hacer 10 sujetos de prueba y comparar con el volúmen del sujeto de HCP.
	- FSL es mejor.
	- Ahora si terminamos los volumenes.
- Me di cuenta que al ver en `freeview` faltaban trozos de la corteza y estaba todo mal etiquetado.
	- Con Seba me puse a ver y era el LUT default del software.
	- Hice LUT custom y quedó bien.
- Continué con la propuesta, lentamente.
## May 28th
- Avances de la propuesta.
- Capítulo de avances ahora tiene estructura y comencé escribir lo que hicimos para GeoSP.
- Eso principalmente.
- Hice unión de volumenes para niveles 1 y 2.
## May 27th
- Para la propuesta:
	- Organicé mejor el SOTA, incluyo dos trabajos nuevos y tiene más sentido (uno de los trabajos soy yo!).
	- Empecé a delinear avances y apliqué otras correciones menores.
- Instalé matlab y brainstorm.
- Poco más.
## May 26th
- Terminaron las funcionales de GeoSP.
- Avances con lo de Schaefer.
- Hay opciones, ir con Brainstorm o hacer un pipeline de FSL.
- Revisé las densidades, están en 55%, 32% y 20% para los niveles 200, 500 y 800. FC están todas a 100%.
- Hay que hacer umbralización, la pregunta es cómo:
	- Opción 1: Umbral fijo.
	- Opción 2: Umbral porcentual.
	- Opción 3: Umbral procentual basado en población.
	- OJO: Yarelis tenía densidades demasiado altas, incluso en 1000 nodos, puede ser la cantidad de fibras.
- Eso no más, no mucho.
## May 25th
- Tenemos todas las matrices estructurales para GeoSP.
- Están terminando las funcionales para GeoSP también.
- Esta semana hay que trabajar en las de Schaefer y en la propuesta.
- Con el resumen de Claude he estado aplicando correcciones.
	- Puso mucho enfásis en secciones que requieren más desarrollo lo que me parece bien.
- Tuve reunión con la profe Ceci:
	- Cree que vamos bien.
	- Planteó usar todo el universo de medidas topológicas, luego filtrar.
	- Ideal sería luego de tener las más relevantes hacer análisis por zona en todos los sujetos. Buscar significancia de los resultados.
	- Aprueba el diseño ablativo.
	- Dice que hay que tener ojo con la hipótesis y hacer una metodología que esté en la misma linea.
## May 22th
- Las intersecciones de los sujetos del nivel 500 terminaron.
- Las matrices funcionales en el nivel 200 fallaron para 294 sujetos.
	- El error es que faltaba un directorio en la lista a revisar para encotrar las imagenes volumetricas de fMRI. De esos 294, hay 291 sujetos con datos. Existen 3 con datos faltantes o incompletos.
	- Hay que aceptar la pérdida.
	- Si bien están los archivos en formato `CIFTI` para todos, se requiere de una reconstrucción del pipeline un poco profunda, cambiando otros resultados y perdiendo consistencia con el método estructural.
	- La explicación más técnica es: 
		- GeoSP termina con un volumen de cerebro completo. El formato `CIFTI` (que son los datos pero en su equivalente de superficie) necesita cierta organización específica que no le estamos dando ahora a los datos.
		- En el método actual "rompemos" el "orden" en las estructuras subcorticales al dividirlas. Para que funciona necesitamos un archivo `.dlabel` (**esto lo mencionó la Cata)**. Además las divisiones son especificas por sujeto, por lo que si bien, es posible crear el `.dlabel` es mucho más engorroso. Incluso si lo intentamos, rompemos la correspondencia entre las matrices funcinoales y estructurales.
## May 20th
-  Los sujetos del nivel 500 fallaron. Faltaron cerca de 200.
	- La solución para borrar los `.annot` tenía mal el nombre del archivo. Ya está arreglado.
- Hice un *script* (fue Claude) para el procesamiento de las funcionales con las señales y los volumenes obtenidos de la proyección y unión. Está basado en el *script* que usó la Cata anteriormente. Funciona así:
	- Primero hacemos una transformación del volumen a MNI (91x109x91) que es espacio de los datos funcionales. Volvemos a usar interpolación *nearest neighbour*.
	- Luego cargamos los volúmenes y verificamos dimensiones luego de transformar.
	- Sacamos las series de tiempo para cada parcela, teniendo una señal temporal representativa de cada región. Se usa el promedio para esta señal representativa.
	- Usamos correlación de Pearson y transformada de Fisher, dejando coeficientes entre -1 y 1.
	- Guardamos en `.csv`  y en `.npy` para uso posterior.
- Respecto a los espacios funcionales-estructurales:
	- El conectoma estructural está enteramente en el espacio del nativo del sujeto (el de HCP). La imágen de fMRI está en espacio MNI por lo que no se puede hacer exactamente lo mismo. Por eso llevamos el volumen del cerebro completo a MNI.
	- A pesar de eso, las matrices y sus indices son perfectamente comparables, lo que quiere la conexión entre $S_i$ , $S_j$ es la misma que en la $F_i$, $F_j$, con *S* la matriz estructural y *F*  la funcional.
- Me econtré con la profe durante la mañana:
	- Encontró que el avance estaba bien para la propuesta. Quiere que esté lista (borrador) para la mitad de junio.
	- Dice que con los datos estructurales ya es suficiente para diseñar *pipelines* y hacer trabajo para SIPAIM.
- Al final del día terminaron los sujetos faltantes del nivel 500.
## May 19th
- Terminaron los sujetos faltantes del nivel 200.
- Empezamos con el nivel 500.
- Corregí la introducción de la propuesta y empecé correcciones al marco teórico.
## May 18th
- Resumen de procesamientos del fin de semana:
	- Viernes noche dejé sujetos procesando a nivel 200.
		- Rutas estaban malas. No corrió y me di cuenta tarde.
	- Sábado arreglé rutas y corrí mismo nivel.
		- Falló primero por `midthickness` que estaban con data duplicada. Solución fue usar las versiones recortadas que ya habíamos generado en un inicio del proyecto.
		- Luego funcionó sin problema hasta que se llenó el disco. El pipeline usa `mri_aparc2aseg` y eso genera un `.annot`en el disco como residuo. 
	- Domingo me di cuenta del disco lleno. Llegamos hasta el sujeto 622.
- Reu con la profe Ceci en la mañana.
	- Resumen de lo que he estado haciendo.
	- Sugirió tener una medida más tangible para la similitud en la reconstrucción de Desikan. *We'll check on that later.*
	- También comentó realizar pruebas con un subconjunto de los datos para asegurarnos que tenemos los datos necesarios para cualquier cosa (AKA. volver desde la parcelación a las regiones de Desikan).
- Pipeline arreglado para eliminación automática de los `.annot` asegurando espacio en los discos para procesamiento continuo.
- Con Seba conversamos un poco sobre la proyección y unión.
	- De acuerdo con lo que dice deberían existir dos `aparc+aseg` uno en espacio nativo (HCP) y el otro en espacio *conformed* (FreeSurfer). De todas formas la transformación del volumen cortical al espacio nativo no es incorrecta. Mencionó que el tipo de interpolación es clave, actualmente usamos *nearest neighbour* pero lo ideal sería *multilabel*.
	- Con respecto a lo de la reconstrucción de Desikan, Seba sugurió usar un Dice Score entre la reconstrucción y el original.
		- Esto se debe hacer posteriormente para cada sujeto, con el de prueba se obtiene un 97 de promedio, con 2 regiones obteniendo un 92. Otras alcanzan el 99.
- 
## May 15th
- Terminamos la proyección de Sachefer para todos los sujetos que faltaban en los niveles que faltaban.
- Corregí errores en el pipeline de proyección y unión.
- Los discos quedaron listos para hacer el pipeline a diferentes niveles, los subcorticales también están listos, por lo que solo queda generar los volumenes.
- Nos quedamos atrapados XD.
- Me dieron una TNE buena por fin.
## May 14th
- Terminar documentación de pasos del algoritmo de proyección y unión. (Dos entradas atrás.)
- Continuar con proyección de Schaefer para los datos del disco **Elements** en las escalas que no teníamos.
- Reunión con Yarelis para ver resultados de proyección y unión.
	- Colores hacen difícil la apreciación de las diferentes parcelas, incluso en el nivel de 200, por lo que con niveles superiores va a ser más complejo.
	- Hacer experimento de recrear Desikan. Si cortamos el árbol a 68 regiones corticales, deberíamos obtener 34 por lado (tal como DK) y juntando con 7 subcorticales por lado, tendríamos Desikan. Si al visualzar esto se corresponde con DK entonces está bien.
	- Debería funcionar.
- Funcionó.
## May 13th
- Nada.
- Documentación del algoritmo por acá. (Entrada anterior.)
- Correr proyección de Schaefer para las escalas que no teníamos (500 y 800) para el disco **Elements 2**.
## May 12th 
- Logramos hacer una proyección y unión con algo de sentido.
	- Usando un tractograma disponible en el sujeto de prueba, corrí `tck2connectome` sin errores ni warnings para un sujeto de prueba con 216 regiones.
	- Falta validación de Yarelis para hacerlo a gran escala.
- Resumen general de los pasos:
	1. Tomar el `.annot` correspondiente al sujeto en la parcelación correspondiente.
	2. Ordenamos los *labels* para que queden secuenciales. 1000+ para LH y 2000+ para RH.
	3. Hacemos un *resampling* para*FreeSurfer* (que necesita los datos en espacio nativo). Mediante un KDTree podemos pasar de 32k a espacio nativo sin mayor problema ya que ambas superficiees existen en espacio de coordenadas (**checkeado**).
	4. Guardamos el `multiscale.annot` para usarlo y tenerlo de respaldo.  **Esto se escribe en el disco externo y en multiples escalas se va a sobreescribir. Requiere parche.** 
	5. Usamos `mri_aparc2aseg` que toma el output del paso anterior y pinta. El resultado es un volumen 256 x 256 x 256 isotrópico a 1mm (el espacio de FreeSurfer).
	6. Como mencionaba antes, el problema de la unión es que ambos volumenes no comparten espacio, por lo que hay que llevar el volumen cortical al espacio de HCP. Para eso usamos `mri_vol2vol --regheader` que encuentra la transformación requerida (usando los *headers* de los volumenes) y luego hace el *resampling* a espacio HCP usando *nearest neighbour interpolation*. 
	7. Cargar los volumenes y verificamos dimensión.
	8. Reemplazamos las etiquetas subcorticales del volumen cortical asignadas por FreeSurfer (`mri_apar2aseg` produce una segmentación cerebral completa) a las generadas por el algoritmo subcortical. Usamos las etiquetas 3000+ y reasignamos los vóxeles. **El código subcortical tuvo que cambiarse a asignar una etiqueta nueva a todas las regiones, antes era solo a las que se dividían.** 
	9. Guardamos el volumen nuevo. Par el caso de 216 parcelas totales tenemos, 96 en el hemisferio izquierdo (desde 1001 hasta 1096), 104 en el hemisferio derecho (desde 2001 hasta 2104) y 16 subcorticales (3001 hasta 3017).
		- **LA DIVISIÓN Y REASIGNACIÓN DE LABELS EN EL PASO SUBCORTICAL PUEDE DEJAR GAPS.**
	10. Preparación para `tck2connectome`. Este requiere que las *labels* sean secuenciales comenzando desde 1 y todo lo que no sea WM que sea 0. Se hace un remapeo de todas las parcelas a el rango corrrecto. Para 216, queda desde 1 hasta 216. Como extra se generan un `.txt` y un `.json` que mapean las nuevas *labels* secuenciales a las antiguas, junto con el hemisferio y el tipo.
## May 11th
- Poco trabajo desde casa.
- Seguí viendo lo de proyectar y unir. La respuesta parece estar en como se hace la proyección de Schaefer.
- Con Claude tengo ahora un script que maneja toda la proyección y unión en un gran paso secuencial.
## May 8th
- Día solo en el laboratorio.
- Trabajé en proyección y unión. 
- En general casi nada funcionó. Uno de los principales obstáculos era el output de `mri_apar2aseg` de *FreeSurfer* pues para la proyección teníamos espacio de (256 x 256 x 256) isotrópico a 1mm, mientras que en HCP tenemos (227 x 272 x 227) isotrópico a 0.8mm.
- Por eso intenté hacer la proyección con otros métodos (herramientas de *wb_command*) pero no hubieron buenos resultados.
- Todos estos experimentos los hice sobre 3 sujetos de prueba que están en el disco **Elements 2**.
- Además me di cuenta que la proyección de Schaefer guarda unos archivos en la carpeta `/label` de cada sujeto por lo que también hice un script para copiarlos en caso de tener que borarlos del disco.
## May 7th
- En la mañana pude avanzar un poco con lo de la proyección. El resultado se veía bien pero escondía más de alguna pifia. Cuando lo vimos usando *FreeSurfer* en realidad lo que vi fueron las piezas por separado, pero tenía cargado el `aparc+aseg` (que tiene cortical y subcortical) por lo que realmente era un engaño.
- Gracias a Seba me di cuenta que la proyección y sobre todo la unión no era tan sencilla. Luego conversando con Yarelis supe que hay que tener ojo con los labels para que luego se pueda usar en MRtrix3 para las matrices.
- En la tarde tuve la reunión con las profes.
	- Lo principal es que las resoluciones a usar son 216 **(200 corticales + 16 subcorticales)**, 532 **(500 corticales + 32 subcorticales)** y 850 **(800 corticales + 50 subcorticales)**.
	- Esta idea viene de resultados previos de Yarelis que muestran que la máxima metaestabilidad del cerebro es a 400 parcelas.
	- Respecto a la diferencia en la cantidad de parcelas por hemisferio se desestimó el efecto ya que el total si coincide.
	- Pusieron foco en mencionar y tener bien claro cuales son los cambios al método GeoSP para tenerlo en la tesis. Explicar con detalle.
## May 6th
- Terminé la adaptación del código subcortical.
	- Me pasé los `aparc+aseg.nii.gz` desde los discos.
	- Corrí para 14 regiones subcorticales (7 por hemisferio) y para 16 (8 por hemisferio).
- Modifique el código multiscale para que guardara los annot que necesitariamos para una eventual proyección.
	- El código estaba medio complejo pero se logró. Ahora se guardan los annot para cada sujeto procesdao al crear una multiescala.
	- Pude ver la de 200 regiones corticales por el lado izquerdo. Se ven parejas al menos para los primeros 4 sujetos.
- Revisé también con freeview los annots generados para un sujeto y después de algunos intentos cargó bien lo que sugiere que los annot están bien generados.
- Mañana tengo que revisar si es posible replicar la proyección para acelerar aún más todo.
## May 5th
- Trabajé en la presentación.
- Me junté con Yarelis para comentar avances.
	- Aprobó el método para setear la cantidad de regiones corticales a obtener.
	- Me dió código nuevo para adaptar. Este corresponde a las regiones subcorticales.
		- Necesitamos archivos aparc+aseg.nii.gz que están en la base.
		- Esto da dato volumétrico como salida.
	- **Me dijo que revisara las parcelaciones corticales obtenidas a diferentes niveles para ver si se conservaba la estructura entre sujetos.**
	- **También vale la pena revisar si podemos usar lo que estabamos haciendo con Schaefer (proyectar a volumétrico) para asi usar MRtrix para unir cortical volumétrico con subcortical volumétrico. No estamos seguros si es posible.**
	- Estructuras corticales de Tian son las mismas que las que usa Yarelis pero tienen alguna que otra división extra.
		- A priori podríamos simplemente subdividir un poco el de Yarelis para ajustarnos a las cantidad de Tian.
		- Problema sigue siendo que no tendremos misma cantidad exacta de corticales por hemisferio pero si podemos tener misma cantidad total de corticales.
- Revisé y los archivos necesarios están disponibles. Hay que pasarlos mañana.
- Claude sugiere que se posible copiar la lógica de la proyección de Schaefer para las corticales. Hay que modificar extensión de archivos pero debería ser posible. Hay que intentar con un sujeto.
- Vino también Bastián Pino por asunto de sus tractografías y datos.
	- Problema era que transformo a MNI antes de hacer tractografía lo que mueve la dirección de los tensores (?). El asunto es que afecta a la tractografía.
	- Usaba también MSMT-CSD pero eran datos con un solo *b-value* pues eran clínicos. Seba recomienda usar 5ttgen.
	- Además Seba se dio cuenta que era la misma base de un trabajo de Claudio.
		- Las imágenes T1 no se podían bajar de la página porque no se les había hecho proceso de *defacing*.
- En general, día lento.
## May 4th
- Revisé que el código del corte estuviese bien.
	- Algunos sujetos tenían más de una carpeta.
		- Esto es por los intentos fallidos anteriores.
		- Ahora se salta los sujetos ya procesados bajo cierta distancia.
		- Se corrio en un `.py` para implementar paralelismo también. Antes moría por sobrecarga del kernel en el `.ipynb` y por un *"memory leak"* en algunas funciones importadas desde `hct`.
	- **El corte a 3.6 de distancia no resultó igual que el de Yarelis.** Voy a probar con otros.
		- Es por las diferencias anatómicas aparantemente.
	- También tengo una función que me permite buscar un total de regiones corticales y encontrar la distancia para eso.
		- Probé con esto y pude generar exactas 200 y 600 corticales. Éxito.
	- Además, había una parte que hace la relación que no había corrido. Ahora está integrado en el `.py`. ***Debería parametrizarse el  `.py`  para hacerle llamadas desde el  `.ipynb`***
- Fijé la reu para el jueves 07/05 a las 3pm.
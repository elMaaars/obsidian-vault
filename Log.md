


## May 12th 
- Logramos hacer una proyección y unión con algo de sentido.
	- Usando un tractograma disponible en el sujeto de prueba, corrí `tck2connectome` sin errores ni warnings para un sujeto de prueba con 216 regiones.
	- Falta validación de Yarelis para hacerlo a gran escala.
- Resumen general de los pasos:
	1. Tomar el `.annot` correspondiente al sujeto en la parcelación correspondiente.
	2. Ordenamos los *labels* para que queden secuenciales. 1000+ para LH y 2000+ para RH.
	3. 
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

## May 7th
- En la mañana pude avanzar un poco con lo de la proyecc
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
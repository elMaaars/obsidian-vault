## May 4th
- Revisé que el código del corte estuviese bien.
	- Algunos sujetos tenían más de una carpeta.
		- Esto es por los intentos fallidos anteriores.
		- Ahora se salta los sujetos ya procesados bajo cierta distancia.
		- Se corrio en un `.py` para implementar paralelismo también. Antes moría por sobrecarga del kernel en el `.ipynb` y por un *"memory leak"* en algunas funciones importadas desde `hct`.
	- **El corte a 3.6 de distancia no resultó igual que el de Yarelis.** Voy a probar con otros.
	- También tengo una función que me permite buscar un total de regiones corticales y encontrar la distancia para eso.
	- Además, había una parte que hace la relación que no había corrido. Ahora está integrado en el `.py`. ***Debería parametrizarse el  `.py`  para hacerle llamadas desde el  `.ipynb`***
	- 
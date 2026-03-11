
# Intro
- Las parcelaciones  se puede generar sobre los ***volúmenes*** o las ***superficies***. La última es más beneficiosa.
- Parcelaciones pueden venir de estructurales (atlases de fasículos, promedios de conexiones) o funcionales (características corticales).
- Diferentes niveles de parcelación (cada vez más granulares) permiten entender mejor la organización funcional-anatómica del cerebro.
- Se propone un *framework* para generar parcelaciones corticales multiescala sobre ***superficies***. Se basa en clustering jerárquico y distancia geodésica. Utilizando una particion del dendograma se consiguen diferentes parcelaciones. Se probó sobre Desikan-Killiany.

# Mat y Met
- Datos de **un (1)** sujeto de la BD ARCHI. Se calcula la tractografía determinística del cerebro completo usando Desikan-Killiany con 34 regiones por hemisferio.
- Se trabaja con cada hemisferio por separado. Se obtiene una matriz con la distancia entre las regiones (usa grafo de afinidad) y se aplica clustering jerárquico al dendograma.
- Dependiendo de las distancias máximas entre las regiones se generan las diferentes escalas de parcelación.
- Con esto se calcula el conectoma para cada nivel.
- Proceso altamente intensivo en recursos. Solo debe hacerse una vez para obtener todas las parcelaciones.

# Conclusión
- Si bien se aplicó a un sujeto, es escalable. Se puede llevar a parcelación simétrica (***no sé qué es eso***).
- En el futuro se añadirá más información apuntando a generar simulaciones.
- Se pueden obtener tantas parcelas como se deseen dependiendo de la cantidad disponible en la parcelación base.





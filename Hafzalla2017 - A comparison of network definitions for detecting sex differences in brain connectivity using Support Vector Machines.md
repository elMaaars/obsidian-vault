#sex

# Intro
- El método más apropiado depende del protocolo, algoritmo de tractografía, etc.
- Investigan impacto de elecciones en el analisis de redes cerebrales estructurales en clasificación de género.

# Mat y Met
- T1w y HARDI de 410 sujetos. Todos cerca de los 20 años.
- Distinguen entre dos formas de segmentar:
	- Atlas based: Usan DK.
	- Cluster based: Usan 10 resoluciones, de 100 a 1000 clusters.
- Para la parte del conectoma distinguen entre dos definiciones de definición de conectividad:
	- Multiregion: Una conexión se cuenta si la fibra toca cualquier otra región.
	- Two-region: Solo se considera el incio y el fin.
- Usan un SVM para clasificar:
	- Kernel lineal.
	- Features son el número de conexiones únicas para un set de nodos (matriz de conectividad?)
#ReinforcementLearning #Poker

# Abstract
- No hay política optima para juegos multijugador (aplica al poker).
- Se propone una politica adaptativa. Usan modelado de oponente con Deep Learning y también un algoritmo de RL basado en Actor-Critic.

# Intro
- El ambiente del poker multiplayer es complejo pues hay mucha información incompleta.
- Los desafíos son analizar a los oponentes y ajustar la política dinámicamente de acuerdo a los estilos de los oponentes.
- Desarrollan una biblioteca y data set para póker multiplayer, un modelo de Deep Learning y uno de RL. Estos "analizan" y predicen el "estilo" de los oponentes, adaptando sus decisiones.

# Related work - RL in poker
- Ramirez 2019 usa la "fuerza" de la mano de poker para el modelo de RL.
- Otros trabajos se enfocan más en Deep Learning u otros tipos de poker.
- También se ha trabajado con oponentes predefinidos.

# Mat y Met
- Caracterizan a los "jugadores" (agentes). Utilizan 3 métodos, uno puntúa la calidad de la mano, otro evalúa cuantitativamente la mano, el último usa las reglas del poker y la mesa para evaluar. Se agregan también probabilidades al azar pre y post flop.
- Las 3 "acciones" identificadas son:
	- Fold: retirarse.
	- Call: igualar o pasar.
	- Bet: aumentar.
- Con esto llegan a 64 "estilos" (no lo termino de entender. Son 3 evaluaciones cuantitativas + 7 probabilidades pre y post flop = 3x15 + 7x7 = 64).
- Computan 4 features:
	- VPIP: $\frac{ManosJugadasPreFlop}{ManosJugadasTotales}\cdot100$
	- PFR: $\frac{SubidasPreFlop}{ManosJugadasTotales}\cdot 100$
	- AFQ: $\frac{Subidas}{Subidas + Bajadas + Igualadas}\cdot 100$
	- WTSD: $\frac{JugadasHastaShowdown}{JugadasHastaFlop}\cdot 100$
- Las primeras dos son preflop, las otras son postflop.
- 
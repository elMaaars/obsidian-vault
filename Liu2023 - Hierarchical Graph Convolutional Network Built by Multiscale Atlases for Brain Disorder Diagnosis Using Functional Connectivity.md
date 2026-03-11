
# Abstract
- Conectividad funcional en el SOTA usa una sola parcelación. Esto es problema pues se ignoran interacciones funcionales en diferentes escalas espaciales.
- Usan atlases multiescala para computar la FCN.
- 1792 sujetos utilizados. Se utilizan para Alzheimer, deterioro cognitivo leve y autismo. (Accuracy de 88.9, 78.6 y 72.7 para cada uno)
- **Importancia**: Merece la pena explorar la jerarquía de las interacciones funcionales en multiescala para entender mejor patologías.

# Intro
- " *It has been found that healthy brain connectomes at different scales exhibit different topological attributes, such as degree distribution, centrality and small-worldness*"
- Graph neural networks (GCN) pueden integrar características nodales junto a la topología aprendiendo y generando una representación completa de la FCN.
- 
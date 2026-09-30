## Mini-TP 2 — Metadatos del modelo con GraphQL

Notebook: [`mini-tp2/mini_tp2.ipynb`](mini-tp2/mini_tp2.ipynb)

Expuse los metadatos de mi modelo (clasificador de tumores cerebrales en MRI, `tensorflow-keras` con
backbone EfficientNetB0; métricas AUC, accuracy y F1) con GraphQL (Strawberry + FastAPI) y los
comparé contra un endpoint REST que sirve el mismo modelo.

| vista | GraphQL | REST |
|---|---|---|
| nombre + versión + AUC | 1 llamada, 87 B | 1 llamada, 454 B (5.2x más) |
| + linaje | 1 llamada | 2 llamadas |

**Qué noté:** REST devuelve el recurso completo aunque sólo necesite tres campos (sobre-fetch), y
cada relación nueva, como el linaje, es otro endpoint y otra llamada. GraphQL trae exactamente lo
que pide la query en un solo viaje. A cambio, hay que definir y mantener un esquema, y el
cacheo HTTP es más difícil, porque todo va por `POST /graphql`.

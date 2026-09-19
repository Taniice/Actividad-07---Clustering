### A. Clustering con dataset Iris

Se utilizó el dataset **Iris**, compuesto por 150 muestras y 4 características. Los datos fueron estandarizados y se entrenaron tres modelos de clustering:

| Modelo                  | Hiperparámetros principales                                                       |
| ----------------------- | --------------------------------------------------------------------------------- |
| **K-Means**             | `n_clusters=3`, `n_init=10`, `random_state=42`                                    |
| **DBSCAN**              | `eps=0.7`, `min_samples=5`                                                        |
| **Spectral Clustering** | `n_clusters=3`, `affinity=nearest_neighbors`, `n_neighbors=10`, `random_state=42` |
<img width="1789" height="495" alt="image" src="https://github.com/user-attachments/assets/c2cbc9d8-5f7c-41aa-941f-007dff7120b5" />

**Resultados:**

| Modelo              |    ARI |    NMI | Homogeneidad | Silhouette | Davies-Bouldin | Calinski-Harabasz |
| ------------------- | -----: | -----: | -----------: | ---------: | -------------: | ----------------: |
| K-Means             | 0.6201 | 0.6595 |       0.6591 |     0.4599 |         0.8336 |          241.9044 |
| DBSCAN              | 0.5401 | 0.6712 |       0.5735 |     0.6018 |         0.5568 |          281.7393 |
| Spectral Clustering | 0.6465 | 0.6838 |       0.6737 |     0.4593 |         0.8224 |          229.6799 |

**Análisis:** Spectral Clustering obtuvo los mejores resultados en las métricas de validación externa, mostrando mayor correspondencia con las especies reales. DBSCAN presentó mejores métricas internas, aunque identificó **2 clusters y 6 puntos como ruido**. K-Means formó 3 clusters sin puntos de ruido.

### B. Clustering con dataset sintético Moons

Se generó un dataset de **500 muestras** con `make_moons`, `noise=0.08` y `random_state=42`. Se entrenaron tres modelos de clustering:

| Modelo                  | Hiperparámetros principales                                                       |
| ----------------------- | --------------------------------------------------------------------------------- |
| **K-Means**             | `n_clusters=2`, `n_init=10`, `random_state=42`                                    |
| **DBSCAN**              | `eps=0.25`, `min_samples=5`                                                       |
| **Spectral Clustering** | `n_clusters=2`, `affinity=nearest_neighbors`, `n_neighbors=10`, `random_state=42` |
<img width="1784" height="492" alt="image" src="https://github.com/user-attachments/assets/39397cb4-8bec-4ca8-b9af-b85099caeea4" />

**Resultados:**

| Modelo              |    ARI |    NMI | Homogeneidad | Silhouette | Davies-Bouldin | Calinski-Harabasz |
| ------------------- | -----: | -----: | -----------: | ---------: | -------------: | ----------------: |
| K-Means             | 0.4451 | 0.3515 |       0.3515 |     0.4932 |         0.8132 |          690.2079 |
| DBSCAN              | 1.0000 | 1.0000 |       1.0000 |     0.3836 |         1.0241 |          430.8867 |
| Spectral Clustering | 1.0000 | 1.0000 |       1.0000 |     0.3836 |         1.0241 |          430.8867 |

**Análisis:** K-Means presentó dificultades para identificar correctamente la estructura curva de las dos medias lunas, obteniendo menores valores en las métricas externas. DBSCAN y Spectral Clustering identificaron correctamente los dos grupos, obteniendo **ARI, NMI y homogeneidad de 1.0**. Las métricas internas favorecieron a K-Means, demostrando que las métricas internas y externas pueden producir evaluaciones diferentes dependiendo de la estructura de los datos.


### C. Clustering con dataset sintético Circle

Se generó un dataset de **1000 muestras** con `make_circles`, `noise=0.05`, `factor=0.5` y `random_state=42`. Se entrenaron tres modelos de clustering:

| Modelo                  | Hiperparámetros principales                                                       |
| ----------------------- | --------------------------------------------------------------------------------- |
| **K-Means**             | `n_clusters=2`, `n_init=10`, `random_state=42`                                    |
| **DBSCAN**              | `eps=0.15`, `min_samples=5`                                                       |
| **Spectral Clustering** | `n_clusters=2`, `affinity=nearest_neighbors`, `n_neighbors=10`, `random_state=42` |
<img width="1784" height="492" alt="image" src="https://github.com/user-attachments/assets/5cd47ac3-7a58-4416-9003-34fae6afc180" />

**Resultados:**

| Modelo              |     ARI |    NMI | Homogeneidad | Silhouette |
| ------------------- | ------: | -----: | -----------: | ---------: |
| K-Means             | -0.0010 | 0.0000 |       0.0000 |     0.3541 |
| DBSCAN              |  1.0000 | 1.0000 |       1.0000 |     0.1125 |
| Spectral Clustering |  1.0000 | 1.0000 |       1.0000 |     0.1125 |

**Análisis:** K-Means presentó dificultades para identificar los círculos concéntricos debido a la estructura no lineal del dataset. DBSCAN y Spectral Clustering identificaron correctamente los dos grupos, obteniendo **ARI, NMI y homogeneidad de 1.0**.

### D.	Determine qué modelo o modelos son de naturaleza lineal y no lineal, así como los hiper parámetros críticos para el entrenamiento exitoso
| Modelo | Naturaleza | Justificación | Hiperparámetros críticos |
|---|---|---|---|
| **K-Means** | Lineal / basado en distancia | Forma clusters alrededor de centroides y funciona mejor con grupos aproximadamente convexos. | `n_clusters`, `n_init`, `random_state` |
| **DBSCAN** | No lineal | Agrupa según densidad y puede detectar clusters con formas arbitrarias. | `eps`, `min_samples` |
| **Spectral Clustering** | No lineal | Utiliza relaciones de vecindad y grafos para detectar estructuras complejas y no convexas. | `n_clusters`, `affinity`, `n_neighbors`, `random_state` |

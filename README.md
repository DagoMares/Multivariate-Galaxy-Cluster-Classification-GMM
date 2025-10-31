# Optimized-RedSequence-Statistical-Clustering-R
## Algoritmo de Clasificación Estadística para la Determinación de Cúmulos de Galaxias (Galaxy Clusters) 🌌

Este repositorio contiene el código fuente en **R** para la aplicación de una técnica de clasificación estadística avanzada. El proyecto aborda el desafío de la **determinación robusta de miembros** en cúmulos de galaxias, un paso crucial en la cosmología observacional para el estudio de la evolución galáctica.

El algoritmo desarrollado refina el método clásico de la Secuencia Roja (**Red-Sequence Technique**) mediante la incorporación de modelos estadísticos multivariados, garantizando una alta pureza en la lista final de miembros del cúmulo y minimizando la contaminación de galaxias de fondo o primer plano.

***

### 1. Visión General y Relevancia Científica

La Secuencia Roja es un patrón observado en galaxias que indica que los miembros de un cúmulo comparten un origen evolutivo y están ubicados en un rango de *redshift* similar. Nuestro proyecto transforma esta observación cualitativa en un método cuantitativo y robusto:

1.  **Modelo Multidimensional:** Las galaxias se analizan en un espacio tridimensional definido por sus parámetros observacionales clave:
    * **Magnitud r:** Brillo o luminosidad en una banda específica.
    * **Índice de Color ($g-r$):** Indicador de la edad estelar o la presencia de polvo.
    * **Redshift (z):** Distancia o velocidad de recesión de la galaxia.
2.  **Optimización:** La clasificación no se basa en cortes rígidos (color cuts), sino en la **distribución probabilística** de las galaxias.

***

### 2. Metodología Analítica

El corazón del algoritmo reside en la integración secuencial de dos poderosas técnicas estadísticas para la clasificación de datos.

#### 2.1. Gaussian Mixture Models (GMM)
* Se utiliza el modelo **Gaussian Mixture Models (GMM)** para modelar la distribución de las galaxias en el espacio 3D, identificando las componentes que mejor se ajustan a la muestra. Cada componente GMM representa un posible cúmulo o población.
* El modelo es particularmente útil para datos donde las clases no son linealmente separables.

#### 2.2. Filtro de Distancia de Mahalanobis
* Tras la clasificación inicial por GMM, se aplica un filtro de robustez utilizando la **Distancia de Mahalanobis** en cada cúmulo identificado.
* Esta distancia mide qué tan lejos se encuentra una galaxia del centroide de su cúmulo, considerando la forma y orientación de la dispersión de datos (**matriz de covarianza**).
* Se establece un nivel de confianza ($\alpha$, típicamente 0.05) para determinar un umbral de $\chi^2$. Las galaxias cuya distancia de Mahalanobis exceda este umbral son rechazadas como posibles contaminantes o no-miembros.

#### 2.3. Criterio de Secuencia Roja (Red Sequence Cut)
* El código incluye un paso de refinamiento que ajusta un corte de color a lo largo de la Secuencia Roja, utilizando los valores medios y los vectores propios de la matriz de covarianza del cúmulo filtrado.

***

### 3. Implementación y Tecnologías

| Recurso | Descripción |
| :--- | :--- |
| **`GlxyCluster.R`** | Función principal en R que implementa el flujo de trabajo GMM y el filtrado por Mahalanobis. |
| **Lenguaje** | **R** (usado por su robustez en estadística y análisis exploratorio de datos). |
| **Librería Clave** | **`mclust`**: Utilizada para la estimación de los parámetros de las mezclas gaussianas. |

***

### 4. Robustez y Resultados

La técnica optimizada fue sometida a rigurosas pruebas de validación (descritas en el artículo adjunto), demostrando:

* **Alta Pureza:** La tasa de galaxias de campo/fondo contaminantes en los cúmulos finales se reduce drásticamente en comparación con métodos que solo usan cortes de color.
* **Eficiencia:** El algoritmo es eficiente para procesar grandes volúmenes de datos provenientes de encuestas astronómicas como el *Sloan Digital Sky Survey (SDSS)*, facilitando el análisis de grandes bases de datos cosmológicos.

![](https://github.com/DagoMares/Multivariate-Galaxy-Cluster-Classification-GMM/blob/main/J0041_918.png)

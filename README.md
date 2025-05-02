
# Informe Comparativo de Modelos de Clasificación

## 1. Resumen del problema

La correcta clasificación de los solicitantes de crédito es fundamental para mitigar el riesgo financiero en instituciones bancarias. Este estudio utiliza un dataset con 1000 observaciones para identificar si un cliente es **bueno (clase 1)** o **malo (clase 2)** a partir de variables demográficas y financieras. El propósito es comparar el desempeño de tres algoritmos de clasificación: Regresión Logística, Support Vector Machine (SVM) y Árbol de Decisión, priorizando la identificación correcta de los buenos clientes.

## 2. Metodología
### 2.1 Descripción de la base de datos
Se utilizó un conjunto de datos Statlog (German Credit Data). El dataset incluye 1.000 observaciones y 20 variables predictoras, tanto cualitativas como cuantitativas, relacionadas con historial crediticio, ingresos, empleo, edad, duración del préstamo, entre otras. La variable objetivo distingue entre buenos (1) y malos (2) pagadores. Dado el costo diferencial de los errores, se dio especial importancia a la correcta identificación de los buenos clientes (clase 1), buscando minimizar falsos positivos en este grupo.


### 2.1 Análisis exploratorio de datos (EDA)

Se inició con una descripción general del conjunto de datos y sus variables. Se identificaron 13 variables cualitativas y 8 cuantitativas. Se visualizó la distribución y presencia de valores atípicos mediante:

- **Gráficos de cajas (boxplots)** para variables como `Attribute2`, `Attribute5` y `Attribute13`.
- **Histogramas con KDE** para analizar la forma de la distribución.
- **Matriz de correlación** para examinar relaciones entre variables numéricas.

### 2.2 Preprocesamiento

- **Tratamiento de outliers**: Las variables `Attribute2`, `Attribute5` y `Attribute13` fueron transformadas en variables ordinales categóricas con 5 rangos.
- **Codificación de variables cualitativas**: Se usó `OrdinalEncoder` para convertir variables categóricas en numéricas.
- **Estandarización**: Se aplicó `StandardScaler` a las variables numéricas para mejorar el desempeño de los modelos.
- **Renombramiento de variables**: Todas las columnas se renombraron para mejorar su interpretabilidad.
- **División de datos**: Se separó en entrenamiento (80%) y prueba (20%) con estratificación.

### 2.3 Entrenamiento de modelos

Se implementaron tres modelos:

- **Regresión Logística**
- **SVM con ajuste de hiperparámetros**
- **Árbol de Decisión con búsqueda de `max_depth`, `criterion` y `min_samples_split`**

Cada modelo fue evaluado con métricas estándar y validación cruzada de 10 particiones.

## 3. Resultados

### 3.1 Evaluación en conjunto de prueba

| Modelo                | Matriz de Confusión       | Precisión (clase 1) | Recall (clase 1) | F1-Score (clase 1) | Accuracy |
|-----------------------|---------------------------|----------------------|------------------|--------------------|----------|
| **Regresión Logística** | `[[126, 15], [28, 31]]`   | 0.82                 | 0.89             | 0.85               | 0.79     |
| **SVM**               | `[[123, 18], [28, 31]]`   | 0.81                 | 0.87             | 0.84               | 0.77     |
| **Árbol de Decisión** | `[[129, 12], [44, 15]]`   | 0.75                 | 0.91             | 0.82               | 0.72     |

### 3.2 Validación cruzada (10-fold)

| Modelo                | Recall Promedio | Desviación Estándar |
|-----------------------|------------------|----------------------|
| Regresión Logística   | 0.881            | 0.032                |
| SVM                   | 0.901            | 0.026                |
| Árbol de Decisión     | 0.873            | 0.060                |

## 4. Conclusiones

Los resultados muestran que el modelo **SVM** es el más robusto y consistente, alcanzando el mejor *recall promedio* (0.901) con baja variabilidad, lo que lo convierte en una opción favorable para la identificación de buenos clientes. La **regresión logística** también demostró buen desempeño, con métricas similares y menor varianza. Por otro lado, aunque el **árbol de decisión** ofreció un alto recall en el conjunto de prueba, su comportamiento fue menos estable, reflejando mayor desviación en la validación cruzada.

En entornos donde el objetivo es minimizar el rechazo de buenos solicitantes, SVM se posiciona como la mejor alternativa, seguido por la regresión logística. El árbol de decisión puede ser útil en contextos donde la interpretabilidad sea crítica, pero con precaución ante su sensibilidad.

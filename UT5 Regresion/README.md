# Trabajo UT5 - Regresión

Este proyecto es un análisis completo de modelos de regresión aplicados a datasets reales.

## Contenido del Notebook

- Este notebook está compartido en Google Colab mediante [este enlace](https://colab.research.google.com/drive/1EoiAKYOz3lxR4b_daBpYQqNHKzuobylq?usp=sharing)

- `UT5_REGRESION_Borja_Ramos.ipynb` incluye:

### 1. **Preprocesado de Datos**
- Importación del dataset
- Manejo de valores missing
- Codificación de variables categóricas
- Separación de datos en conjuntos de entrenamiento y test
- Estandarización/normalización de características

### 2. **Análisis Exploratorio de Datos (EDA)**

#### 🧩 Bloque 1 – Distribución del Precio + Log
- **Histograma original vs log-transformado**: El precio presenta asimetría positiva con cola larga a la derecha (muchas viviendas normales, pocas muy caras).
- **Transformación logarítmica**: Reduce significativamente la skewness (de ~0.87 a ~0.18), facilitando un mejor ajuste del modelo.
- **Conclusión**: La transformación logarítmica es fundamental para que los modelos de regresión no se sesguen por valores extremos.

#### 🧩 Bloque 2 – Matriz de Correlación (Heatmap)
- **Variables económicas**: Inmigración e hipotecas muestran correlación positiva con el precio → mayor actividad económica presiona precios al alza.
- **Materiales de construcción**: Acero, cemento, cobre y energía correlacionan positivamente → el coste de construcción se refleja en el precio final.
- **Demografía**: Edad media correlaciona negativamente → zonas envejecidas con menor presión sobre precios.
- **Conclusión**: El precio depende de múltiples factores (económicos, demográficos, materiales), justificando regresión multivariable.

#### 🧩 Bloque 3 – Barras de Correlación con el Target
- Identifica las variables más correlacionadas con el precio.
- Inmigración e hipotecas lidera correlaciones positivas; edad media destaca en negativas.
- Prepara el terreno para entender qué características peso más en las predicciones.

#### 🧩 Bloque 4 – Pairplot
- **Diagonal**: Distribuciones individuales de variables (asimetría, valores extremos).
- **Fuera diagonal**: Relaciones entre pares de variables.
- **Hallazgo clave**: Las relaciones existen pero no son puramente lineales (ej. inmigración vs precio es dispersa, año vs precio muestra ciclos no lineales).
- **Conclusión**: Justifica el uso de modelos complejos (polinomial, árboles, random forest) más allá de regresión lineal simple.

#### 🧩 Bloque 5 – Evolución Temporal del Precio
- Línea de precio medio por año muestra ciclo inmobiliario real: subida (2000-2007), crisis (2008-2009), recuperación posterior.
- Demuestra que el modelo captura tendencias reales, no ruido.
- Eleva el análisis a nivel económico.

#### 🧩 Bloque 6 – Precio por Comunidad
- Grandes diferencias regionales: España no es un mercado homogéneo.
- Justifica la inclusión de comunidad como variable categórica con One-Hot Encoding.
- EDA informando directamente el preprocesado.

### 3. **Modelos de Regresión Aplicados**
- Regresión Lineal / Regresión Lineal Múltiple
- Regresión Polinomial
- Máquinas de Soporte Vectorial (SVM)
- Árboles de Decisión
- Bosques Aleatorios

### 4. **Evaluación y Comparación**
- Análisis de residuos
- Detección de overfitting
- Cálculo de métricas: MSE, MAE, R², R² ajustada
- Ensemble prediction (promedio de predicciones)

## Datasets

- `data/Maths.csv` - Datos de matemáticas
- `data/Portuguese.csv` - Datos de portugués
- `data2/` - Datos adicionales de minería de datos

## Fuente de Datos

El dataset principal utilizado en este proyecto proviene de:
- [Datos Precios Viviendas y más - España](https://www.kaggle.com/datasets/dan0li/datos-precios-viviendas-y-mas-espaa)

## Objetivo

Comparar el rendimiento de diferentes algoritmos de regresión y seleccionar el mejor modelo basado en métricas de error y bondad de ajuste.

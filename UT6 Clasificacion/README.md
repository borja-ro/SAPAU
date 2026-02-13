# Trabajo UT6 - Clasificación

Este proyecto es un análisis completo de modelos de clasificación binaria aplicados al dataset de diagnóstico de cáncer de mama.
***Por Borja R.O., Curso especialización IA & Big Data***

## Introducción

## Contenido del Notebook

El video explicativo [se puede encontrar aquí](https://gofile.me/7rLu1/t9Invn81o) 

El notebook, ejecutable en Google Colab, mediante [este enlace](https://colab.research.google.com/drive/18J4-G_rSWPHgTGh4XyY8TLhkGsdnvanM?usp=sharing) incluye:

### 1. Preprocesado de Datos

- **Importación del dataset:** `sklearn.datasets.load_breast_cancer` (569 muestras, 30 features)
- **Manejo de valores missing:** Demostración de `SimpleImputer` (el dataset no contiene missing)
- **Codificación de variables categóricas:** 
  - Label Encoding para variables categóricas binarias
  - Ordinal Encoding para variables ordinales
  - One-Hot Encoding con `get_dummies()`
  - **Evitar la trampa de las variables dummy:** Uso de `drop_first=True` para eliminar multicolinealidad perfecta
- **Separación en conjuntos train/test:** 80% entrenamiento, 20% test con estratificación
- **Estandarización de características:** Escalado a media=0, desviación=1 con `StandardScaler`

### 2. Análisis Exploratorio de Datos (EDA)

**🧩 Bloque 1 – Matriz de Correlación (Heatmap)**
- Visualización de correlaciones entre los 30 features del dataset
- Identifica features altamente correlacionadas (r > 0.9)
- Ejemplo: `mean radius`, `mean perimeter` y `mean area` miden esencialmente lo mismo (tamaño del tumor)

**🧩 Bloque 2 – Eliminación de Features Redundantes**
- Elimina columnas con correlación > 0.9 para reducir redundancia
- Reduce de 30 a 16 features sin perder información relevante
- Mejora la interpretabilidad y reduce overfitting en modelos lineales

**🧩 Bloque 3 – Pairplot**
- Diagonal: Distribuciones individuales de features
- Fuera diagonal: Relaciones entre pares de variables discriminadas por clase
- Colores: Rojo (maligno) vs Azul (benigno)

**🧩 Bloque 4 – Correlación con Variable Target**
- Identifica las variables más discriminativas para la clasificación
- Features de tamaño y textura del tumor muestran mayor correlación con el diagnóstico

**Conclusión EDA:** Los datos presentan separabilidad lineal razonable, justificando el éxito de modelos lineales en este problema.

### 3. Modelos de Clasificación Aplicados

#### 3.1 Regresión Logística
Modelo lineal que estima la probabilidad de pertenencia a una clase mediante la función sigmoide. Interpretable y eficiente.

#### 3.2 K-Vecinos Cercanos (KNN)
Algoritmo basado en instancias: clasifica según la clase mayoritaria de los k=5 vecinos más cercanos. No paramétrico.

#### 3.3 Máquinas de Soporte Vectorial (SVM)
Busca el hiperplano que maximiza el margen entre clases.
- **Kernel Lineal:** Frontera de decisión lineal
- **Kernel RBF:** Captura relaciones no lineales mediante transformación a espacio de mayor dimensión

#### 3.4 Naive Bayes (Gaussian)
Aplica el teorema de Bayes asumiendo independencia entre features. Rápido y efectivo en datos de alta dimensión.

#### 3.5 Árbol de Decisión
Divide el espacio de features mediante reglas if/else jerárquicas. Interpretable pero propenso al overfitting.

#### 3.6 Bosque Aleatorio (Random Forest)
Ensemble de múltiples árboles de decisión entrenados con subconjuntos aleatorios. Mitiga el overfitting del árbol individual.

### 4. Evaluación y Comparación

#### 4.1 Detección de Overfitting
Comparativa de accuracy en train vs test:
- **Árboles de Decisión:** Mayor diferencia (overfitting claro)
- **Modelos Lineales:** Mejor generalización
- **Random Forest:** Mitiga el overfitting respecto a árbol individual

#### 4.2 Métricas de Evaluación (en conjunto test)

| Métrica | Descripción |
|---------|-------------|
| **Accuracy** | Proporción de predicciones correctas |
| **Precision** | Entre los predichos positivos, cuántos son realmente positivos |
| **Sensitivity (Recall)** | Entre los casos reales positivos, cuántos detectamos |
| **Specificity** | Entre los casos reales negativos, cuántos detectamos correctamente |
| **AUC (Area Under Curve)** | Métrica integral de la curva ROC (0.5=aleatorio, 1=perfecto) |

#### 4.3 Matrices de Confusión Visualizadas
Desglose de predicciones correctas (TP, TN) e incorrectas (FP, FN) para cada modelo.

#### 4.4 Curvas ROC y AUC
- Gráficas que muestran el trade-off entre sensibilidad y especificidad
- Modelos: Regresión Logística y SVM obtienen las mejores curvas ROC
- Todos los modelos superan la línea aleatoria (AUC > 0.5)

#### 4.5 Validación Cruzada (5-fold)
Valida la estabilidad del modelo mediante validación cruzada en el conjunto de entrenamiento.
- Modelos con menor varianza entre folds son más fiables
- Confirma que los resultados no son producto del azar en la partición train/test

#### 4.6 Conclusiones de la Evaluación

**Mejores modelos:** 
- Regresión Logística y SVM obtienen los mejores resultados en AUC y accuracy
- El dataset es razonablemente separable de forma lineal

**Overfitting:**
- Árbol de Decisión: overfitting claro (accuracy train ~99% vs test inferior)
- Random Forest: mitiga significativamente el overfitting
- Modelos lineales: mejor generalización

**Naive Bayes:**
- Rendimiento inferior: la asunción de independencia entre features no se cumple
- El dataset contiene features altamente correlacionadas

### 5. GridSearch - Optimización Automática de Hiperparámetros

`GridSearchCV` prueba sistemáticamente todas las combinaciones de hiperparámetros definidas y selecciona la mejor mediante validación cruzada.

**Modelos optimizados:**
- **Logistic Regression:** Parámetro C (regularización) y solver
- **SVM:** C (regularización), kernel (lineal/rbf), gamma
- **Random Forest:** n_estimators (número de árboles), max_depth (profundidad máxima), criterion (gini/entropy)

**Conclusión GridSearch:** La optimización automática afina los hiperparámetros mejorando ligeramente los resultados respecto a valores por defecto.

## Dataset

**breast_cancer (Breast Cancer Wisconsin):**
- 569 muestras
- 30 características cuantitativas (mediciones de células cancerosas)
- Variable target binaria: 0=Maligno, 1=Benigno
- Fuente: `sklearn.datasets.load_breast_cancer()`
- Referencia: https://scikit-learn.org/stable/datasets/toy_dataset.html#breast-cancer-dataset

## Objetivo

Comparar el rendimiento de diferentes algoritmos de clasificación binaria y seleccionar el mejor modelo basado en:
- Accuracy, Precision, Recall, Specificity
- AUC y curvas ROC
- Robustez ante overfitting
- Validación cruzada

## Conclusiones Generales

1. **Preprocesado:** Se demostraron todas las técnicas de preprocesado (manejo de missing, codificación categórica con evitar trampa de dummies, estandarización).

2. **EDA:** Identificó features altamente correlacionadas y su relación con el target, informando decisiones de modelado.

3. **Modelos:** Se aplicaron 7 modelos de clasificación. Los modelos lineales (Regresión Logística, SVM) funcionan muy bien en este dataset de separabilidad linear.

4. **Overfitting:** El árbol de decisión es el más propenso; Random Forest lo reduce significativamente mediante ensemble.

5. **Evaluación:** Curvas ROC y validación cruzada confirman que los modelos son robustos y generalizan bien.

6. **Optimización:** GridSearch confirma y mejora ligeramente los resultados mediante búsqueda sistemática de hiperparámetros.

---

**Autor:** Borja Ramos
**Asignatura:** Sistemas de Aprendizaje Automático (SAA)  
**Unidad Temática:** UT6 - Clasificación

TRABAJO UT5
- REGRESIÓN-
Instrucciones:
- Se deberá elaborar un Colab y subir el fichero en el tiempo de entrega establecido
- El fichero deberá nombrarse UT5_nombre_apellido1_apellido2_dni.ipynb
- Se deberá argumentar cada uno de los puntos en el trabajo con una explicación clara
- Se deberá grabar un video de duración máxima de 10 minutos, realizando una breve
explicación de cómo se ha abordado cada uno de los puntos.
- El trabajo tendrá una ponderación del 70% y el video con la defensa del 30%.
Puntos del trabajo
(1 puntos) Preprocesado de los datos
- Importar dataset
- Manejar datos missing
- Manejar datos categóricos
- Evitar trampa de las variables dummy
- Separar datos en conjuntos de entrenamiento y test
- Estandarizar o normalizar los datos
(0.5 puntos) EDA básico (Colab 5.4)
- Análisis de correlaciones, pairplot, mapas de calor, etc…
- Conclusiones
(1 puntos) Aplicar algoritmos de Regresión lineal o Regresión lineal múltiple o Regresión
polinomial y generar predicciones para nuevos valores.
(1 puntos) Aplicar algoritmos de Máquinas de soporte vectorial y generar predicciones para
nuevos valores.
(1 puntos) Aplicar algoritmos de árboles de decisión y generar predicciones para nuevos
valores.
(1 puntos) Aplicar bosques aleatorios y generar predicciones para nuevos valores
(0.5 puntos) EDA básico (Colab 5.4)
- Representar el error en la predicción (y_pred - y_test), también denominado residuo
frente al valor predicho (y_pred) (Colab 5.4)
- Determinar si hay o no overfitting (error_test > error_train?)
- Normalizar la distribución aplicando el logaritmo
(1 puntos) Aplicación de métricas y comparar resultados entre algoritmos.
- Error cuadrático medio y error cuadrático absoluto
- R2 y R2 ajustada
- Generar predicciones, aplicando la media de los resultados obtenidos por varios
algoritmos. (Colab 3. Asemle Prediction)
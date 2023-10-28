# HIV_DETECTION
¿Qué pacientes con VIH tendrán un desenlace fracaso virológico en los próximos seis meses?

I. ENTENDIMIENTO DEL NEGOCIO
El virus de inmunodeficiencia humana “VIH” es una enfermedad que ataca el sistema inmunitario del cuerpo humano, permite el desarrollo de infecciones oportunistas y cánceres potencialmente mortales, cuando los niveles de linfocitos T CD4+ están por debajo de 200 por mililitro. La transmisión se da por sangre, semen, flujo vaginal, líquido preseminal y leche de lactancia. En países desarrollados transmuta en 10 años a síndrome de inmunodeficiencia adquirida (SIDA). Predecir que pacientes presentaran fracaso virológico permite a los sistemas de salud centrar esfuerzos en poblaciones con mayor riesgo de transmutación en una ventana de tiempo variable. Modelos de inteligencia artificial permiten realizar predicciones basados en datos de los usuarios por lo cual se plantea desarrollar modelos de IA para contribuir a su temprana detección.
II. PREGUNTA A RESOLVER
¿Qué pacientes con VIH tendrán un desenlace fracaso virológico en los próximos seis meses?
III. VISUALIZACION DE VARIABLES
Se seleccionaron las variables con mayor correlación en la matriz de confusión desarrollada mas adelante para graficar e identificar hipótesis que ayuden a solucionar el propósito del modelo.

• Desenlace virológico vs número fracaso

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/ab1fc71c-9225-47cb-982a-d4f6dee089d1)

Grafica 1. Desenlace virológico vs número de fracasos en el tratamiento del paciente.
Los pacientes con éxito virológico están en un rango de numero de fracasos previos desde 0 hasta 2 fracasos con una media de 1 fracaso. Los pacientes con éxito virológico han tenido un promedio de 1 fracaso virológico en su tratamiento. Mientras que los pacientes fracaso virológico han tenido un promedio de 2 fracasos virológico en todo su tratamiento. Esta tendencia se presenta indiscriminadamente del género.

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/5f336488-b086-497b-8849-5d4c7714ea89)

Grafica 2. Desenlace virológico vs número de fracasos en el tratamiento del paciente vs género.
• Desenlace virológico vs tiempo en tratamiento

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/816f4fd8-1ea5-4a84-86c8-e6a3d45d4efa)

Grafica 3. Diagrama desenlace virológico vs tiempo en tratamiento.

El promedio de tiempo que los usuarios con desenlace virológico exitoso son de 626 días. En contraparte los usuarios que tiene desenlace virológico fracaso en promedio son de 500 días. Esta medida indica que es necesario en promedio un filtro de 500 días para detectar el desenlace virológico en vez de 180 días (6 meses aproximadamente).
• Desenlace virológico vs Recuento Cd4

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/76cf32b3-e76d-4561-831c-fa289905116a)

Grafica 4. Estado final vs promedio recuento Cd4
Los pacientes con fracaso virológico exitoso tienen un promedio de recuento Cd4 de 671; los pacientes con fracaso virológico Fracaso tiene un promedio de recuento Cd4 de 483,7.

• Fracaso virológico vs edad

El promedio de los usuarios que tiene fracaso virológico exitoso es de 35 años. Mientras que los usuarios con fracaso virológico tienen una edad promedio de 33 años. Se formula como hipótesis que la edad no es de relevancia en la predicción del fracaso virológico.

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/aa036da6-3fa6-492b-b0e7-8178db16315a)

IV. EXPLORACION DE DATOS

El siguiente cogido desarrollado se encuentra en el archivo “Exploracion_limpieza_datos.ipynb ”adjunto en la carpeta.
1. Análisis descriptivo - tipo de variable
El conjunto datos está integrado por 55 variables, de las cuales 14 son de naturaleza numérica y 41 de tipo categórico. La variable objetivo se denomina “estado_final” de estructura categórica.

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/0d7592db-3410-4c21-8fbb-e7b240f60110)

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/48fa89a8-0f65-41cd-b7c8-558c70e2e7fc)

2. Exploración de datos
   
Se realiza un análisis estadístico del dataset teniendo en cuenta:
• Numero de clases por variable categóricas.

• Porcentaje perdida de datos.

• Filtrado de datos.

• Aproximación variable objetivo.

• Análisis inferencial multivariado - matriz de confusión

• Imputación de datos.

Numero de clases por variable categóricas

Las variables que están conformadas únicamente por 1 clase se eliminan del dataset al no proporcionar información, las cuales son:

• Aspergilosis

• Nocardiosis

Porcentaje perdida de datos

Se calcula el porcentaje perdida de datos seleccionando las variables a imputar o eliminar del dataset.

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/33675bbc-2bef-4f5d-95be-394c4dd56c7e)

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/ada56fab-21d0-4182-baca-30f162a8432e)

En la tabla 2 se evidencia un alto porcentaje de datos perdidos en las variables:
• Preferencia: 22.1%

• Rango_CT: 14.2%

• TG_categorico: 20.9%

• Rango_TG: 20.9%

• LDL_categorico: 43.3%

• CT_categorico: 14.2%

Estadísticamente las variables con una perdida de datos inferior al 25% es posible imputarle datos con técnicas avanzadas como generación sintética de datos sin afectar su distribución. La variable LDL_categorico obtiene un 43.3% de perdida acercándose al 50%, por lo que imputar datos generaría una desviación de los datos afectando el desempeño del modelo, se elimina del dataset.
Filtrado de datos
Las variables CT_categorico y Rango_CT presentan los mismos valores únicamente cambiando su estructura lingüística además de obtener el mismo porcentaje de perdida de datos 14.2% por lo que se elimina la variable Rango_CT al presentar un menor valor en la matriz de correlación.
Las variables TG_categorico y Rango_TG presentan los mismos valores únicamente cambiando su estructura lingüística además de obtener el mismo porcentaje de perdida de datos 20.9% por lo que se elimina la variable Rango_TG al presentar un menor valor en la matriz de correlación.
Se eliminan la variable "tiempo_de_tratamiento" la cual presenta los mismos datos que la variable "tiempo_en_tratamiento_arv".
Aproximación variable objetivo
La variable objetivo inicial sin filtros temporales (> 6 meses) cuenta con 4504 registros de Éxito (83.3%) y 902 registros de fracaso (16.7%). Se evidencia un desbalanceo de clases por lo que se implementara técnicas de balanceo sintético de datos. No se encuentra errores gramaticales como combinación de mayúsculas o minúsculas.

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/fc48a5f0-23b2-4986-8d57-cd890f1849a8)

Grafica 6. Distribución estadística para la variable Estado final.

Análisis inferencial multivariado - Matriz de correlación
Con el conjunto de datos filtrado se aplica una matriz de correlación para determinar las variables mas relevantes con la variable objetivo “estado final”. El conjunto de datos se encuentran variables categorías y numéricas; se empleó la librería Nominal-dython que permite encontrar la correlación entre variables tipo numéricas y/o categóricas. Los valores inferiores a ±0.00 o ±0.09 representan una correlación nula por lo que se descartan del conjunto de datos a implementar en el modelo de inteligencia artificial.

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/f946e9a4-37e0-469f-830a-6d1fb7a4520f)

Grafica 7. Matriz de correlación.

Centrándose en la variable objetivo se simplifican los resultados en la siguiente tabla:

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/e7c40b3a-2184-49e8-8ea9-fa049e07152e)

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/13b63598-c3be-47af-9839-14c9c0f399f1)

Las variables seleccionadas para conformar el dataset para el entrenamiento y prueba del modelo de IA se resaltaron en amarrillo por tener un nivel de correlación con la variable objetivo, las demás se eliminan. Se elimina la variable "Fecha de inicio arv" al no representa un valor alto de correlación y no presenta una ventana de tiempo variable.
Imputación de datos
A las variables de la matriz de confusión seleccionadas y que presentan perdida de datos se realizara procesos de imputación de datos que no desequilibren las medidas de tendencia central en cada variable. A variables categóricas se aplicará la moda en los datos faltantes y en variables numéricas se reemplazarán por la media aritmética.

• Esquema ARV: La variable tiene una perdida 0.2% de los datos, se calcula la moda contando los elementos en cada clase. La mayor clase es de "Abacavir/Lamivudina+Efavirenz" con 12988 filas. Se reemplaza los valores NaN con la clase de mayor frecuencia.
• Recuento_Cd4: La variable tiene una perdida 6.8% de los datos, se calcula la media para reemplazar los valores vacíos.

• CT_categorico: La variable tiene una perdida 14.2% de los datos, se calcula la moda contando los elementos en cada clase. Se reemplaza los valores NaN con la clase de mayor frecuencia.

• TG_categorico: La variable tiene una perdida 20.9% de los datos, se calcula la moda contando los elementos en cada clase. Se reemplaza los valores NaN con la clase de mayor frecuencia.

• HDL_categorico: La variable tiene una perdida 16.6% de los datos, se calcula la moda contando los elementos en cada clase. Se reemplaza los valores NaN con la clase de mayor frecuencia.
Generación variable objetivo
La IPS requiere predecir con 6 meses de anticipación el desenlace "fracaso virológico" por lo cual se realiza un filtro a los datos permitiendo definir la clase objetivo como:

• Clase objetivo = “1”
Pacientes menor o igual a seis meses en tratamiento
Paciente con estado final Fracaso

• Clase no objetivo = 0
Pacientes con mayor a seis meses en tratamiento
Pacientes con estado final Exitoso
La variable objetivo genera 22 registros mientras que la variable no objetivo obtiene 4484 registros. Se presenta un claro desbalanceo de datos por lo cual se aplicarán técnicas de Underfitting y/o Overfitting.

ONE HOT ENCODING

Se requiere convertir las variables categóricas a formato binario para que los modelos de inteligencia artificial puedan emplean sus registros. Se crea por cada variable y clase una nueva columna indicando su pertenencia con un “1” y su ausencia con un “0”.

V. GENERACION DE MODELOS IA PARA LA PREDICCION DE VARIABLE FRACASO VIROLOGICO
El siguiente desarrollo se encuentra en el archivo “Modelos_IA.ipynb” adjunto en la carpeta.
Se divide el dataset en conjunto de prueba (80%) y test (20%) con una semilla aleatoria fija para poder ser reproducible los resultados. Se estandarizan las variables numéricas para no generar un sesgo en el entrenamiento. Para el correcto desarrollo de modelos de IA se requiere un conjunto de datos balanceado para evitar sesgos en la predicción del resultado. Se evidencia un marcado desbalanceo en la clase objetivo “Éxito = 0,488237905%” y “Fracaso = 99,51176209%”. Se combinan técnicas de Overfitting y Underfitting. Como primer paso se selecciona de manera aleatoria 500 registros de la clase mayoritaria “fracaso”. Empleando la librería SMOTE se generan datos sintéticos que igualen la clase mayoritaria y minoritaria.

• Antes de balanceo de datos:

Variable objetivo: 13
Variable no objetivo: 404

• Después de balanceo de datos:

Variable objetivo: 404
Variable no objetivo: 387

Random Forest
Se emplea el modelo Random Forest basada en árboles de decisión. Su principal ventaja se centra en un óptimo rendimiento de generalización para un rendimiento en entrenamiento. Se busca los mejores hiperparametros realizando un barrido en los parámetros empleando el criterio de Gini y Entropia.
• n_estimators: 150

• max_features: 5, 7, 9

• max_depth: 0, 3, 10, 20

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/8e16dc43-d3e0-47fe-89e9-3c07567e577d)

El mejor resultado se da con 5 características y 0 poda de hojas.

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/c3ba8045-4d79-4638-8b5c-7d0f89f09723)

Grafica 9. Matriz de decisión arboles de decisión.
• Accuracy entrenamiento: 1.0
• Accuracy testeo: 0.9904761904761905
• Recall: 1.0
• Precisión: 0.9
• F1 Score: 0.9473684210526316
• Roc Auc Score: 0.9947916666666667
La métrica Acurracy en entrenamiento y prueba presenta un buen desempeño acompañado de la métrica F1 score. La matriz de decisión presenta un sesgo en la predicción de la variable no objetivo con 95 casos mientras que la variable objetivo presenta 9 casos. Se da como hipótesis un desbalanceo en las clases por la no correcta generación sintética de clases en la variable minoritaria en este caso objetivo

REGRESION LINEAL

Se emplea una función que busca los mejores parámetros para una regresión lineal con los siguientes parámetros:
• solvers = ['newton-cg', 'lbfgs', 'liblinear']

• penalty = ['l2']

• c_values = [100, 10, 1.0, 0.1, 0.01]

Los resultados óptimos son: 'C': 100, 'penalty': 'l2', 'solver': 'newton-cg.

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/2d3005c7-e1c8-4c21-b64e-c8350324711e)

El modelo presenta un 57% de precisión, un recall del 89% y f1-score del 70% en la variable objetivo, son valores aceptables. La matriz de correlación presenta un sesgo a la variable no objetivo con 90 casos vs 8 casos de verdaderos positivos.

AdaBoosting

Se estructura un modelo para la sintonización de los hiperparametros:

• n_estimators: 10, 50, 100, 500

• learning_rate: 0.0001, 0.001, 0.01, 0.1, 1.0

Los hiperparametros con mejor resultado fueron learning_rate: 0.0001 y n_estimators: 10

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/2ab5f173-499e-4542-b235-c3294df6176f)

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/6f69cde2-99c3-469b-801a-f4f61347826a)

XGBoost

Para este modelo se sintoniza los hiperparametros en los siguientes intervalos

• learning_rate: 0.05, 0.10, 0.15, 0.20, 0.25, 0.30

• max_depth: 3, 4, 5, 6, 8, 10, 12, 15

• min_child_weight: 1, 3, 5, 7

• gamma: 0.0, 0.1, 0.2, 0.3, 0.4

• colsample_bytree: 0.3, 0.4, 0.5, 0.7

Los hiperparametros con mejor puntaje son: {'min_child_weight': 5, 'max_depth': 4, 'learning_rate': 0.25, 'gamma': 0.2, 'colsample_bytree': 0.7}

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/dc1dbb03-c55c-478e-88ae-12bcfc3a68d6)

![image](https://github.com/cesra147/HIV_DETECTION/assets/99692504/5e4bb703-423a-47af-aad1-c9b7af304664)

El modelo presenta un optimo desempeño en los parámetros de precisión, recall y F1-scrore. La matriz de confusión evidencia un desbalanceo de clases

VI. CONCLUSION DESARROLLO DE MODELOS

Los modelos empleados un buen desempeño en las métricas de precisión, recall y F1-score resaltando el modelo XGBoost. Por otra parte, las matrices de confusión evidencian un sesgo en la variable no objetivo “0”. Esto se debe a la incorrecta creación sintética de la variable minoritaria. Para solucionar este problema se propone adquirir mas datos de pacientes que su estado virológico sea fracaso y su tiempo de tratamiento sea menor o igual a 6 meses. Se propone aumentar el tiempo de predicción de 6 meses a 12 meses, el cual es cerca al promedio que tienen los pacientes con fracaso virológico en desarrollar su tratamiento.


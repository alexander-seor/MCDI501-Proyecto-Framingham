# Guion de presentación — Sumativa 3

Duración estimada: **9 minutos 55 segundos**.

## Diapositiva 1. Portada — 30 segundos

Buenos días. En esta presentación resumiré el proyecto desarrollado con los datos de Framingham. El objetivo fue estudiar el riesgo de enfermedad coronaria a diez años y conectar lo realizado en tres etapas: la exploración de la Sumativa 1, la validación de la Sumativa 2 y el modelamiento predictivo de la Sumativa 3.

## Diapositiva 2. Problema y datos — 50 segundos

Trabajamos con 4.238 personas y 16 variables demográficas, conductuales y clínicas. La variable objetivo fue `TenYearCHD`; la sigla CHD significa enfermedad coronaria. Esta variable indica si la persona desarrolló el evento durante diez años. El 15,20 % presentó el evento. Esto genera **desbalance de clases**, porque el grupo positivo es mucho menor.

Nuestro objetivo no fue afirmar que una variable causa la enfermedad, sino estudiar **asociaciones** y evaluar qué tan bien el modelo distingue entre personas con y sin evento.

## Diapositiva 3. Progresión S1, S2 y S3 — 1 minuto

El proyecto avanzó en tres etapas conectadas.

En la Sumativa 1 diagnosticamos la calidad de los datos, describimos las variables y encontramos las primeras asociaciones mediante estadística descriptiva e inferencial.

En la Sumativa 2 preguntamos si esas conclusiones eran estables. Para comprobarlo utilizamos **bootstrap**, pruebas de **permutación** y análisis de sensibilidad frente a valores extremos. De manera complementaria, la simulación **Monte Carlo** mostró cómo podían variar las tasas de enfermedad coronaria en cohortes hipotéticas generadas con parámetros fijos; por tanto, no correspondió a una validación externa ni a una comprobación de las asociaciones.

En concreto, S1 destacó variables como la edad y la presión sistólica; S2 comprobó la estabilidad y robustez de los resultados. En S3, esas fases orientaron la preparación y la comparación de candidatos, mientras que M3 seleccionó finalmente las variables mediante BIC.

## Diapositiva 4. Datos faltantes e imputación — 1 minuto 5 segundos

Los datos faltantes podían reducir la muestra y cambiar su composición. Glucosa fue la variable más afectada, con 9,16 % de valores ausentes.

Comparamos tres estrategias: eliminar registros incompletos, aplicar imputación simple y estimar los valores mediante **regresiones lineales múltiples**.

Elegimos la imputación por regresión porque conserva todas las observaciones y utiliza información de varias variables. Sin embargo, la figura muestra que la imputación determinista concentra los valores y que varias regresiones tuvieron una capacidad explicativa limitada. Por eso la decisión se considera razonable, pero no perfecta.

## Diapositiva 5. Tres modelos logísticos — 1 minuto 10 segundos

Construimos tres modelos.

M1 combinó seis variables destacadas en S1 y S2 e incorporó en S3 un término cuadrático para la edad. M2 aplicó selección **stepwise**, que agrega o retira variables según su significancia. M3 eliminó variables hacia atrás minimizando el **criterio de información bayesiano**, o BIC, que equilibra ajuste y complejidad.

El AUC es el área bajo la curva ROC y resume qué tan bien el modelo separa ambos grupos. M2 obtuvo el mayor AUC promedio en validación cruzada, pero M3 quedó prácticamente empatado con tres variables menos. La regla de un error estándar favoreció M3 por **parsimonia**, es decir, por obtener un resultado semejante con una estructura más simple.

El modelo final incluyó edad, cigarrillos diarios, presión sistólica, glucosa y sexo. El conjunto de prueba no participó en esta selección.

## Diapositiva 6. Desempeño del modelo M3 — 1 minuto 20 segundos

En el conjunto de prueba, M3 obtuvo un AUC de 0,7026, que corresponde a una **discriminación moderada**.

La sensibilidad fue 0,6010, por lo que detectó aproximadamente seis de cada diez casos con enfermedad coronaria. La precisión fue 0,2479: cerca de una de cada cuatro alertas correspondió realmente a un caso positivo.

En la matriz de confusión observamos 116 verdaderos positivos, 77 falsos negativos y 352 falsos positivos. La ponderación de clases buscó aumentar la detección; con el umbral 0,5 se observaron esos 352 falsos positivos. El indicador F1 resume el equilibrio entre sensibilidad y precisión.

Por esta razón, los puntajes del modelo permiten ordenar riesgo, pero no deben interpretarse como probabilidades clínicas calibradas.

## Diapositiva 7. Estabilidad mediante bootstrap — 1 minuto

Evaluamos la estabilidad del modelo mediante bootstrap. Generamos 1.000 remuestras con reemplazo del conjunto de entrenamiento y reajustamos el modelo en cada una.

Los cinco intervalos de confianza, o IC, percentil al 95 % de los **odds ratios**, también llamados razones de momios, quedaron por encima de uno y fueron próximos a los intervalos tradicionales de Wald. Esto indica que las asociaciones positivas fueron internamente estables.

Sin embargo, el bootstrap usa el mismo origen de datos y mantiene fija la imputación y la selección. Por tanto, no demuestra causalidad ni reemplaza una validación externa.

## Diapositiva 8. Diagnóstico de supuestos — 55 segundos

Los diagnósticos muestran dónde el modelo simplifica demasiado la realidad.

El factor de inflación de la varianza, o VIF, máximo fue 1,239, muy por debajo del umbral práctico de cinco. Por ello no observamos multicolinealidad preocupante.

La prueba de Box-Tidwell detectó no linealidad para la edad, con un valor p de 0,0154. También identificamos observaciones influyentes mediante distancia de Cook y residuos de Pearson.

No eliminamos automáticamente esos casos porque pueden representar personas reales. La recomendación principal es modelar la edad con una forma más flexible.

## Diapositiva 9. Impacto de la estrategia de imputación — 55 segundos

Ajustamos M3 con las tres estrategias de datos faltantes y comparamos las versiones sobre las mismas 1.117 personas completas de prueba.

Los AUC fueron 0,7073 para eliminación y 0,7059 para ambas imputaciones. Los intervalos de los coeficientes también se superpusieron. Esto indica que la conclusión general cambió poco.

La eliminación perdió 427 observaciones de entrenamiento y no entregó una ventaja clara. La comparación utiliza casos completos en prueba, por lo que no permite saber qué método imputaría mejor a una persona nueva con información faltante.

## Diapositiva 10. Conclusiones y recomendaciones — 1 minuto 10 segundos

M3 ofreció el mejor equilibrio entre desempeño y simplicidad. El modelo detectó una parte relevante de los casos, pero su discriminación fue moderada y la baja precisión produjo numerosos falsos positivos.

Las asociaciones fueron estables dentro del dataset, aunque eso no demuestra causalidad ni garantiza el mismo funcionamiento en otra población.

Antes de aplicarlo habría que validarlo en otra población, calibrar los puntajes y elegir el umbral según el costo de los errores. También conviene anidar todo el preprocesamiento, comparar imputación múltiple y modelar la edad de forma flexible.

El principal valor del trabajo es metodológico: integra exploración, validación y predicción de manera reproducible y reconoce con claridad sus límites. Muchas gracias.

## Resumen fácil para estudiar

- **S1:** entendimos los datos y encontramos asociaciones.
- **S2:** comprobamos si esas asociaciones eran estables.
- **S3:** construimos y evaluamos un modelo predictivo.
- **Resultado:** el modelo funciona mejor que el azar, pero todavía comete demasiados errores para usarlo clínicamente.
- **Conclusión técnica:** existe estabilidad interna, pero falta calibración y validación externa.

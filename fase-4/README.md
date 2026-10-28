# Fase 4 - Modelamiento predictivo integrado

## Propósito

Esta fase integra los resultados obtenidos en las Sumativas 1 y 2 para construir y evaluar modelos de regresión logística sobre el dataset Framingham. El objetivo es distinguir perfiles con y sin enfermedad coronaria a diez años, comparar alternativas para tratar los datos faltantes y evaluar la estabilidad y los supuestos del modelo seleccionado.

El análisis es observacional y corresponde a una validación interna. Por tanto, los resultados describen asociaciones y capacidad predictiva dentro del dataset estudiado, pero no establecen causalidad ni permiten utilizar el modelo directamente para decisiones clínicas.

## Contenido de la fase

- `sumativa-3/notebooks/`: notebook ejecutado con la preparación de datos, modelamiento, evaluación e interpretación.
- `sumativa-3/figuras/`: cinco visualizaciones exportadas desde el notebook.
- `sumativa-3/resultados/`: tablas CSV con métricas, coeficientes, intervalos y diagnósticos.
- `sumativa-3/informe/`: informe técnico final en PDF y su fuente LaTeX.
- `sumativa-3/presentacion/`: presentación final en PowerPoint con notas del presentador.

## Estructura

```text
fase-4/
├── sumativa-3/
│   ├── figuras/
│   │   ├── figura_1_imputacion_regresion.png
│   │   ├── figura_2_desempeno_modelos.png
│   │   ├── figura_3_bootstrap_odds_ratios.png
│   │   ├── figura_4_diagnosticos_modelo.png
│   │   └── figura_5_impacto_imputacion.png
│   ├── informe/
│   │   ├── informe_final_sumativa_3.pdf
│   │   └── latex/
│   │       └── main.tex
│   ├── notebooks/
│   │   └── sumativa_3_framingham.ipynb
│   ├── presentacion/
│   │   └── presentacion_sumativa_3.pptx
│   └── resultados/
│       ├── coeficientes_por_imputacion.csv
│       ├── desempeno_regresiones_imputacion.csv
│       ├── desempeno_tres_modelos.csv
│       ├── diagnosticos_regresiones_imputacion.csv
│       ├── impacto_estrategias_imputacion.csv
│       ├── intervalos_bootstrap_modelo_final.csv
│       ├── linealidad_logit_modelo_final.csv
│       ├── sensibilidad_observaciones_influyentes.csv
│       ├── validacion_cruzada_modelos.csv
│       └── vif_modelo_final.csv
└── README.md
```

## Preparación de los datos

La muestra contiene 4.238 observaciones y una prevalencia de enfermedad coronaria a diez años de 15,20 %. Se utilizó una partición estratificada de 70 % para entrenamiento y 30 % para prueba:

- Entrenamiento: 2.966 observaciones.
- Prueba: 1.272 observaciones.
- Semilla aleatoria: `42`.

Los imputadores, límites de winsorización entre los percentiles 1 y 99 y escaladores se ajustaron solo con el conjunto de entrenamiento. Esta separación reduce el riesgo de que información de prueba influya en la construcción del modelo.

Se compararon tres estrategias para los datos faltantes:

1. Eliminación de casos incompletos.
2. Imputación simple.
3. Imputación mediante regresiones lineales múltiples.

La imputación por regresión se utilizó como estrategia principal porque incorpora información de varias variables y conserva la muestra completa. Sin embargo, no demostró una ventaja clara sobre la imputación simple y presentó baja capacidad explicativa para algunas variables.

## Modelos comparados

Se ajustaron tres modelos de regresión logística:

1. **M1 S1/S2:** variables orientadas por los resultados anteriores y un término cuadrático para edad.
2. **M2 Stepwise:** selección bidireccional según significancia estadística.
3. **M3 BIC:** eliminación hacia atrás minimizando el criterio de información bayesiano.

M2 obtuvo la mayor área bajo la curva ROC (AUC) promedio en validación cruzada, pero M3 presentó un resultado prácticamente equivalente con tres variables menos. La regla de un error estándar favoreció M3 por su mayor parsimonia. El modelo seleccionado incluyó:

- Edad.
- Cigarrillos diarios.
- Presión arterial sistólica.
- Glucosa.
- Sexo.

El conjunto de prueba no intervino en esta selección.

## Resultados principales

### Desempeño en prueba

El modelo M3 obtuvo:

- AUC: `0,7026`.
- Exactitud: `0,6627`.
- Sensibilidad o recall: `0,6010`.
- Precisión: `0,2479`.
- F1: `0,3510`.
- Verdaderos negativos: `727`.
- Falsos positivos: `352`.
- Falsos negativos: `77`.
- Verdaderos positivos: `116`.

La sensibilidad indica que el modelo detectó cerca de seis de cada diez casos con enfermedad coronaria. La precisión muestra, en cambio, que aproximadamente una de cada cuatro alertas correspondió a un caso positivo. El AUC representa una discriminación moderada: supera el azar, pero todavía requiere calibración y validación externa antes de cualquier aplicación.

### Estabilidad mediante bootstrap

Se realizaron 1.000 remuestras bootstrap del conjunto de entrenamiento. Los cinco intervalos percentil al 95 % de los odds ratios quedaron por encima de uno y fueron próximos a los intervalos de Wald. Esto respalda la estabilidad interna de las asociaciones positivas, pero no demuestra causalidad ni garantiza el mismo comportamiento en otra población.

### Diagnóstico del modelo

- El factor de inflación de la varianza máximo fue `1,239`, sin evidencia de multicolinealidad preocupante.
- La prueba de Box–Tidwell indicó no linealidad para edad (`p = 0,0154`) y una señal limítrofe para glucosa (`p = 0,0636`).
- Se identificaron 261 observaciones sobre el umbral de Cook `4/n` y 81 residuos de Pearson con valor absoluto superior a 3.
- Los signos de los coeficientes se mantuvieron en el análisis de sensibilidad, aunque algunas magnitudes cambiaron.

Estos diagnósticos no invalidan el ejercicio, pero muestran que M3 no debe considerarse una especificación definitiva.

### Sensibilidad a la imputación

Las estrategias de eliminación, imputación simple e imputación por regresión se compararon sobre los mismos 1.117 casos completos de prueba. Las diferencias de AUC fueron pequeñas (`0,7073`, `0,7059` y `0,7059`) y los intervalos de los coeficientes se superpusieron. La conclusión general cambió poco entre estrategias, aunque la eliminación redujo el entrenamiento en 427 observaciones.

## Ejecución del notebook

Desde la raíz del repositorio:

```powershell
.venv\Scripts\Activate.ps1
jupyter lab
```

Abra `fase-4/sumativa-3/notebooks/sumativa_3_framingham.ipynb`, seleccione el kernel **Python (MCDI501-Framingham)** y ejecute **Restart Kernel and Run All Cells**.

La ejecución completa utiliza la semilla `42`, regenera las cinco figuras y actualiza los diez archivos CSV de resultados.

## Entregables

- [Notebook reproducible, ejecutado y documentado](sumativa-3/notebooks/sumativa_3_framingham.ipynb).
- Cinco figuras en formato PNG.
- Diez tablas de resultados en formato CSV.
- [Informe técnico final de ocho páginas en PDF](sumativa-3/informe/informe_final_sumativa_3.pdf).
- Fuente LaTeX del informe.
- [Presentación final en PowerPoint](sumativa-3/presentacion/presentacion_sumativa_3.pptx), con notas del presentador incorporadas.
- Video final pendiente de grabación.

## Limitaciones

- La validación es interna y no reemplaza una evaluación en otra población.
- La validación cruzada no repitió todo el preprocesamiento dentro de cada pliegue.
- El conjunto de prueba corresponde a una sola partición.
- Los puntajes del clasificador no están calibrados como probabilidades clínicas.
- La imputación por regresión es determinista y reduce la variabilidad de los valores imputados.
- La edad requiere una representación más flexible que la linealidad asumida por el modelo.

## Estado

- [x] Preparación de datos sin utilizar información del conjunto de prueba.
- [x] Comparación de tres estrategias de datos faltantes.
- [x] Comparación y selección de tres modelos logísticos.
- [x] Evaluación fuera de muestra.
- [x] Bootstrap de coeficientes e intervalos.
- [x] Diagnóstico de supuestos y observaciones influyentes.
- [x] Sensibilidad frente a la estrategia de imputación.
- [x] Cinco figuras y diez tablas de resultados exportadas.
- [x] Informe LaTeX compilado y PDF revisado.
- [x] Resultados contrastados con el notebook y las fases anteriores.
- [x] Presentación final con notas del presentador, revisada y contrastada con las cuatro fases.
- [ ] Video de exposición.

## Autor

**Alexander Sepúlveda Ormazábal**  
Magíster en Ciencia de Datos e Inteligencia Artificial - Universidad Andrés Bello

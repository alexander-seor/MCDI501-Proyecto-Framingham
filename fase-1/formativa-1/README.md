# Formativa 1 - Caracterización inicial del dataset Framingham

## Propósito

Esta actividad corresponde a la Fase 1 del proyecto de la asignatura. Su propósito es comprender el problema seleccionado, documentar el conjunto de datos, clasificar sus variables y presentar relaciones preliminares mediante estadística descriptiva e inferencia básica.

El trabajo se desarrolla de manera individual y utiliza una versión del dataset Framingham Heart Study.

## Pregunta de análisis

¿Qué diferencias demográficas, conductuales y clínicas se observan entre las personas que desarrollaron y las que no desarrollaron enfermedad coronaria durante los diez años de seguimiento?

## Contenido desarrollado

El notebook incluye:

1. Carga y revisión de la estructura del dataset.
2. Identificación de valores ausentes y filas duplicadas.
3. Diccionario y clasificación de las 16 variables.
4. Preparación de variables cuantitativas y categóricas.
5. Medidas de tendencia central, posición y dispersión.
6. Frecuencias absolutas y porcentajes para variables categóricas.
7. Histogramas, diagramas de caja y gráficos de barras.
8. Estimación de la proporción de enfermedad coronaria e intervalo de confianza de Wilson del 95 %.
9. Estimación de la presión sistólica media e intervalo de confianza t del 95 %.
10. Prueba t de Welch para comparar la presión sistólica media entre los grupos con y sin enfermedad coronaria.
11. Interpretaciones, limitaciones y conclusiones preliminares.

## Estructura de la actividad

```text
formativa-1/
├── figuras/
│   ├── chd_segun_hipertension.png
│   ├── comparacion_variables_chd.png
│   ├── distribucion_chd.png
│   └── distribuciones_cuantitativas.png
├── informe/
│   ├── informe_formativa_1.tex
│   ├── informe_formativa_1.pdf
│   └── logo_unab.png
├── notebooks/
│   └── formativa_1_framingham.ipynb
└── README.md
```

## Resultados principales

- El dataset contiene 4.238 observaciones y 16 variables.
- No se detectaron filas duplicadas.
- Siete variables presentan valores ausentes; `glucose` posee el mayor porcentaje, con 9,16 %.
- El 15,20 % de las personas desarrolló enfermedad coronaria durante el seguimiento.
- El intervalo de confianza del 95 % para esa proporción es 14,15 %-16,31 %.
- La presión sistólica media de la muestra es 132,35 mmHg.
- El intervalo de confianza del 95 % para la presión sistólica media es 131,69-133,02 mmHg.
- La presión sistólica media es 130,33 mmHg en el grupo sin enfermedad coronaria y 143,62 mmHg en el grupo que sí la desarrolló.
- La prueba t de Welch identifica evidencia estadística de una diferencia entre las medias (`p < 0,001`), con una diferencia estimada de 13,29 mmHg y un tamaño del efecto moderado (`d = 0,617`).

Estos resultados representan asociaciones observadas y no demuestran causalidad.

## Cómo reproducir el análisis

Desde la carpeta principal del repositorio:

```powershell
.venv\Scripts\Activate.ps1
jupyter lab
```

En JupyterLab se debe abrir:

```text
fase-1/formativa-1/notebooks/formativa_1_framingham.ipynb
```

Luego se selecciona el kernel **Python (MCDI501-Framingham)** y se ejecutan todas las celdas en orden mediante **Run All Cells**.

El notebook espera encontrar el dataset en:

```text
fase-1/datos/raw/framingham.csv
```

## Tratamiento de los datos

El archivo original no se modifica. Las variables se preparan en una copia denominada `df_analisis`. No se imputan datos ausentes en esta etapa; cada procedimiento utiliza los registros disponibles para las variables involucradas e informa el tamaño muestral correspondiente.

## Entregables

- [x] Notebook ejecutable y documentado.
- [x] Figuras exportadas.
- [x] Informe técnico en LaTeX.
- [x] Informe final en PDF.

## Fuentes

- [Dataset en Kaggle](https://www.kaggle.com/datasets/dileep070/heart-disease-prediction-using-logistic-regression)
- [Documentación docente del NHLBI](https://biolincc.nhlbi.nih.gov/teaching/)

## Autor

**Alexander Sepúlveda Ormazábal**

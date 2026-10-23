# MCDI501 - Estadística Computacional para la Toma de Decisiones

Repositorio personal del proyecto desarrollado para la asignatura **Estadística Computacional para la Toma de Decisiones**. El trabajo utiliza datos del Framingham Heart Study para estudiar características asociadas con el desarrollo de enfermedad coronaria durante un seguimiento de diez años.

## Pregunta general del proyecto

¿Qué diferencias demográficas, conductuales y clínicas se observan entre las personas que desarrollaron y las que no desarrollaron enfermedad coronaria durante los diez años de seguimiento?

El análisis es observacional. Sus resultados permiten describir asociaciones y patrones, pero no establecer relaciones causales.

## Dataset seleccionado

Se utiliza la versión del dataset **Framingham Heart Study** publicada por [Dileep en Kaggle](https://www.kaggle.com/datasets/dileep070/heart-disease-prediction-using-logistic-regression).

- Observaciones: 4.238 personas.
- Variables: 16.
- Variable de respuesta: `TenYearCHD`.
- Codificación de la respuesta: `0` indica que no se desarrolló enfermedad coronaria y `1` indica que sí se desarrolló durante el seguimiento.
- Contexto: salud cardiovascular.

La documentación del [NHLBI](https://biolincc.nhlbi.nih.gov/teaching/) se utiliza como referencia contextual sobre el Framingham Heart Study y sus conjuntos docentes.

## Organización del repositorio

```text
MCDI501-Framingham/
├── fase-1/
│   ├── datos/
│   │   └── raw/
│   └── formativa-1/
│       ├── figuras/
│       ├── informe/
│       ├── notebooks/
│       └── README.md
├── fase-2/
│   └── sumativa-1/
│       ├── figuras/
│       ├── informe/
│       ├── notebooks/
│       └── README.md
├── fase-3/
│   ├── ejercicios/
│   ├── sumativa-2/
│   │   ├── figuras/
│   │   ├── informes/
│   │   ├── notebooks/
│   │   └── resultados/
│   └── README.md
├── fase-4/
├── .gitignore
├── README.md
└── requirements.txt
```

- `fase-1/`: selección, comprensión y caracterización inicial del dataset.
- `fase-2/`: análisis exploratorio e inferencial de la Sumativa 1.
- `fase-3/`: validación interna mediante remuestreo, simulación y análisis de sensibilidad.
- `fase-4/`: actividades correspondientes a la cuarta fase del proyecto.
- `datos/raw/`: archivo original, conservado sin modificaciones.
- `notebooks/`: análisis reproducibles realizados en Python.
- `figuras/`: visualizaciones exportadas desde los notebooks.
- `informe/` o `informes/`: fuentes LaTeX y PDF de cada entrega.

## Avance del proyecto

### Fase 1 - Formativa 1

Selección del dataset, definición de la pregunta de análisis, revisión de variables y caracterización inicial.

### Fase 2 - Sumativa 1

Análisis descriptivo e inferencial, intervalos de confianza y pruebas de hipótesis sobre variables asociadas con enfermedad coronaria a diez años.

### Fase 3 - Sumativa 2

Validación interna de los resultados anteriores mediante:

- Bootstrap de medias con intervalos percentil y BCa.
- Prueba de permutación para la diferencia de presión sistólica según `TenYearCHD`.
- Bootstrap de cinco correlaciones.
- Simulación Monte Carlo de cohortes hipotéticas.
- Análisis de robustez frente a valores extremos.
- Preparación de resultados y recomendaciones para la Sumativa 3.

Los detalles se encuentran en [`fase-3/README.md`](fase-3/README.md).

## Estado del proyecto

- [x] Repositorio y entorno virtual configurados.
- [x] Dataset seleccionado y almacenado.
- [x] Formativa 1 desarrollada en un notebook reproducible.
- [x] Informe PDF de la Formativa 1.
- [x] Sumativa 1: análisis exploratorio e inferencial, notebook e informe PDF.
- [x] Sumativa 2: remuestreo, simulación, robustez, notebook e informe PDF.
- [ ] Fase 4 y actividades posteriores.

## Entorno de trabajo

El proyecto utiliza Python, JupyterLab y un entorno virtual local llamado `.venv`. Las dependencias se encuentran registradas en `requirements.txt`.

Desde la carpeta principal del repositorio, el entorno se crea y prepara con:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

Para registrar el entorno como kernel de Jupyter:

```powershell
python -m ipykernel install --user --name mdci501-framingham --display-name "Python (MCDI501-Framingham)"
```

Para iniciar JupyterLab:

```powershell
jupyter lab
```

Los notebooks deben ejecutarse desde la carpeta principal `C:\MCDI501-Framingham`, porque utilizan rutas relativas respecto de esa ubicación.

## Elaboración de informes

Los informes se preparan en LaTeX utilizando las plantillas oficiales de la asignatura. Para compilarlos localmente en Windows se utiliza MiKTeX junto con la extensión LaTeX Workshop de Visual Studio Code.

## Reproducibilidad

- El dataset original se conserva en `fase-1/datos/raw/`.
- Las transformaciones se realizan sobre copias en memoria y no modifican el archivo original.
- Los procedimientos, resultados e interpretaciones quedan documentados en notebooks ejecutados.
- La Sumativa 2 utiliza la semilla `42` en sus procedimientos aleatorios.
- Las dependencias de Python están declaradas en `requirements.txt`.
- Los archivos temporales, el entorno virtual y las credenciales están excluidos mediante `.gitignore`.

## Autor

**Alexander Sepúlveda Ormazábal**  
Magíster en Ciencia de Datos - Universidad Andrés Bello

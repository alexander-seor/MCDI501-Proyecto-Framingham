# Sumativa 1 - Análisis exploratorio e inferencial

## Propósito

Esta evaluación corresponde a la Fase 2 del proyecto de MCDI501. Su objetivo es ampliar la caracterización del dataset Framingham mediante análisis exploratorio, estimación de parámetros y pruebas de hipótesis vinculadas con el riesgo de enfermedad coronaria a diez años.

## Pregunta de análisis

¿Qué diferencias demográficas, conductuales y clínicas se observan entre las personas que desarrollaron y las que no desarrollaron enfermedad coronaria durante los diez años de seguimiento?

## Entregables

- Notebook ejecutable y documentado.
- Cinco figuras reproducibles.
- Informe técnico en PDF de máximo ocho páginas, sin anexos.
- Fuente LaTeX y enlace al repositorio GitHub.

## Estructura

```text
sumativa-1/
├── figuras/
├── informe/
│   ├── informe_sumativa_1.tex
│   ├── informe_sumativa_1.pdf
│   └── logo_unab.png
├── notebooks/
│   └── sumativa_1_framingham.ipynb
└── README.md
```

## Contenido estadístico

1. Preparación, tipos de variables y calidad de los datos.
2. Estadística descriptiva numérica y categórica.
3. Distribuciones, correlaciones y relaciones bivariadas.
4. Intervalos de confianza del 95 % para edad, presión sistólica y colesterol total.
5. Intervalo de Wilson para la proporción de enfermedad coronaria.
6. Prueba t de Welch para la presión sistólica según enfermedad coronaria.
7. Prueba chi-cuadrado para hipertensión previa y enfermedad coronaria.
8. Tamaños de efecto, limitaciones y próximos pasos.

## Ejecución

Desde la raíz del repositorio:

```powershell
.venv\Scripts\Activate.ps1
jupyter lab
```

Abra `fase-2/sumativa-1/notebooks/sumativa_1_framingham.ipynb`, seleccione el kernel **Python (MCDI501-Framingham)** y ejecute **Restart Kernel and Run All Cells**.

## Estado

- [x] Estructura de carpetas.
- [x] Notebook inicial de la Sumativa 1.
- [x] Plantilla LaTeX oficial.
- [x] Notebook ejecutado y auditado.
- [x] Figuras verificadas.
- [x] Informe técnico desarrollado.
- [x] PDF final revisado.

## Autor

**Alexander Sepúlveda Ormazábal**

# Fase 3 - Validación, simulación y remuestreo

## Propósito

Esta fase revisa la estabilidad de los principales resultados obtenidos en la Sumativa 1. La validación realizada es interna: se trabaja con remuestras y simulaciones construidas a partir del mismo dataset, por lo que no reemplaza una validación en otra población ni permite establecer relaciones causales.

## Contenido de la fase

- `ejercicios/`: actividades prácticas sobre simulación y comportamiento de la media muestral.
- `sumativa-2/`: notebook, figuras, resultados exportados e informe final de la segunda evaluación sumativa.

## Estructura

```text
fase-3/
├── ejercicios/
│   ├── A4_Ley_Grandes_Numeros.ipynb
│   └── media_muestral.py
├── sumativa-2/
│   ├── figuras/
│   │   ├── figura_1_bootstrap_intervalos.png
│   │   ├── figura_2_permutacion_presion_sistolica.png
│   │   ├── figura_3_estabilidad_correlaciones.png
│   │   ├── figura_4_monte_carlo_chd.png
│   │   └── figura_5_analisis_robustez.png
│   ├── informes/
│   │   ├── informe_sumativa_2.tex
│   │   ├── informe_sumativa_2.pdf
│   │   └── logo_unab.png
│   ├── notebooks/
│   │   ├── sumativa_2_framingham.ipynb
│   │   └── sumativa_2_framingham_validacion.ipynb
│   └── resultados/
│       └── resultados_validados_para_s3.csv
└── README.md
```

## Sumativa 2

### Procedimientos aplicados

1. Intervalos de confianza para las medias de edad, presión sistólica y colesterol total.
   - Intervalo clásico con distribución t.
   - Bootstrap percentil y BCa con 10.000 remuestras.
2. Prueba de permutación bilateral con 10.000 repeticiones para comparar la presión sistólica entre personas con y sin enfermedad coronaria a diez años.
3. Bootstrap pareado con 3.000 remuestras para cinco correlaciones con `TenYearCHD`.
4. Simulación Monte Carlo de 10.000 cohortes hipotéticas de 1.000 personas.
5. Análisis de sensibilidad mediante recorte, winsorización y jackknife.
6. Síntesis de resultados y recomendaciones para la siguiente etapa del proyecto.

### Resultados principales

- Los intervalos clásico, percentil y BCa entregaron límites muy similares para las tres medias analizadas.
- La presión sistólica media fue 13,29 mmHg mayor en el grupo que desarrolló enfermedad coronaria. La prueba de permutación obtuvo `p = 0,00010` y condujo a la misma decisión estadística que Welch en la Sumativa 1.
- Los intervalos bootstrap de las cinco correlaciones quedaron por encima de cero, aunque sus magnitudes fueron débiles o modestas (`r` entre 0,082 y 0,225).
- La simulación produjo una tasa media de enfermedad coronaria de 15,19 %, cercana al 15,20 % esperado a partir de sus parámetros.
- La diferencia de presión sistólica se mantuvo al limitar valores extremos: 13,29 mmHg originalmente y 12,78 mmHg después de winsorizar.
- Glucosa fue la variable más sensible a valores extremos y también presentó un menor número de observaciones completas.

Estos resultados respaldan la estabilidad interna de las conclusiones principales, pero todavía deben comprobarse fuera de muestra en la etapa predictiva.

## Ejecución del notebook

Desde la raíz del repositorio:

```powershell
.venv\Scripts\Activate.ps1
jupyter lab
```

Abra `fase-3/sumativa-2/notebooks/sumativa_2_framingham.ipynb`, seleccione el kernel **Python (MCDI501-Framingham)** y ejecute **Restart Kernel and Run All Cells**.

La ejecución completa utiliza la semilla `42`, regenera las cinco figuras y exporta `resultados_validados_para_s3.csv`.

## Entregables

- Notebook principal ejecutado y documentado.
- Copia de validación de la ejecución integral.
- Cinco figuras reproducibles en formato PNG.
- Tabla CSV con resultados preparados para la Sumativa 3.
- Informe técnico en LaTeX y PDF de siete páginas.

## Estado

- [x] Notebook ejecutado de principio a fin.
- [x] Bootstrap, permutación, correlaciones y Monte Carlo.
- [x] Análisis de robustez y preparación para la Sumativa 3.
- [x] Cinco figuras exportadas y verificadas.
- [x] Informe LaTeX compilado.
- [x] PDF final revisado.
- [x] Resultados contrastados con el dataset original.

## Autor

**Alexander Sepúlveda Ormazábal**

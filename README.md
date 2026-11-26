# Proyecto_final_antifungicos

Análisis exploratorio de los ensayos *in vitro* de actividad antifúngica y de la
caracterización DLS contenidos en `resultados actividad antifúngica.xlsx`.

## Archivos

| Archivo | Uso |
|---|---|
| `proyecto-antifungicos-para-ejecutar.ipynb` | **Versión lista para ejecutar**: código completo, sin salidas y preparada para hojas de datos adicionales. |
| `proyecto_antifungicos.ipynb` | **Guía para estudiantes**: consignas, pistas, espacio para el prompt y celdas de código vacías. |
| `proyecto_antifungicos_resuelto.ipynb` | **Versión docente**: mismas consignas + prompts de referencia + código Python. |
| `herramientas/crear_guia.py` | Regenera la guía a partir del resuelto. |
| `requirements.txt` | Versiones fijadas del entorno. |

Para regenerar la guía después de editar el resuelto:

```powershell
python herramientas/crear_guia.py proyecto_antifungicos_resuelto.ipynb proyecto_antifungicos.ipynb
```

La versión `para-ejecutar` **no está ejecutada**: las salidas están vacías. Antes de
correrla, agregar las planillas pendientes (formulaciones ≥ 8, IR) como hojas nuevas
del Excel o como archivos en la carpeta; la celda 1.1 las detecta sola y el bloque 7
carga los archivos de IR cuando existan.

## Estructura del análisis

1. **Conexión con los datos**: lectura del Excel en pandas, con verificación de
   encabezados y registro del SHA-256 del archivo original.
2. **Skills**: descarga reproducible de todas las skills de
   `K-Dense-AI/scientific-agent-skills` (commit `c21d13b…`) a `.agents/skills/`.
3. **Limpieza**: tabla *tidy* de actividad (celdas fusionadas, `NA`, ceros) y tabla
   DLS (cabecera doble, coma decimal, `±` y `ND`).
4. **Descriptiva** y **bioestadística**: `% inhibición`, supuestos, tests por familia,
   curvas 4PL con EC50 por bootstrap y sensibilidad de los ceros.
5. **Visualización**: figuras en `outputs/` y **informe** en `outputs/informe_resumen.md`.
6. **IR**: bloque preparado para las formulaciones ≥ 8; si no hay archivos, se salta.

## Advertencias

- El control de crecimiento tiene una sola medición (1.9 cm): todos los `% de
  inhibición` son condicionales a ese valor.
- Los 5 ceros son inhibición completa (dato válido); las 3 celdas `NA` son faltantes.
- T5–T8 tienen solo 2 dosis: EC50 no estimable por diseño.
- El análisis es exploratorio: los valores de *p* son descriptivos.

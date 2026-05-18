# Sprint 03 — Análisis de Comportamiento Musical por Ciudad y Día

> **TripleTen Data Science Bootcamp · Sprint 3 · Proyecto Integrador**
> Estado: ✅ Aprobado — Iteración 2

## Descripción

Proyecto de análisis exploratorio de datos aplicado a una plataforma de streaming musical. A partir de un dataset real con registros de reproducción de dos ciudades —**Springfield** y **Shelbyville**—, el objetivo es responder una pregunta de negocio concreta:

> *¿El comportamiento de escucha de los usuarios varía según la ciudad y el día de la semana?*

El proyecto recorre el ciclo completo de un análisis: inspección inicial, limpieza y preprocesamiento, análisis comparativo y conclusiones fundamentadas con datos.

---

## Etapas del Proyecto

| Etapa | Descripción | Técnicas aplicadas |
|-------|-------------|-------------------|
| 1. Inspección | Carga y revisión inicial del dataset | `pd.read_csv()`, `head()`, `info()` |
| 2. Encabezados | Normalización a snake_case y minúsculas | Bucle `for`, `lower()`, `strip()`, `rename()` |
| 3. Valores ausentes | Detección y sustitución por `'unknown'` | `isnull()`, `isna()`, `fillna()` |
| 4. Duplicados explícitos | Conteo y eliminación de filas repetidas | `duplicated()`, `drop_duplicates()` |
| 5. Duplicados implícitos | Unificación de variantes del género `hiphop` | Función `replace_wrong_values()`, `unique()` |
| 6. Análisis | Conteo de reproducciones por ciudad y día | `groupby()`, `count()`, filtros booleanos |
| 7. Función de consulta | Reproducciones por combinación ciudad-día | Función `number_tracks(day, city)` |
| 8. Conclusiones | Interpretación de patrones y hallazgos | Análisis crítico con soporte numérico |

---

## Hallazgos Principales

- **Springfield** registra un volumen de reproducción significativamente mayor: 15,740 canciones los lunes y 15,945 los viernes.
- **Shelbyville** muestra un pico atípico los miércoles (7,003 reproducciones), superando su actividad de lunes (5,614) y viernes (5,895).
- Los datos **confirman** que el comportamiento musical varía según ciudad y día, posiblemente influenciado por densidad poblacional y rutinas laborales.

---

## Funciones Desarrolladas

```python
# Filtra reproducciones por día y ciudad
def number_tracks(day, city):
    track_list = df[(df['day'] == day) & (df['city'] == city)]
    return track_list['user_id'].count()

# Reemplaza valores incorrectos por el valor correcto en una columna
def replace_wrong_values(df, column, wrong_values, correct_value):
    for wrong_value in wrong_values:
        df[column] = df[column].replace(wrong_value, correct_value)
    return df
```

---

## Stack Técnico

- **Python 3**
- **pandas**
- **Jupyter Notebook**
- Dataset: `music_project_en.csv`

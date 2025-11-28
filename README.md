# Proyecto: Predicción del resultado de un partido de fútbol (win/draw/loss)

Proyecto paso a paso para practicar un flujo completo de ML + MLOps: desde la adquisición de datos de fútbol hasta servir un modelo con FastAPI y Docker. Cada fase incluye objetivos claros y entregables para que puedas defender el proyecto en una entrevista técnica.

## Plan por fases

1. **FASE 0 — Preparación del entorno**: requirements, Dockerfile base, estructura del proyecto y cómo levantar el entorno en contenedor.
2. **FASE 1 — Selección del dataset**: comparar datasets reales de fútbol y elegir la fuente de datos.
3. **FASE 2 — EDA**: limpieza, estadísticas, visualizaciones y hallazgos en un notebook.
4. **FASE 3 — Definición del problema**: objetivo multiclase (win/draw/loss) y features iniciales.
5. **FASE 4 — Feature Engineering**: variables de contexto (local/visitante), forma reciente, goles, Elo, etc.
6. **FASE 5 — Preprocesado + Pipeline**: ColumnTransformer, escalado, one-hot, imputación y pipeline en `src/train_model.py`.
7. **FASE 6 — División Train/Test**: partición temporal y análisis de distribución de clases.
8. **FASE 7 — Entrenamiento de modelos**: Logistic Regression, Random Forest, Gradient Boosting/XGBoost, búsqueda de hiperparámetros y comparación.
9. **FASE 8 — Interpretabilidad**: SHAP/feature importance y documentación.
10. **FASE 9 — Serialización y predicción**: guardar pipeline final en `models/model.pkl` y crear `src/predict.py`.
11. **FASE 10 — API con FastAPI**: endpoint `/predict` con Pydantic, logging y respuesta con probabilidades.
12. **FASE 11 — Dockerización**: imagen de la API y ejecución con `docker run -p 8000:8000 football-ml-api`.
13. **FASE 12 — Pruebas (opcional)**: tests con pytest para funciones y API.
14. **FASE 13 — Preparación para entrevista**: discursos cortos y Q&A técnica.

## Estructura inicial

```
.
├── api/                  # Código de la API (FastAPI) – se completará en fases posteriores
├── data/                 # Datos locales (excluidos de git)
│   ├── raw/
│   └── processed/
├── logs/                 # Logs de entrenamiento/servicio (excluidos de git)
├── models/               # Modelos serializados (excluidos de git)
├── notebooks/            # Notebooks para EDA y experimentos
├── src/                  # Código de procesamiento, features y entrenamiento
├── Dockerfile            # Imagen base para desarrollo/servicio
├── requirements.txt      # Dependencias del proyecto
└── README.md
```

## Cómo levantar el entorno con Docker

1. **Construir la imagen base** (incluye dependencias de sistema para compilar librerías como `shap`):
   ```bash
   docker build -t football-ml-base .
   ```

2. **Ejecutar un contenedor interactivo montando el código local** (ideal para desarrollo):
   ```bash
   docker run --rm -it -v $(pwd):/app -p 8000:8000 football-ml-base bash
   ```
   - El directorio del proyecto se monta en `/app` dentro del contenedor.
   - Desde ahí podrás ejecutar notebooks (con puerto 8888 si usas Jupyter) o scripts de entrenamiento.

3. **Instalación manual (fuera de Docker, opcional)**:
   ```bash
   python -m venv .venv
   source .venv/bin/activate
   pip install --upgrade pip
   pip install -r requirements.txt
   ```

## Uso con VS Code + Docker (Dev Containers)

- Instala la extensión **Dev Containers** y abre la carpeta del proyecto en VS Code.
- Selecciona "Reopen in Container" y asegúrate de que el contenedor use la imagen `football-ml-base`.
- Así mantienes paridad entre tu entorno local y el entorno de despliegue, evitando problemas de dependencias.

## Próximos pasos

- **Confirmar FASE 0** y avanzar a **FASE 1** para seleccionar el dataset.
- Mantener el código formateado con **black** e importaciones ordenadas con **isort** (PEP8).
- Registrar logs en `logs/` y no versionar datos ni modelos.

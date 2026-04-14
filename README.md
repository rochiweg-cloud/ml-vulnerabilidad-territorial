# Predicción de Vulnerabilidad Territorial con Machine Learning

## Descripción del Proyecto

Este proyecto aplica técnicas de **Machine Learning supervisado** para predecir indicadores de vulnerabilidad territorial en Argentina, utilizando datos del Censo Nacional, la Encuesta Permanente de Hogares y registros de establecimientos productivos.

El modelo busca identificar patrones espaciales de vulnerabilidad sanitaria (acceso a hospitales y centros de salud) a partir de características socioeconómicas y territoriales de los radios censales.

## Técnicas Utilizadas

### Preprocesamiento
- Integración de múltiples fuentes de datos (joins espaciales y tabulares)
- Tratamiento de outliers mediante percentiles
- Reducción de dimensionalidad con **PCA** (Análisis de Componentes Principales)
- Creación de variables de interacción (aglomerado × distancia al centroide)
- Normalización y encoding de variables categóricas

### Modelos de Machine Learning
- **Random Forest** (`ranger`)
- **XGBoost** (Gradient Boosting)

### Validación y Evaluación
- Split train/test (80/20)
- **Validación cruzada** (5-fold cross-validation)
- **Tuning de hiperparámetros** mediante grid search
- Métricas: RMSE, MAE, MAPE, R²

### Interpretabilidad
- Análisis de importancia de variables (VIP)
- Visualización de residuos

## Estructura del Repositorio

```
├── README.md                    # Este archivo
├── modelo_vulnerabilidad.Rmd    # Script principal con el análisis completo
├── data/                        # Carpeta para datos (no incluidos por confidencialidad)
│   └── README.md                # Descripción de las fuentes de datos
└── outputs/                     # Resultados y modelos exportados
    ├── modelo_random_forest.rds
    └── modelo_boosting.rds
```

## Requisitos

```r
# Librerías necesarias
install.packages(c(
  "tidyverse",
  "tidymodels",
  "sf",
  "ranger",
  "xgboost",
  "vip",
  "DALEXtra"
))
```

## Resultados Principales

El modelo XGBoost mostró el mejor desempeño en la predicción del índice de vulnerabilidad (PC1), con las siguientes variables más importantes:

1. Proporción de hogares con acceso a red cloacal
2. Distancia al centroide del aglomerado
3. Acceso a agua de red
4. Proporción de hogares sin NBI

## Autora

**Rocío Wegman**  
Analista de Políticas Públicas | Especialización en Métodos Cuantitativos (IDAES-UNSAM)

- 📧 rochiweg@gmail.com
- 🔗 [LinkedIn](https://www.linkedin.com/in/rocío-wegman-806643268/)

## Contexto Académico

Trabajo final desarrollado en el marco de la **Especialización en Métodos Cuantitativos y Ciencias Sociales Computacionales** - IDAES/UNSAM (2024-2025).

---

*Este repositorio forma parte de mi portfolio de proyectos en ciencia de datos aplicada a políticas públicas.*

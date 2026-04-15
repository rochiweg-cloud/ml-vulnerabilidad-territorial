# Predicción de Accesibilidad a la Salud con Machine Learning

## Descripción del Proyecto

Este proyecto aplica técnicas de **Machine Learning supervisado** para predecir la accesibilidad geográfica a servicios de salud en aglomerados urbanos de Argentina. Utilizando datos del Censo Nacional, la Encuesta Permanente de Hogares, registros de vulnerabilidad sanitaria y establecimientos productivos, se entrenaron modelos predictivos para identificar los determinantes del tiempo de acceso a hospitales y centros de salud.

La accesibilidad se entiende como la posibilidad física de llegar a un centro de atención, medida en tiempo de traslado a pie. El objetivo es comprender cómo el territorio participa en la producción de desigualdades sanitarias e identificar patrones de exclusión estructural.

## Técnicas Utilizadas

### Preprocesamiento
- Integración de 4 fuentes de datos mediante joins espaciales y tabulares
- Filtrado de outliers extremos (percentil 99.5)
- Reducción de dimensionalidad con **PCA** para construir un índice de accesibilidad (PC1)
- Creación de variable espacial: distancia logarítmica al centroide del aglomerado
- Interacciones entre aglomerado y distancia al centroide

### Modelos de Machine Learning
- **Random Forest** (`ranger`) — *modelo con mejor desempeño*
- **XGBoost** (Gradient Boosting)

### Validación y Evaluación
- Split train/test (80/20)
- **Validación cruzada** (5-fold cross-validation)
- **Tuning de hiperparámetros** mediante grid search
- Métricas: RMSE, MAE, MAPE, R²

### Interpretabilidad
- Análisis de importancia de variables (VIP - permutation importance)
- Visualización de residuos y distribución de errores

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

### Modelo ganador: Random Forest
Random Forest mostró mejor desempeño que XGBoost, con un RMSE de ~0.75 en test (vs ~0.85 de XGBoost). La diferencia sugiere que XGBoost incurrió con mayor frecuencia en predicciones con desvíos amplios en los extremos del rango.

### Variables más importantes (Random Forest)
1. **log_distancia_centroide** — Distancia al centro del aglomerado urbano
2. **aglomerado_Gran.Buenos.Aires** — Pertenencia al GBA
3. **Interacción GBA × distancia** — Efecto combinado de localización
4. **desague_red_cloaca** — Acceso a red cloacal
5. **agua_de_red** — Acceso a agua de red

### Conclusiones
- La **centralidad geográfica** (cercanía al centro del aglomerado) es el factor más determinante de la accesibilidad a la salud
- La distribución de efectores de salud reproduce una **lógica centro-periferia**
- Las condiciones de infraestructura básica (cloacas, agua de red) funcionan como proxies del nivel de integración territorial
- Los modelos tienen limitaciones para predecir casos extremos (radios con peor accesibilidad), posiblemente por subrepresentación en el entrenamiento

## Autora

**Rocío Wegman** 

- 📧 rochiweg@gmail.com
- 🔗 [LinkedIn - Rocío Wegman](https://www.linkedin.com/in/rocío-wegman-806643268/)

## Contexto Académico

Trabajo final desarrollado en el marco de la **Especialización en Métodos Cuantitativos y Ciencias Sociales Computacionales** - IDAES/UNSAM (2024-2025).

## Referencias

- Vázquez Brust, A., Olego, T., & Rosati, G. (2018). *Construcción de un mapa de vulnerabilidad sanitaria en Argentina a partir de datos públicos*. Fundación Bunge y Born / IDAES-UNSAM.
- World Health Organization. (2017). *Health Systems Strengthening Glossary*.

---

*Este repositorio forma parte del portfolio de proyectos en ciencia de datos aplicada a políticas públicas.*


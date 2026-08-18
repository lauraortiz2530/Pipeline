# Trabajo Evaluativo 1 — Pre-procesamiento de Datos

Este repositorio contiene el desarrollo del primer trabajo evaluativo del curso: selección de un
dataset, mini-EDA, y diseño/implementación de un pipeline de pre-procesamiento con `scikit-learn`.

## Contenido

- [`Trabajo_Evaluativo_1_Preprocesamiento.ipynb`](./Trabajo_Evaluativo_1_Preprocesamiento.ipynb):
  notebook principal con todo el desarrollo (EDA + pipeline).
- [`datos.csv`](./datos.csv): dataset utilizado.
- [`requirements.txt`](./requirements.txt): dependencias necesarias para ejecutar el notebook.

## Dataset

`datos.csv` contiene información de postulantes a un proceso de colocación laboral:

| Columna      | Tipo                  | Descripción                                   |
|--------------|------------------------|------------------------------------------------|
| `name`       | Texto / identificador  | Nombre del postulante (se descarta del modelo) |
| `city`       | Categórica nominal      | Ciudad de residencia (4 categorías)           |
| `gender`     | Categórica nominal      | Género (`male` / `female`)                    |
| `profession` | Categórica ordinal      | Nivel académico (`bachelor` < `masters` < `phd`) |
| `age`        | Numérica                | Edad del postulante                           |
| `cgpa`       | Numérica                | Promedio académico                            |
| `placed`     | Binaria (target)        | 1 si fue colocado, 0 si no                    |

El dataset cumple con las condiciones pedidas en la guía: mezcla de variables numéricas y
categóricas (nominales y ordinales), baja cardinalidad en las nominales, entre 5 y 10 columnas, y
presencia real de datos faltantes.

## Resumen del pipeline

1. **Custom Transformer (`FunctionTransformer`)**: limpia texto de las columnas categóricas
   (quita espacios en blanco y normaliza a minúsculas), resolviendo inconsistencias reales
   presentes en `city`.
2. **`ColumnTransformer`** con tres ramas:
   - Numéricas (`age`, `cgpa`): imputación por mediana + `StandardScaler`.
   - Categóricas nominales (`city`, `gender`): imputación por moda + `OneHotEncoder`.
   - Categórica ordinal (`profession`): imputación por moda + `OrdinalEncoder` con orden
     `bachelor < masters < phd`.
3. Validación del pipeline entrenando un modelo de `LogisticRegression` con `train_test_split`.

## Cómo ejecutar

```bash
python -m venv venv
source venv/bin/activate   # En Windows: venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook Trabajo_Evaluativo_1_Preprocesamiento.ipynb
```

## Autor

_(agregar nombre y curso)_

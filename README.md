# Iris Classifier - MLOps Training Notebook

Notebook de entrenamiento de un clasificador sobre el dataset Iris integrado con una plataforma MLOps. Diseñado para ejecutarse automáticamente mediante un webhook de GitHub.

## Descripción

Este repositorio contiene un Jupyter Notebook (`train.ipynb`) que entrena un modelo de clasificación de flores Iris usando `scikit-learn`. El notebook se integra con una plataforma MLOps basada en Kubeflow/Papermill y MLflow, siguiendo un flujo de CI/CD automatizado.

## Flujo Automático

1. Se realiza un **push** al repositorio → se dispara un **GitHub Webhook**
2. La plataforma descarga este notebook
3. Lo ejecuta con **Papermill** inyectando parámetros de ejecución
4. Registra el modelo y métricas en **MLflow**
5. Si `accuracy >= 70%`, despliega el modelo automáticamente

## Tecnologías Utilizadas

- **Python 3.11**
- **scikit-learn** – Entrenamiento del modelo (RandomForestClassifier)
- **Papermill** – Ejecución parametrizada del notebook
- **MLflow** – Tracking de experimentos y registro de modelos
- **joblib** – Serialización del pipeline

## Modelo

- **Algoritmo:** RandomForestClassifier
- **Dataset:** Iris (150 muestras, 4 features, 3 clases)
- **Split:** 80% entrenamiento / 20% prueba
- **Preprocesamiento:** StandardScaler
- **Hiperparámetros:** `n_estimators=100`, `max_depth=5`, `random_state=42`

## Parámetros Inyectables (Papermill)

| Parámetro | Valor por defecto | Descripción |
|---|---|---|
| `MODEL_OUTPUT_PATH` | `model.joblib` | Ruta de salida del modelo |
| `PIPELINE_ID` | `local-run` | ID del pipeline |
| `MLFLOW_TRACKING_URI` | `http://mlflow:5000` | URI del servidor MLflow |
| `MLFLOW_RUN_ID` | `""` | ID del run de MLflow |

## Ejecución Local

```bash
pip install scikit-learn mlflow joblib papermill jupyter
jupyter notebook train.ipynb
```

## Autor

Juan Sebastian Pardo Anzola – [@JuanPar063](https://github.com/JuanPar063)

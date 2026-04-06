# Trabajo-de-Examen-Profesional-Leonardo-Marquez-Juarez
## Hierarchical Quant Pipeline: Predicción Direccional de Acciones

Este repositorio contiene el código fuente oficial y la infraestructura de datos para la investigación de tesis: **"Pronóstico de Movimientos de Acciones mediante un Pipeline Jerárquico de Aprendizaje Automático: Integrando Clustering, Random Forests y Clasificadores de Vectores de Soporte"** (UNAM, Facultad de Economía).

## 📌 Resumen del Proyecto

El pronóstico de series temporales financieras tradicionales (modelos monolíticos) fracasa ante la no-estacionariedad de los mercados (cambios de régimen). Este proyecto implementa una arquitectura modular de Machine Learning que imita la adaptabilidad del mercado, mitigando el "riesgo direccional" y el sobreajuste al ruido financiero.

## 🏗️ Arquitectura del Modelo (Base 4.0)

El pipeline se divide en tres etapas ejecutadas secuencialmente:

1. **Aprendizaje No Supervisado (Gaussian HMM):** Un Modelo Oculto de Markov segmenta la serie de tiempo en regímenes latentes (ej. alta volatilidad vs. tendencia estable) usando el algoritmo Baum-Welch.
2. **Selección Topológica (Random Forest):** Dentro de cada régimen aislado, un ensamble de árboles evalúa la importancia estática de las características (Feature Importance) utilizando evaluación Out-of-Bag, descartando indicadores ruidosos.
3. **Maximización del Margen Direccional (SVC):** Un Clasificador de Vectores de Soporte con kernel RBF y penalización asimétrica (`class_weight='balanced'`) toma la decisión final (Compra/Venta) mitigando la Paradoja de la Precisión.

## 📂 Estructura del Repositorio
```text
├── data/               # Datos históricos (OHLCV) extraídos vía yfinance
├── notebooks/          # Exploración de datos (EDA) y validación de regímenes
├── src/                # Código fuente del pipeline
│   ├── features.py     # Ingeniería de características (RSI, Medias Móviles)
│   └── pipeline.py     # Clase principal HierarchicalBaseModel4
└── README.md
```
## 🚀 Ejecución Interactiva

El pipeline cuantitativo completo (extracción de datos, entrenamiento del modelo HMM/SVC y backtesting financiero) está consolidado en un único cuaderno para facilitar su evaluación. 

Puedes ejecutar el código en la nube sin necesidad de instalar librerías locales haciendo clic aquí:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1kRt_9eN-Iw1ZVM7q65AxZpF_McWBxPSP)

*(Nota para el sínodo: El cuaderno está configurado en modo lectura. Al abrirlo, Colab creará una copia temporal en su entorno para que pueda ejecutar las celdas libremente).*

*(Nota para el evaluador: El código solicitará acceso a Google Drive en la primera ejecución exclusivamente para crear y almacenar en caché el archivo `.csv` con la serie de tiempo financiera, garantizando el determinismo en ejecuciones futuras).*

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

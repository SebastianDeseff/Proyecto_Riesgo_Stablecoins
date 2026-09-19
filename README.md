# 🏦 Stress Test de Contagio Financiero: Análisis de Riesgo Sistémico

**Perfil del Autor:** Sebastián E. Deseff | *Lic. en Economía (En curso)* | [Enlace a LinkedIn]

## 📌 Resumen Ejecutivo
Este proyecto desarrolla un modelo automatizado para evaluar la transmisión de shocks financieros globales hacia el costo de fondeo del sistema bancario argentino. A través de la integración de APIs públicas internacionales y locales, el modelo analiza si las fluctuaciones en la liquidez de activos digitales (*Stablecoins*) y las variaciones en las tasas libres de riesgo (Treasury 10Y) ejercen presión sobre la tasa de referencia local (BADLAR).

El objetivo es construir un marco cuantitativo aplicable a **Stress Testing** y gestión del **Riesgo Crediticio**.

## 🛠️ Stack Tecnológico
* **Lenguaje:** Python 3
* **Entorno:** Jupyter Notebook / Visual Studio Code
* **Librerías principales:** `pandas` (ETL y Feature Engineering), `scipy` (Inferencia Estadística), `matplotlib` (Visualización de datos), `requests` (API ingestion).

## 📊 Arquitectura de Datos
El pipeline de datos extrae, limpia y unifica series temporales con distintas frecuencias y calendarios de mercado, aplicando técnicas de interpolación (*forward-fill*).

1. **Rendimiento Bono Tesoro EE.UU. a 10 años (FRED API):** Variable proxy del costo de oportunidad del capital global.
2. **Liquidez Global de Stablecoins (DeFiLlama API):** Proxy de fuga/movimiento de capitales digitales de alta liquidez.
3. **Tasa BADLAR (BCRA):** Tasa pasiva de referencia para plazos fijos mayoristas; canal de transmisión directo hacia las tasas de préstamos a tasa variable y morosidad local.

## ⚙️ Metodología Analítica

* **Data Engineering:** Consolidación de fuentes asincrónicas en un *DataFrame* maestro (`dataset_estres_unificado.csv`), estandarizando feriados y fines de semana.
* **Feature Engineering:** Construcción del "Spread de Riesgo" (Diferencial entre BADLAR y US 10Y).
* **Econometría y Estadística:**
  * **Análisis de Lags (Rezagos temporales):** Evaluación de la asincronía en el contagio financiero mediante coeficientes de correlación de Pearson aplicados a variables desplazadas ($t-1$, $t-3$, $t-5$).
  * **Test de Jarque-Bera:** Análisis estructural de asimetría y curtosis sobre los shocks de tasas para evaluar la presencia de "colas pesadas", fundamentales en la estimación del Riesgo Crediticio.

## 📈 Visualizaciones Clave
* *Gráficos de Eje Dual (Twin Axes):* Evolución superpuesta de la presión de fondeo local versus la volatilidad de liquidez global.
* *Mapas de Calor:* Identificación rápida de jornadas de alto estrés financiero.
* *Ajuste Distribucional:* Histograma de frecuencia del Spread vs. Distribución Normal Teórica (Campana de Gauss).
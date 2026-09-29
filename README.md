# 💳 Predicción de Riesgo de Crédito — Clasificación de Clientes en Default

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-FF6600?style=flat-square)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat-square)
![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0?style=flat-square)

---

## 📋 Descripción del proyecto

Modelo de clasificación para predecir si un cliente incurrirá en incumplimiento de pago (default) en el siguiente mes, basándose en su historial financiero y comportamiento de pagos. El proyecto apoya la decisión de aprobación o rechazo de crédito en instituciones financieras, reduciendo pérdidas por cartera vencida sin excluir innecesariamente a buenos pagadores.

**Fuente de datos:** UCI Machine Learning Repository — Default of Credit Card Clients  
**Link:** https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients  
**Registros:** 30,000 clientes · 24 variables · Variable objetivo: `default payment next month`

---

## 🎯 Objetivo de negocio

Predecir qué clientes incurrirán en default el siguiente mes para que el equipo de riesgo crediticio pueda:
- Priorizar revisiones manuales de solicitudes de crédito
- Reducir pérdidas por cartera vencida
- Tomar decisiones de crédito más informadas y justificables

---

## 🗂️ Estructura del análisis

| Paso | Descripción |
|---|---|
| 1 | Exploración inicial — forma, tipos, nulos, duplicados, balance de clases |
| 2 | Preparación — corrección de categorías, features derivados |
| 3 | Construcción — Regresión Logística, Random Forest, XGBoost |
| 4 | Evaluación — AUC-ROC, ajuste de umbral, matriz de confusión |
| 5 | Conclusiones — decisiones técnicas, aprendizajes, próximos pasos |

---

## 🔧 Herramientas utilizadas

| Herramienta | Uso |
|---|---|
| Python | Lenguaje principal |
| Pandas / NumPy | Manipulación y limpieza de datos |
| Scikit-learn | Modelos de clasificación, métricas, división train/test |
| XGBoost | Modelo final de clasificación |
| Matplotlib / Seaborn | Visualización de resultados |

---

## 🧹 Decisiones técnicas de preparación

| Decisión | Justificación |
|---|---|
| EDUCATION (0, 5, 6) → reclasificado como 4 (Others) | Valores no documentados en el diccionario de datos |
| MARRIAGE (0) → reclasificado como 3 (Others) | Valor no documentado en el diccionario de datos |
| Feature `UTIL_RATIO` creado | Promedio de facturas / límite de crédito — captura el nivel de endeudamiento relativo |
| Feature `AVG_PAY_AMT` creado | Promedio de pagos realizados — captura el comportamiento de pago histórico |
| Columna ID eliminada | No aporta información predictiva |
| `scale_pos_weight` en XGBoost | Manejo del desbalance de clases (77.9% / 22.1%) sin alterar los datos |

---

## 📊 Comparativa de modelos

| Modelo | AUC-ROC | Recall Default | Precision Default |
|---|---|---|---|
| Regresión Logística | 0.7095 | 0.62 | 0.37 |
| Random Forest | 0.7586 | 0.33 | 0.64 |
| **XGBoost (umbral 0.5)** | **0.7775** | 0.62 | 0.47 |
| **XGBoost (umbral 0.35) ← Seleccionado** | **0.7775** | **0.82** | 0.33 |

---

## 💡 Resultado principal

**AUC-ROC: 0.7775** — el modelo tiene 77.75% de probabilidad de rankear correctamente un cliente en default sobre uno que no lo es.

**Ajuste de umbral de 0.5 → 0.35:**

| Métrica | Umbral 0.5 | Umbral 0.35 | Mejora |
|---|---|---|---|
| Recall Default | 62% | **82%** | +20 pp |
| Defaults no detectados | 509 | **234** | **−54%** |
| Buenos pagadores rechazados | 668 | 2,180 | +1,512 |

El ajuste reduce los defaults no detectados en un **54%** — la métrica más importante para una institución financiera, donde aprobar a quien no paga es más costoso que rechazar a quien sí pagaría.

---

## 🏆 Variables más predictivas (XGBoost)

1. **PAY_0** — Estado del pago más reciente ← variable más importante
2. **PAY_2 a PAY_6** — Historial de atrasos de los últimos 6 meses
3. **LIMIT_BAL** — Límite de crédito otorgado
4. **UTIL_RATIO** — Ratio de utilización del crédito (feature derivado)

El historial de atrasos domina la predicción — quien ya se atrasó tiene alta probabilidad de volver a hacerlo.

---

## 🚀 Qué mejoraría con más tiempo

1. Optimización de hiperparámetros con GridSearchCV o Optuna
2. SHAP values para explicabilidad individual por cliente
3. Incorporar variables macroeconómicas (tasa de desempleo, ciclo económico)
4. Validación cruzada estratificada k-fold para resultados más robustos

---

## 📁 Archivos del repositorio

| Archivo | Descripción |
|---|---|
| `riesgo_credito_clasificacion.ipynb` | Notebook completo del análisis |
| `README.md` | Documentación del proyecto |

---

## 🔗 Enlaces

[![Portafolio](https://img.shields.io/badge/Ver_Portafolio-0d1b2a?style=for-the-badge&logo=github&logoColor=white)](https://dataanalystwil.github.io)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/wilma-cruz-74279822)
[![Fuente de datos](https://img.shields.io/badge/UCI_Dataset-00599C?style=for-the-badge)](https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients)

---

*Proyecto de análisis de datos — Portafolio Business Analyst / Data Analyst*

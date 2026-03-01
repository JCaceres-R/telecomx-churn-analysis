# 📡 TelecomX — Análisis de Churn de Clientes

Análisis exploratorio de datos (EDA) enfocado en comprender y predecir la evasión de clientes en una empresa de telecomunicaciones. El proyecto aplica un proceso completo de **ETL** para limpiar y transformar los datos, seguido de visualizaciones estratégicas e insights accionables.

---

## 📋 Descripción del Problema

TelecomX enfrenta una alta tasa de cancelaciones y necesita entender los factores que llevan a la pérdida de clientes (**Churn**). El objetivo es identificar patrones de comportamiento a partir de datos históricos para que el equipo de Data Science pueda avanzar en modelos predictivos y diseñar estrategias de retención.

---

## 🎯 Objetivos

- Importar y manipular datos en formato JSON de manera eficiente.
- Aplicar los conceptos de **ETL** (Extracción, Transformación y Carga) en la preparación de los datos.
- Crear visualizaciones estratégicas para identificar patrones y tendencias.
- Realizar un **Análisis Exploratorio de Datos (EDA)** y generar un informe con insights relevantes.

---

## 🛠️ Tecnologías Utilizadas

| Librería | Uso |
|---|---|
| `pandas` | Manipulación y transformación de datos |
| `numpy` | Operaciones numéricas |
| `plotly.express` | Visualizaciones interactivas |
| `matplotlib` | Visualizaciones estáticas |
| `sqlalchemy` | Conexión y manejo de base de datos |

---

## 🔄 Proceso ETL

### 📌 Extracción
- Carga del dataset desde un archivo JSON con estructura anidada.
- Inspección inicial del dataframe y distribución de la variable objetivo `Churn`.

### 🔧 Transformación
- **Normalización:** Se aplicó `pd.json_normalize` para aplanar las columnas anidadas, resultando en un dataframe de 21 columnas.
- **Tipos de datos:** Conversión de columnas a `int64`, `float64` y `category` según corresponda.
- **Mapeo binario:** Variables con valores `Yes/No` fueron codificadas como `1/0` para facilitar el análisis.
- **Tratamiento de nulos:** Los valores vacíos en `account_Charges_Total` fueron imputados con `0` (usuarios sin cargos acumulados por antigüedad cero).
- **Variable objetivo:** El 3% de registros con Churn `"Unknown"` fue eliminado al no mostrar correlaciones claras con el resto de las variables.
- **Nueva variable:** Se creó `account_Charges_Daily` (cargo mensual / 30) y `internet_Service` (binaria: tiene internet o no).

### 📊 Carga y Análisis
- Estadísticas descriptivas del dataset limpio.
- Análisis univariado y bivariado de variables categóricas y numéricas.

---

## 📈 Principales Hallazgos

### Distribución General
Aproximadamente el **70%** de los usuarios permanecen en la empresa, mientras que un **~26%** son evasores confirmados.

### Variables Categóricas
- **Género:** No es un factor determinante. La tasa de churn es casi idéntica entre hombres y mujeres.
- **Tipo de Contrato (hallazgo crítico):**
  - Contrato **mes a mes**: tasa de deserción del **42.7%**.
  - Contrato **dos años**: solo **2.8%** de deserción.
- **Método de pago:** Los usuarios con **Electronic Check** presentan la mayor tasa de abandono (**45.3%**). El 78.2% de estos usuarios tienen contratos mes a mes, formando una combinación de alto riesgo.

### Variables Numéricas
- **Antigüedad (Tenure):** La mediana de abandono es de **10 meses** vs. **38 meses** de los usuarios retenidos. Los primeros 10 meses son el "período crítico".
- **Gasto Total:** Las fugas se concentran en el rango de **0 a 1,000 unidades**, indicando que los clientes se van antes de consolidarse como usuarios de alto valor.

---

## 👤 Perfil del Cliente de Alto Riesgo

1. Contrato **mes a mes**.
2. Pago mediante **Electronic Check**.
3. Antigüedad menor a **10 meses**.

---

## 💡 Recomendaciones Estratégicas

1. **Programa de Onboarding:** Atención prioritaria durante los primeros **12 meses** del cliente.
2. **Incentivos al Pago Automático:** Descuentos o beneficios para usuarios que migren de eCheck a métodos automáticos.
3. **Conversión de Contratos:** Campañas para incentivar el paso de planes mensuales a anuales o bienales.
4. **Sistema de Alertas Tempranas:** Notificaciones automáticas cuando clientes con Tenure < 10 meses reportan incidencias técnicas.

---

## 📁 Estructura del Proyecto

```
telecomx-churn-analysis/
│
├── TelecomX.ipynb        # Notebook principal con todo el análisis
├── README.md             # Documentación del proyecto
└── data/
    └── TelecomX_Data.json  # Dataset original (no incluido por privacidad)
```

---

## 🚀 Cómo Ejecutar

1. Clona el repositorio:
   ```bash
   git clone https://github.com/tu-usuario/telecomx-churn-analysis.git
   ```
2. Instala las dependencias:
   ```bash
   pip install pandas numpy plotly matplotlib sqlalchemy
   ```
3. Coloca el archivo `TelecomX_Data.json` en la carpeta `data/`.
4. Abre y ejecuta el notebook `TelecomX.ipynb`.

---

## 📌 Contexto

Proyecto desarrollado como parte del programa de formación en Data Science de **Alura Latam**.

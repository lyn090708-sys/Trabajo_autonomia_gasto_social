# Análisis de Dependencia de Transferencias y Autonomía Financiera en Gobiernos Locales del Perú

## Descripción del proyecto
Este proyecto analiza la relación entre las **fuentes de financiamiento municipal** y la **priorización del gasto social** en los gobiernos locales del Perú, utilizando datos del **Ministerio de Economía y Finanzas (MEF)** para el periodo **2014–2019**.  

El objetivo central es responder a la pregunta:  
"¿La **dependencia de transferencias fiscales** (como el FONCOMUN) reduce la asignación de recursos a educación y salud, mientras que una mayor **autonomía financiera** favorece un gasto más orientado al bienestar ciudadano?"  

---

## Fuentes de datos
Los datos provienen de las bases abiertas del MEF:

- **Presupuesto y Ejecución de Gasto – Devengado Mensual**  
  Incluye información de gasto devengado por función, nivel de gobierno y pliego.  
  [Ver dataset](https://datosabiertos.gob.pe/dataset/presupuesto-y-ejecución-de-gasto-–-devengado-mensual)

- **Transferencias intergubernamentales (Canon, Regalías, FONCOMUN, etc.)**  
  Registra montos transferidos por fuente de financiamiento a nivel municipal.  

- **Ingresos municipales (tributarios y no tributarios)**  
  Datos de recaudación de ingresos propios de los gobiernos locales.  

---

## Metodología

1. **Ingesta y limpieza de datos**  
   - Filtrado de gobiernos locales.  
   - Normalización de nombres y formatos de variables clave (año, mes, pliego, función, rubro).  

2. **Construcción de indicadores**  
   - **Dependencia de transferencias**: proporción de transferencias en los ingresos totales.  
   - **Autonomía financiera**: proporción de ingresos propios en los ingresos totales.  
   - **Gasto social**: participación de las funciones de educación y salud en el gasto devengado.  

3. **Análisis descriptivo**  
   - Estadísticas básicas (media, mediana, desviación estándar, percentiles).  
   - Comparaciones por quintiles de autonomía.  
   - Identificación de patrones, ciclos estacionales y casos atípicos.  

4. **Visualización**  
   - Series de tiempo (2014–2019) de autonomía y transferencias.  
   - Gráficos de barras y líneas comparativas.  
   - Relación entre gasto social y autonomía financiera.  

---

## Principales hallazgos

- La **autonomía financiera municipal** es muy baja: en la mayoría de meses y municipios se mantiene en valores cercanos a cero.  
- La **dependencia de transferencias** es estructural: en todos los años analizados, los montos transferidos superan ampliamente a los ingresos propios.  
- El **gasto social** en educación y salud es altamente volátil, con picos que en algunos casos coinciden con transferencias elevadas, pero que en muchos otros dependen de **decisiones políticas y coyunturales**.  
- Al segmentar por quintiles, se observa que los municipios con mayor autonomía financiera tienden a asignar **más recursos al gasto social**, lo que confirma la relación positiva entre autonomía y bienestar ciudadano.  

---

## Relevancia del estudio
Este trabajo constituye un **análisis exploratorio** de cómo se relacionan las fuentes de financiamiento municipal con la inversión social. Los resultados pueden servir como insumo para:  

- Evaluar la eficacia del sistema de transferencias fiscales. 
- Identificar municipios con **alta dependencia y baja inversión social**.  
- Proponer lineamientos de política que fortalezcan la **descentralización fiscal** y la **capacidad de gestión local**, con miras a un gasto social más eficiente y sostenible.

## Análisis de Modelos 

###  Objetivo del estudio

El objetivo principal es **evaluar empíricamente** si una mayor **autonomía financiera** —medida como la proporción de ingresos propios sobre el total— se asocia con un **mayor gasto social**, y si una alta **dependencia de transferencias** puede generar desincentivos fiscales o distorsionar la asignación de recursos hacia sectores prioritarios como educación y salud.

---

### Variables principales

| Variable | Descripción | Tipo |
|-----------|--------------|------|
| `ln_gasto_social` | Logaritmo natural del gasto social municipal. | Variable objetivo (target) |
| `autonomia` | Proporción de ingresos propios sobre el total de ingresos municipales. | Independiente |
| `autonomia2` | Término cuadrático de la autonomía (captura efectos no lineales). | Independiente |
| `prop_transferencias` | Proporción de transferencias en los ingresos totales. | Independiente / control |

Estas variables fueron derivadas a partir de datos del MEF y estandarizadas para permitir comparaciones temporales y entre gobiernos locales.

---

## Metodología y decisiones de modelado

1. **Ingesta y limpieza de datos:**  
   - Filtrado de gobiernos locales.  
   - Normalización de nombres, códigos y periodos.  
   - Construcción de indicadores de autonomía, transferencias y gasto social.  

2. **Modelado supervisado:**  
   - **Modelo 1 (OLS Simple):** relación lineal entre autonomía y gasto social.  
   - **Modelo 2 (OLS Cuadrático):** incorpora un término no lineal (autonomía²) para capturar rendimientos decrecientes.  

3. **Evaluación del desempeño:**  
   - División del conjunto en entrenamiento (75%) y prueba (25%).  
   - Validación cruzada **k-Fold (k=5)**.  
   - Métrica de comparación: **Error Cuadrático Medio (MSE)** y desviación estándar.  

4. **Interpretación de resultados:**  
   - El modelo cuadrático reduce significativamente el error medio y mejora el ajuste.  
   - Se evidencia una **relación no lineal** entre autonomía fiscal y gasto social, con rendimientos decrecientes a niveles altos de autonomía.  

---

### Resultados principales

| Modelo | MSE Promedio (CV) | Desviación Estándar |
|---------|--------------------|--------------------|
| Baseline | 4.575 | 0.000 |
| OLS Simple | 0.214 | 0.107 |
| **OLS Cuadrático** | **0.0386** | **0.0443** |

El modelo cuadrático presenta un mejor desempeño predictivo, reflejando que la relación entre autonomía fiscal y gasto social **no es lineal**, sino que existe un punto donde el efecto marginal de la autonomía comienza a disminuir.

---

## **Actualización Metodológica y Modelado Avanzado (PCA + Machine Learning + Series de Tiempo)**

Esta sección amplía el análisis del Trabajo 2 incorporando:

- Ingeniería de variables fiscales
- Análisis de Componentes Principales (PCA)
- Modelos predictivos avanzados
- Validación temporal (TimeSeriesSplit)
- Análisis de importancia de variables

---

## Limpieza y estandarización adicional 

- Eliminación de observaciones con `gasto_social = 0`  
- Eliminación de observaciones con `autonomia = 0`  
- Conversión uniforme de todas las columnas numéricas  
- Construcción del índice temporal `fecha`  
- Normalización fiscal por municipio  

---

## Construcción de indicadores (Trabajo 3)

Se añadieron variables clave:

- `autonomia2` — autonomía al cuadrado  
- `autonomia_x_transferencias` — interacción autonomía-transferencias  
- `dependencia_transferencias`  
- `canon_prop_transferencias`  
- `esfuerzo_tributario_relativo`  
- `relacion_transf_propios`  
- `prop_transferencias`  
- `prop_propios`  
- `lag1_ln_gasto` — rezago para capturar persistencia temporal

Estas variables permiten analizar efectos no lineales, dependencia estructural, capacidad tributaria y dinámica del gasto.

---

## Análisis Descriptivo Avanzado

Incluye:

- Resumen estadístico de variables fiscales  
- Matriz de correlaciones  
- Serie temporal del gasto social agregado 2014–2019  

**Hallazgo clave:** el gasto social muestra ciclos fuertes e inercia temporal, lo cual justifica el uso de rezagos en el modelado.

---

# PCA (Análisis de Componentes Principales)

### **Resultados del PCA**

- **PC1 explica ~48% de la varianza** — eje que contrapone dependencia de transferencias vs. autonomía y esfuerzo tributario.  
- **PC2 explica ~28% de la varianza** — ligado a composición del canon y estructura de financiamiento.  
- Los dos primeros componentes capturan **~76%** de la estructura fiscal.

### **Interpretación del biplot**

- Los municipios presentan estructuras fiscales heterogéneas.  
- PC1 distingue municipios autónomos de los altamente dependientes.  
- PC2 distingue según peso del canon y composición interna de ingresos.

---

# 🤖 Modelado Predictivo (Ridge, Lasso, Random Forest, XGBoost)

Se utilizó un dataset **agregado por fecha** (promedio entre municipios) para capturar la dinámica nacional mensual del gasto social.

### Validación temporal  
Se empleó **TimeSeriesSplit (5 folds)**.

---

## Resultados de modelos (Trabajo 3)

| Modelo | MSE | R² |
|--------|-----|----|
| RidgeCV | 0.327 | 0.348 |
| LassoCV | 0.324 | 0.354 |
| XGBoost | 0.368 | menor |
| **Random Forest** | **0.244** | **mejor** |

---

## Predicción vs. Real (último fold)

- La predicción del RF sigue la tendencia del gasto social.  
- El modelo suaviza picos abruptos, pero captura la dinámica temporal.  
- **MSE último fold ≈ 0.046**, **R² ≈ 0.27**.  
- El gasto social depende fuertemente del gasto del mes previo.

---

## Importancia de variables

### **Random Forest**
- `lag1_ln_gasto` — dominante (>75%)  
- `esfuerzo_tributario_relativo`  
- `dependencia_transferencias`  

### **XGBoost**
- `lag1_ln_gasto` — dominante (~54%)  
- luego: esfuerzo tributario y relación transferencias/propios  

 **Conclusión clave:**  
La dinámica temporal es el determinante principal; la estructura fiscal aporta información adicional pero menor.

---

# Conclusiones Generales

- La autonomía financiera en Perú es baja y la dependencia de transferencias es estructural.  
- El gasto social tiene alta persistencia temporal.  
- Los municipios con mayor esfuerzo tributario tienden a invertir más en gasto social.  
- Random Forest es el mejor modelo para predecir gasto social mensual.  
- El análisis confirma que **fortalecer la recaudación local** podría mejorar la inversión social sostenida.


### Instrucciones de ejecución

A continuación se detallan los pasos para reproducir este trabajo en cualquier entorno local o en Google Colab.

#### **Clonar el repositorio**
Descargue el proyecto desde GitHub con el siguiente comando: git clone git clone https://github.com/lyn090708-sys/Trabajo_autonomia_gasto_social.git cd Trabajo_autonomia_gasto_social

### Instalar librerías necesarias
pip install pandas==2.2.2 numpy==1.26.4 matplotlib==3.8.3 seaborn==0.13.2 scikit-learn==1.5.0 statsmodels==0.14.1

### Abrir el notebook para ejecutar el análisis
jupyter notebook Trabajo_3.ipynb


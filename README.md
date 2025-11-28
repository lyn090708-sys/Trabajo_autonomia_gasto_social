# Análisis del Mecanismo Fiscal y su Relación con el Gasto Social en Gobiernos Locales del Perú (2014–2019)

## Introducción

El presente estudio examina cómo la estructura fiscal de los gobiernos locales del Perú influye en su capacidad para financiar gasto social, particularmente en educación y salud, durante el periodo 2014–2019. En un contexto donde la autonomía financiera municipal es limitada y la dependencia de transferencias del gobierno central es elevada, resulta relevante analizar qué factores fiscales y administrativos condicionan las decisiones de inversión social de los municipios.

El propósito del análisis es determinar si una mayor autonomía financiera —expresada como la capacidad de generar ingresos propios— se asocia con un mayor nivel de gasto social, y si la alta dependencia de transferencias puede restringir dicha inversión. Asimismo, el estudio incorpora elementos estructurales como el esfuerzo tributario, la capacidad administrativa y el impacto de recursos extraordinarios como el canon, con el fin de comprender los determinantes fiscales que influyen en la priorización del gasto.

La importancia de este trabajo radica en proporcionar evidencia empírica sobre el funcionamiento del sistema fiscal municipal, identificando las limitaciones y potencialidades de los gobiernos locales en su rol de proveedores de servicios públicos esenciales. Los resultados permiten entender los incentivos y restricciones que moldean la asignación del gasto social y constituyen un insumo para la formulación de políticas de fortalecimiento fiscal y descentralización.

---

## Objetivo del estudio

Evaluar si los municipios con mayor autonomía financiera y mayor capacidad para generar recursos propios tienden a asignar un mayor nivel de gasto social, y determinar cómo la dependencia de transferencias, el esfuerzo tributario y la disponibilidad de recursos extraordinarios influyen en esta relación. Adicionalmente, se busca modelar y predecir la dinámica temporal del gasto social agregado a nivel nacional y comprender los determinantes fiscales más relevantes.

---

## Datos utilizados

El estudio emplea información del Ministerio de Economía y Finanzas (MEF), incluyendo:

- Ejecución presupuestal mensual (devengado) por función.
- Transferencias intergubernamentales (Canon, FONCOMUN, regalías, entre otros).
- Ingresos tributarios y no tributarios municipales.
- Información de estructura fiscal e ingresos propios.

Se construyó un panel mensual por municipalidad y posteriormente una serie temporal agregada con el promedio nacional para identificar tendencias generales del gasto social.
Link de la data: "https://drive.google.com/uc?id=14SzqUbYjGUqF8pJFM_RndMukbHimynr3"
---

## Metodología general

### 1. Limpieza e integración de datos
- Homogeneización de nombres, códigos y periodos.
- Conversión de columnas numéricas.
- Eliminación de observaciones inválidas (autonomía = 0 o gasto social = 0).
- Construcción de indicadores fiscales normalizados.

### 2. Construcción de variables fiscales
Se desarrollaron indicadores clave:

- Autonomía financiera.
- Dependencia de transferencias.
- Esfuerzo tributario relativo.
- Canon como proporción de transferencias.
- Interacción autonomía × transferencias.
- Autonomía cuadrática.
- Relación ingresos propios / transferencias.

Estas variables permiten capturar no linealidades, relaciones estructurales y mecanismos de dependencia fiscal.

### 3. Análisis descriptivo
- Distribución de variables fiscales.
- Evolución temporal del gasto social.
- Identificación de patrones estacionales y ciclos.
- Matriz de correlaciones entre indicadores.

### 4. Análisis de Componentes Principales (PCA)
El PCA permitió reducir la dimensionalidad y entender patrones estructurales:

- El primer componente explica aproximadamente el 48 % de la varianza y distingue municipios autónomos de dependientes.
- El segundo componente explica cerca del 28 % y está asociado a la composición del canon.
- Los dos primeros componentes resumen alrededor del 76 % de la estructura fiscal municipal.

### 5. Modelos predictivos
Se utilizaron diversos modelos supervisados sobre la serie temporal agregada:

- RidgeCV
- LassoCV
- Random Forest
- XGBoost
- MLPRegressor (red neuronal)
- Validación temporal con TimeSeriesSplit

La métrica principal fue el error cuadrático medio (MSE).

### 6. Modelo causal (DAG)
Se desarrolló un DAG que representa el mecanismo fiscal que determina el gasto social, considerando autonomía, esfuerzo tributario, capacidad administrativa, dependencia de transferencias, shocks económicos y canon. Este esquema identifica confounders relevantes y relaciones económicas plausibles.

---

## Principales hallazgos

- La autonomía financiera municipal es considerablemente baja y se mantiene cercana a cero para la mayoría de municipios.
- La dependencia de transferencias es estructural y configura los incentivos fiscales locales.
- El gasto social muestra una fuerte persistencia temporal, lo que sugiere que las decisiones se ajustan gradualmente.
- El esfuerzo tributario se asocia positivamente con mayores niveles de gasto social.
- Los municipios con mayor capacidad recaudatoria tienden a invertir más en servicios sociales.
- Los modelos no lineales (XGBoost y MLP) identifican relaciones complejas entre autonomía, transferencias y gasto.
- Random Forest y XGBoost muestran buen desempeño predictivo, aunque la variabilidad temporal y el tamaño reducido de la serie presentan limitaciones.
- El análisis causal indica que la autonomía y la capacidad administrativa influyen directamente en la asignación del gasto social, mientras que shocks económicos y la estructura de transferencias actúan como confounders.

---

## Cómo reproducir el proyecto

### Clonar el repositorio
```bash
git clone https://github.com/lyn090708-sys/Trabajo_autonomia_gasto_social.git
cd Trabajo_autonomia_gasto_social


### Instalar librerías necesarias
pip install pandas==2.2.2 numpy==1.26.4 matplotlib==3.8.3 seaborn==0.13.2 scikit-learn==1.5.0 statsmodels==0.14.1

### Abrir el notebook para ejecutar el análisis
jupyter notebook Trabajo_3.ipynb


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


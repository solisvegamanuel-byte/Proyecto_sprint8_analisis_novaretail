# 📊 NovaRetail+ | Explorando los factores que impulsan el valor del cliente

**Análisis de E-commerce | Python · Pandas · SciPy · Estadística · Análisis Correlacional**

## 1. 📊 Contexto y problema de negocio

NovaRetail+ es una plataforma de comercio electrónico en Latinoamérica que busca comprender qué factores del comportamiento de sus clientes están asociados con los ingresos que generan para el negocio.

Al cierre de 2024, el equipo de Crecimiento y Retención necesitaba identificar qué variables podían aportar información relevante para mejorar las estrategias de adquisición, fidelización y generación de ingresos.

Aunque la empresa dispone de información sobre frecuencia de compra, visitas, inversión publicitaria, satisfacción y características de sus usuarios, no estaba claro cuáles de estas variables presentaban relaciones significativas con el valor económico de cada cliente.

### Preguntas de negocio

- ¿Qué comportamientos presentan mayor asociación con el ingreso anual generado?
- ¿Los usuarios que visitan la plataforma con mayor frecuencia generan más ingresos?
- ¿Existe alguna relación entre la inversión en publicidad dirigida y la actividad del cliente?
- ¿La satisfacción se relaciona con el abandono de la plataforma?
- ¿La membresía premium presenta asociaciones relevantes con las compras o los ingresos?
- ¿Qué variables podrían ser útiles para diseñar futuras estrategias de crecimiento y retención?

**Problema central:** identificar y evaluar relaciones entre variables comerciales, conductuales y demográficas para orientar decisiones de negocio, evitando confundir correlación con causalidad.

---

## 2. 🎯 Objetivo y estrategia de análisis

El objetivo principal fue desarrollar un análisis correlacional de los clientes de NovaRetail+ durante 2024, identificando las relaciones estadísticas más relevantes y traduciendo los resultados en recomendaciones para el equipo de Crecimiento y Retención.

Para ello, organicé el proyecto en seis etapas:

1. **Exploración:** comprender la estructura, calidad y distribución de los datos.
2. **Preparación:** verificar tipos de datos, valores faltantes y características de cada variable.
3. **Visualización:** construir un mapa de correlaciones y gráficos de dispersión.
4. **Evaluación estadística:** aplicar Pearson, Spearman, correlación punto-biserial y V de Cramér.
5. **Interpretación:** diferenciar relaciones fuertes, débiles, estadísticamente significativas y potencialmente engañosas.
6. **Recomendaciones:** convertir los resultados en posibles líneas de investigación y experimentación comercial.

La estrategia consistió en seleccionar el método estadístico según la naturaleza de las variables, contrastar los resultados con evidencia visual y evaluar su significado desde una perspectiva de negocio.

**Principio metodológico:** una asociación estadística no demuestra que una variable cause cambios en otra.

---

## 3. 🧰 Tecnologías utilizadas

| Herramienta | Aplicación |
|---|---|
| Python | Desarrollo del análisis estadístico |
| Pandas | Exploración, transformación y agrupación |
| NumPy | Cálculos numéricos y V de Cramér |
| SciPy | Pruebas de correlación y chi-cuadrado |
| Seaborn | Heatmap y gráficos de dispersión |
| Matplotlib | Visualización y líneas de tendencia |
| Jupyter Notebook | Documentación, resultados y reporte ejecutivo |

### Dataset utilizado

**Archivo:** `novaretail_comportamiento_clientes_2024.csv`

| Característica | Resultado |
|---|---|
| Registros | 15,000 |
| Variables | 12 |
| Período | 2024 |
| Valores faltantes iniciales | 0 |
| Variable objetivo | `ingreso_anual` |

El dataset contiene información sobre clientes, actividad de compra, inversión publicitaria, satisfacción, membresía premium, abandono, región y dispositivo utilizado.

La variable `ingreso_anual` representa el ingreso anual generado por cada cliente para la empresa, no el salario personal del usuario.

---

## 4. 🔎 Desarrollo del proyecto

### Etapa 1. Exploración y comprensión de los datos

**Problema:** antes de estudiar relaciones estadísticas, era necesario comprender cómo estaban distribuidas las variables y comprobar si la información era adecuada para el análisis.

Cargué el dataset mediante Pandas y realicé una exploración inicial utilizando:

- `df.info()`
- `df.head()`
- `df.describe()`
- `nunique()`
- `groupby()`

**Trabajo realizado:**

- Verificación de registros, columnas y tipos de datos.
- Identificación de variables numéricas, categóricas y binarias.
- Revisión de valores faltantes.
- Exploración de medidas descriptivas.
- Cálculo de tasas de abandono según membresía.
- Comparación de compras por región y dispositivo.

### Resultados exploratorios

| Indicador | Resultado |
|---|---:|
| Edad promedio | 38.26 años |
| Visitas mensuales promedio | 10.03 |
| Compras mensuales promedio | 1.21 |
| Participación de móviles en las compras registradas | 65.34% |
| Participación de escritorio | 24.70% |
| Participación de tablet | 9.96% |

También identifiqué una diferencia importante en las tasas de abandono:

| Segmento | Tasa de abandono |
|---|---:|
| Clientes sin membresía premium | 16.81% |
| Clientes premium | 4.36% |

La diferencia descriptiva es de aproximadamente **12.45 puntos porcentuales**.

Este resultado sugiere una asociación relevante para investigar, pero no demuestra que adquirir la membresía premium reduzca el abandono.

**Resultado:** se obtuvo una caracterización inicial de los clientes y se identificaron patrones que justificaban un análisis estadístico más profundo.

### Etapa 2. Preparación y diagnóstico de variables

**Problema:** las técnicas correlacionales requieren identificar correctamente la naturaleza de las variables y verificar que los datos permitan aplicar los métodos seleccionados.

El dataset contenía 15,000 registros sin valores faltantes. La mayor parte de los campos ya tenía tipos adecuados.

**Acciones realizadas:**

- Conversión de `edad` de `float64` a `int64`.
- Verificación de variables binarias codificadas como 0 y 1.
- Identificación de tres tipos de dispositivo y cuatro regiones.
- Revisión de distribuciones y rangos numéricos.
- Documentación de supuestos para cada técnica estadística.

Se clasificaron las variables en tres grupos:

**Numéricas:** edad, nivel de ingreso del cliente, visitas, compras, gasto publicitario, satisfacción e ingreso anual generado.

**Binarias:** membresía premium y abandono.

**Categóricas:** región y tipo de dispositivo.

**Resultado:** la información quedó preparada para aplicar diferentes métodos de asociación de acuerdo con el tipo de variable.

### Etapa 3. Visualización exploratoria de correlaciones

**Problema:** una correlación numérica aislada puede resultar engañosa si no se examina la distribución de los datos.

Construí una matriz de correlación y diferentes gráficos de dispersión utilizando Seaborn y Matplotlib.

**Visualizaciones desarrolladas:**

1. Heatmap de correlaciones entre variables numéricas.
2. Scatterplot de compras mensuales frente al ingreso anual.
3. Scatterplot de visitas mensuales frente al gasto publicitario.
4. Scatterplot de visitas mensuales frente al ingreso anual.
5. Scatterplot de compras mensuales frente a visitas mensuales.

Los gráficos incorporaron líneas de tendencia para facilitar la interpretación visual.

**Resultados iniciales:**

- Se identificó una relación positiva muy fuerte entre `compras_mes` e `ingreso_anual`.
- La inversión en publicidad dirigida y las visitas mensuales mostraron una asociación positiva moderada.
- Otras relaciones presentaron una magnitud considerablemente menor.

**Resultado:** la visualización permitió seleccionar relaciones relevantes para comprobarlas mediante coeficientes estadísticos.

### Etapa 4. Análisis de correlación con Pearson y Spearman

**Problema:** era necesario cuantificar las relaciones identificadas visualmente y distinguir patrones lineales de asociaciones monotónicas.

Utilicé los coeficientes de Pearson y Spearman sobre pares de variables numéricas.

### Resultados

| Variables | Pearson | Spearman |
|---|---:|---:|
| Compras mensuales vs. ingreso anual | 0.9671 | No calculado |
| Publicidad dirigida vs. visitas mensuales | 0.5789 | 0.5593 |
| Publicidad dirigida vs. ingreso anual | 0.1975 | 0.1850 |

**Interpretación:**

**Compras mensuales e ingreso anual**

La correlación de Pearson de 0.9671 indica una asociación lineal positiva extremadamente fuerte.

Sin embargo, esta relación debe interpretarse cuidadosamente porque ambas variables pueden representar dimensiones muy relacionadas de la actividad económica del cliente.

No es correcto concluir que una mayor frecuencia de compra causa, por sí sola, un incremento independiente del ingreso.

**Publicidad dirigida y visitas mensuales**

Los coeficientes de Pearson (0.5789) y Spearman (0.5593) muestran una asociación positiva moderada.

La similitud de sus magnitudes respalda la presencia de una relación positiva, aunque no demuestra que la publicidad sea responsable del incremento en las visitas.

**Publicidad dirigida e ingreso anual**

Los coeficientes obtenidos indican una asociación positiva débil.

Esto sugiere que una mayor inversión publicitaria por cliente no necesariamente se acompaña de un incremento proporcional en los ingresos generados.

**Resultado:** se identificaron diferencias importantes entre la fuerza de las asociaciones y su posible utilidad para el negocio.

### Etapa 5. Correlación punto-biserial

**Problema:** algunas de las variables de interés estaban codificadas de forma binaria, por lo que necesitaba un método adecuado para estudiar su relación con indicadores numéricos.

Utilicé `pointbiserialr()` de SciPy para evaluar cuatro combinaciones.

| Relación | Coeficiente | Valor p |
|---|---:|---:|
| Premium vs. compras mensuales | 0.0034 | 0.6744 |
| Premium vs. ingreso anual | 0.0931 | < 0.001 |
| Abandono vs. satisfacción | -0.0238 | 0.0035 |
| Abandono vs. visitas mensuales | -0.0089 | 0.2734 |

### Interpretación

**Membresía premium e ingreso anual**

La asociación fue positiva y estadísticamente significativa, aunque su magnitud fue pequeña.

Esto significa que existe evidencia de una diferencia estadística, pero la pertenencia al programa premium, por sí sola, aporta poca información sobre el ingreso anual generado.

**Abandono y satisfacción**

La asociación fue negativa y estadísticamente significativa, pero extremadamente débil.

La dirección es compatible con una mayor tendencia al abandono cuando disminuye la satisfacción, aunque el tamaño del efecto es demasiado pequeño para utilizar esta variable como explicación suficiente del abandono.

**Abandono y visitas mensuales**

No se encontró evidencia estadística suficiente de asociación bajo el umbral convencional de significancia del 5%.

**Membresía premium y compras mensuales**

El coeficiente fue prácticamente nulo y el resultado no fue estadísticamente significativo.

**Resultado:** el análisis permitió distinguir entre significancia estadística y relevancia práctica, evitando sobreinterpretar coeficientes pequeños.

### Etapa 6. Asociaciones categóricas con V de Cramér

**Problema:** era necesario estudiar si variables categóricas como región y tipo de dispositivo presentaban asociaciones relevantes con la membresía premium o el abandono.

Construí tablas de contingencia mediante `pd.crosstab()` y calculé estadísticos chi-cuadrado utilizando SciPy.

Posteriormente obtuve el coeficiente V de Cramér para cada combinación.

| Variables | V de Cramér |
|---|---:|
| Región vs. dispositivo | 0.0124 |
| Dispositivo vs. premium | 0.0197 |
| Dispositivo vs. abandono | 0.0072 |
| Región vs. premium | 0.0126 |
| Región vs. abandono | 0.0154 |

Todos los coeficientes fueron cercanos a cero.

**Interpretación:** no se identificaron asociaciones de magnitud relevante entre las variables categóricas analizadas.

La evidencia no respalda utilizar exclusivamente la región o el dispositivo como criterios principales para segmentar estrategias de retención o suscripción premium.

**Resultado:** se descartó la utilidad práctica de varias asociaciones categóricas como base aislada para estrategias comerciales.

---

## 5. 📈 Resultados y hallazgos principales

### Hallazgo 1. Las compras mensuales presentan la asociación más fuerte con el ingreso anual

<escape>**Pearson: r = 0.9671**</escape>

La relación entre frecuencia de compra e ingreso anual fue considerablemente más fuerte que las demás asociaciones numéricas evaluadas.

**Interpretación de negocio:** ambas variables podrían reflejar parcialmente un mismo concepto subyacente: la actividad o valor económico del cliente.

Por ello, antes de utilizarlas simultáneamente en un modelo predictivo, sería conveniente investigar la redundancia entre ambas y comprobar posibles problemas de multicolinealidad.

### Hallazgo 2. La inversión publicitaria está relacionada con la frecuencia de visitas

<escape>**Pearson: r = 0.5789 | Spearman: ρ = 0.5593**</escape>

Se identificó una asociación positiva moderada entre publicidad dirigida y visitas mensuales.

A diferencia de características estructurales como la región, el presupuesto publicitario es una variable que la empresa puede modificar.

**Interpretación de negocio:** esta asociación convierte a la publicidad dirigida en una candidata relevante para experimentación.

Sin embargo, es posible que la empresa asigne mayor inversión a los clientes que ya presentan más actividad. Por lo tanto, no puede atribuirse el incremento de visitas directamente a la publicidad sin evidencia experimental.

### Hallazgo 3. La satisfacción muestra una asociación estadística débil con el abandono

<escape>**Punto-biserial: r = -0.0238 | p = 0.0035**</escape>

El coeficiente negativo indica que una mayor satisfacción se asocia con una ligera reducción en el indicador de abandono.

Aunque el resultado fue estadísticamente significativo, su magnitud fue muy pequeña.

**Interpretación de negocio:** la satisfacción puede considerarse una variable complementaria para investigar el abandono, pero no resulta suficiente para construir una estrategia predictiva sólida por sí sola.

### Hallazgo 4. Región y dispositivo no mostraron asociaciones categóricas relevantes

Los cinco coeficientes de V de Cramér se encontraron entre 0.0072 y 0.0197.

**Interpretación de negocio:** los resultados no justifican priorizar la segmentación de abandono o membresía premium exclusivamente por región o dispositivo.

Sería más conveniente investigar características del comportamiento, experiencia y trayectoria del cliente.

### Hallazgo 5. La membresía premium merece un análisis específico de retención

Durante la exploración se observó una tasa de abandono de 16.81% entre clientes sin membresía premium, frente a 4.36% entre los clientes premium.

Esta diferencia descriptiva es considerable y abre una pregunta de negocio adicional:

**¿Qué características distinguen a los clientes premium y cómo se relacionan con su permanencia en la plataforma?**

La diferencia no permite afirmar que la membresía premium prevenga el abandono. Es posible que los clientes más comprometidos con la plataforma también sean quienes tienden a contratarla.

---

## 6. ✅ Validación y confiabilidad del análisis

Para respaldar los resultados, apliqué métodos de verificación y seleccioné técnicas estadísticas adecuadas para las variables estudiadas.

| Control | Evidencia |
|---|---|
| Integridad de datos | 15,000 registros y 12 columnas sin valores nulos |
| Tipos de datos | Revisión mediante `df.info()` |
| Variables binarias | Verificación de sus valores únicos |
| Estadística descriptiva | Uso de `df.describe()` y agrupaciones |
| Correlaciones numéricas | Pearson y Spearman |
| Correlaciones binarias | Punto-biserial y valores p |
| Asociaciones categóricas | Chi-cuadrado y V de Cramér |
| Validación visual | Heatmap y scatterplots |
| Interpretación | Distinción entre fuerza de asociación, significancia y causalidad |

### Evidencia de revisión

El proyecto recibió una evaluación aprobatoria en su primera revisión.

La retroalimentación destacó:

- La calidad de los diagnósticos iniciales.
- La selección de relaciones relevantes para visualización.
- La interpretación de los coeficientes punto-biseriales.
- La aplicación de V de Cramér.
- El análisis crítico sobre posibles relaciones engañosas.
- La identificación del gasto publicitario como variable potencialmente accionable.

### Consideraciones metodológicas

Para mantener la confiabilidad de las conclusiones, es importante reconocer las siguientes limitaciones:

- Las correlaciones no permiten establecer relaciones causales.
- Un resultado estadísticamente significativo puede representar un efecto muy pequeño.
- La existencia de numerosas comparaciones requiere cautela ante posibles falsos positivos.
- La correlación fuerte entre compras e ingreso puede reflejar una relación estructural entre ambas métricas.
- Los valores de V de Cramér describen fuerza de asociación, pero no explican causalidad.
- El análisis no controla simultáneamente otras variables que podrían influir en los resultados.

**Ajuste pendiente:** calcular y documentar la correlación de Spearman entre `compras_mes` e `ingreso_anual`, ya que el notebook original solamente contiene el cálculo de Pearson para ese par.

---

## 7. 💡 Conclusiones y recomendaciones de negocio

El análisis permitió identificar qué variables presentaban las asociaciones más relevantes con la actividad e ingreso generado por los clientes de NovaRetail+ durante 2024.

La principal conclusión fue que **la frecuencia de compra presenta una asociación extremadamente fuerte con el ingreso anual**, mientras que la inversión publicitaria muestra una relación moderada con la actividad de visitas.

En contraste, las variables geográficas y de dispositivo presentaron asociaciones categóricas prácticamente nulas en los pares evaluados.

### Recomendación 1. Evaluar experimentalmente la publicidad dirigida

La publicidad dirigida fue una de las variables con mayor asociación observada y representa una decisión de presupuesto controlable.

**Acción propuesta:** desarrollar un experimento A/B con asignación aleatoria para evaluar si incrementar o modificar la inversión publicitaria produce cambios medibles en visitas, conversiones e ingresos.

### Recomendación 2. Investigar los factores detrás del abandono

Las asociaciones observadas con satisfacción y visitas fueron demasiado pequeñas para explicar adecuadamente el abandono.

**Acción propuesta:** incorporar información adicional sobre:

- Motivos de cancelación.
- Historial de atención al cliente.
- Antigüedad y frecuencia de uso.
- Cambios en precios.
- Experiencias negativas.
- Comportamiento previo al abandono.

### Recomendación 3. Analizar el valor de los clientes premium

La diferencia descriptiva en tasas de abandono entre clientes premium y no premium justifica una investigación adicional.

**Acción propuesta:** comparar grupos equivalentes de clientes y estudiar su actividad previa a la contratación para distinguir posibles efectos de selección de una eventual contribución de la membresía.

### Recomendación 4. Evitar variables redundantes en futuros modelos

La relación entre compras mensuales e ingreso anual requiere atención antes de construir modelos explicativos o predictivos.

**Acción propuesta:** revisar las definiciones de ambas métricas con el equipo de negocio y evaluar su redundancia antes de utilizarlas conjuntamente como predictores.

### Recomendación 5. Priorizar variables conductuales

Las asociaciones categóricas débiles sugieren que la región y el dispositivo no deben ser los únicos criterios para diseñar estrategias comerciales.

**Acción propuesta:** investigar segmentaciones basadas en comportamiento, frecuencia de compra, experiencia y actividad del cliente, comprobando posteriormente su utilidad real.

### Valor aportado

El proyecto permitió transformar datos de comportamiento en evidencia estadística para orientar investigaciones y decisiones comerciales.

Desde el punto de vista técnico, integré análisis exploratorio, visualización, correlaciones numéricas, pruebas de significancia y asociaciones categóricas.

Desde el punto de vista del negocio, identifiqué variables relevantes, diferencié asociaciones fuertes de relaciones poco útiles y propuse experimentos para comprobar hipótesis comerciales.

**El valor principal del trabajo no fue únicamente encontrar correlaciones, sino determinar cuáles merecen atención y cuáles podrían conducir a decisiones equivocadas.**

---

## 8. 📁 Recursos del proyecto

**Dataset**

- `novaretail_comportamiento_clientes_2024.csv` — 15,000 registros de clientes correspondientes a 2024.

**Notebook**

- `S8 Student Version-Project-NovaRetail (2).ipynb`

**Contenido del análisis**

- Exploración y validación de datos.
- Estadística descriptiva.
- Heatmap de correlaciones.
- Scatterplots con líneas de tendencia.
- Pearson y Spearman.
- Correlación punto-biserial.
- Chi-cuadrado y V de Cramér.
- Interpretación de resultados.
- Limitaciones y recomendaciones de negocio.

### Reproducibilidad

El análisis utiliza Python y las librerías Pandas, NumPy, SciPy, Seaborn y Matplotlib.

Para reproducir los resultados se requiere disponer del CSV original y ajustar la ruta de lectura del archivo según el entorno de ejecución.

---

## 👨‍💻 Autor

**Manuel Eduardo Solís Vega**

Data Analyst Jr. | Python · SQL · Power BI · Estadística Aplicada

Proyecto desarrollado como parte de mi portafolio profesional, enfocado en análisis estadístico, comportamiento de clientes y toma de decisiones basada en datos.

# UT8 — Reducción de Dimensionalidad y PCA
## Análisis del dataset *Statistical Review of World Energy*

Este proyecto forma parte de la unidad **UT8 – Reducción de Dimensionalidad** y tiene como objetivo explorar diferentes técnicas de selección y reducción de características aplicadas a un dataset energético global.

El análisis se realiza utilizando datos del **Statistical Review of World Energy**, una de las bases de datos energéticas más completas disponibles a nivel internacional.

El objetivo del trabajo es investigar si el **perfil energético de un país** permite predecir si dicho país pertenece o no a la **OCDE**, utilizando diferentes técnicas de reducción de dimensionalidad y selección de variables.

---

# Contexto del dataset

El dataset utilizado en este proyecto procede del informe anual **Statistical Review of World Energy**, publicado por el **Energy Institute**.

El Energy Institute es una organización internacional dedicada al análisis del sistema energético global. Desde 1952 publica este informe que recopila estadísticas energéticas de prácticamente todos los países del mundo.

Este informe es utilizado habitualmente por:

- organismos internacionales
- gobiernos
- investigadores
- economistas
- empresas del sector energético

El dataset recoge información sobre:

- producción energética
- consumo energético
- generación eléctrica
- energías renovables
- emisiones de CO₂
- recursos energéticos

Los datos cubren el periodo **1965–2024** e incluyen aproximadamente **140 países**.

---

# Estructura del dataset

El dataset original se presenta en formato **long (narrow)**.

Esto significa que cada fila representa una observación del tipo:

(país, año, métrica energética)

Ejemplo conceptual:

| Country | Year | Var | Value |
|-------|------|------|------|
| Spain | 2020 | oilcons_ej | 2.3 |
| Spain | 2020 | solar_twh | 36 |
| Spain | 2020 | co2_combust_mtco2 | 245 |

Para aplicar técnicas de **machine learning**, el dataset se transforma a formato **wide**, donde cada métrica energética se convierte en una columna.

De este modo cada fila representa **un país** y cada columna representa **una característica energética**.

---

# ¿Qué es la OCDE?

La **OCDE (Organización para la Cooperación y el Desarrollo Económico)** es una organización internacional formada por países con economías avanzadas y sistemas democráticos.

Su objetivo es promover:

- crecimiento económico sostenible  
- cooperación internacional  
- comercio global  
- políticas públicas eficaces  

Actualmente cuenta con **38 países miembros**, entre ellos:

- España  
- Estados Unidos  
- Alemania  
- Francia  
- Japón  
- Canadá  
- Australia  

Los países de la OCDE suelen presentar características comunes:

- mayor desarrollo económico  
- mayor consumo energético per cápita  
- infraestructuras energéticas más desarrolladas  
- mayor transición hacia energías renovables  

---

# Justificación de la variable objetivo

En este trabajo se utiliza la variable **OECD** como variable objetivo para un problema de **clasificación binaria**.

El objetivo es investigar si el **perfil energético de un país** permite identificar si pertenece o no a la OCDE.

Esta elección es interesante porque el sistema energético de un país suele reflejar su nivel de desarrollo económico y tecnológico.

Por ejemplo:

- los países más desarrollados suelen tener mayor electrificación
- presentan mayor consumo energético per cápita
- suelen tener mayor penetración de energías renovables
- tienen infraestructuras energéticas más avanzadas

Por tanto, es razonable plantear la hipótesis de que **los países OCDE presentan patrones energéticos diferenciables** respecto al resto del mundo.

---

# Unidades energéticas utilizadas

El dataset utiliza diversas unidades energéticas estándar.

| Unidad | Significado |
|------|------|
| EJ | Exajoule (10¹⁸ joules) |
| TWh | Terawatt-hora |
| PJ | Petajoule |
| bcm | Billion cubic meters |
| bcfd | Billion cubic feet per day |
| kbd | Thousand barrels per day |
| mt | Million tonnes |
| kt | Kilotonnes |
| pc | Per capita |

Estas unidades permiten expresar energía, producción o consumo en diferentes escalas.

---

# Diccionario de variables utilizadas

El modelo final utiliza **30 métricas energéticas** que describen diferentes dimensiones del sistema energético de cada país.

## Demografía

| Variable | Descripción |
|------|------|
| pop | Población total del país |

---

## Consumo energético total

| Variable | Descripción |
|------|------|
| tes_ej | Consumo total de energía primaria |
| tes_gj_pc | Consumo energético total per cápita |

---

## Electricidad

| Variable | Descripción |
|------|------|
| elect_twh | Generación total de electricidad |

---

## Combustibles fósiles

| Variable | Descripción |
|------|------|
| coalcons_ej | Consumo total de carbón |
| gascons_bcfd | Consumo de gas natural |
| gascons_bcm | Consumo de gas natural en metros cúbicos |
| gascons_ej | Consumo de gas natural expresado como energía |

---

## Petróleo

| Variable | Descripción |
|------|------|
| oilcons_ej | Consumo de petróleo |
| oilcons_kbd | Consumo de petróleo en barriles diarios |
| oilcons_mt | Consumo de petróleo en millones de toneladas |
| liqcons_kbd | Consumo total de combustibles líquidos |

---

## Energía nuclear

| Variable | Descripción |
|------|------|
| nuclear_ej | Producción de energía nuclear |

---

## Energía hidroeléctrica

| Variable | Descripción |
|------|------|
| hydro_ej | Producción hidroeléctrica |

---

## Energías renovables

| Variable | Descripción |
|------|------|
| renewables_ej | Consumo total de energías renovables |
| ren_power_ej | Energía renovable destinada a generación eléctrica |
| ren_power_twh | Generación renovable en TWh |
| ren_power_twh_net | Generación renovable neta |

---

## Energía solar

| Variable | Descripción |
|------|------|
| solar_ej | Producción de energía solar |
| solar_twh | Producción solar en TWh |
| solar_twh_net | Producción solar neta |

---

## Energía eólica

| Variable | Descripción |
|------|------|
| wind_ej | Producción de energía eólica |
| wind_twh | Producción eólica en TWh |
| wind_twh_net | Producción eólica neta |

---

## Bioenergía y geotermia

| Variable | Descripción |
|------|------|
| biogeo_ej | Energía procedente de biomasa y geotermia |
| biogeo_twh | Producción bioenergética |
| biogeo_twh_net | Producción bioenergética neta |

---

## Emisiones de CO₂

| Variable | Descripción |
|------|------|
| co2_combust_mtco2 | Emisiones de CO₂ procedentes de combustibles fósiles |
| co2_combust_pc | Emisiones de CO₂ per cápita |
| co2_combust_per_ej | Intensidad de emisiones por unidad de energía |

---

# Variables más importantes según RFE

La técnica **Recursive Feature Elimination (RFE)** identificó **8 variables clave** que concentran la mayor parte del poder predictivo del modelo.

Estas variables son:

- biogeo_ej
- wind_ej
- solar_twh_net
- co2_combust_mtco2
- solar_twh
- co2_combust_per_ej
- solar_ej
- pop

Estas variables describen principalmente tres dimensiones del sistema energético:

### 1. Nivel de desarrollo energético
Variables como:

- pop
- co2_combust_mtco2

reflejan el tamaño del sistema energético de un país.

Los países más desarrollados suelen tener mayor demanda energética y mayores emisiones totales.

---

### 2. Transición hacia energías renovables

Variables como:

- solar_ej
- solar_twh
- wind_ej

indican el nivel de desarrollo de energías renovables.

Los países de la OCDE suelen tener **mayor penetración de energía solar y eólica**.

---

### 3. Intensidad energética y emisiones

Variables como:

- co2_combust_per_ej

miden la **intensidad de emisiones por unidad de energía consumida**.

Esto refleja la eficiencia del sistema energético y el tipo de fuentes utilizadas.

---

# Interpretación del modelo

El modelo sugiere que la pertenencia a la OCDE está fuertemente relacionada con:

- el tamaño del sistema energético
- el nivel de electrificación
- la penetración de energías renovables
- el perfil de emisiones de CO₂

Esto refleja que los países más desarrollados presentan **sistemas energéticos más complejos y diversificados**.

---

# Conclusión

El análisis demuestra que una pequeña cantidad de variables energéticas es suficiente para capturar gran parte de las diferencias entre países OCDE y no OCDE.

Las técnicas de selección de características permiten identificar estas variables clave y reducir significativamente la dimensionalidad del problema sin perder capacidad predictiva.

Este tipo de análisis es útil para comprender cómo los **patrones energéticos globales están relacionados con el desarrollo económico de los países**.
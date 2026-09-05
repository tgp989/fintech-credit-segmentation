# Integración Multidimensional: Sector Fintech

## Descripción del proyecto

Este proyecto desarrolla un proceso de **integración multidimensional de datos aplicado al sector fintech**, con el propósito de optimizar la asignación de solicitantes de crédito y apoyar la reorganización de las sucursales encargadas de su evaluación.

El caso plantea la reducción del número de sucursales mediante la consolidación de los solicitantes en **cinco nuevos grupos**, utilizando sus características demográficas y financieras para identificar perfiles similares.

Para realizar esta segmentación se seleccionaron variables como edad, hijos, personas a cargo, estrato, ingresos, egresos, monto del crédito, plazo y cuota. A partir de estas variables se construyeron cinco semillas de integración y posteriormente se aplicó un proceso de agrupamiento mediante **K-medois**, obteniendo cinco clusters que representan las nuevas sucursales.

Finalmente, se analizaron las características de cada grupo, su distribución geográfica y los porcentajes de preaprobación y prenegación de créditos.

---

## Objetivo

Realizar una integración multidimensional de los solicitantes de crédito que permita **segmentarlos en cinco grupos con características similares**, facilitando la toma de decisiones relacionada con la asignación de sucursales y la evaluación de los perfiles de crédito.

### Objetivos específicos

- Preparar y organizar la información de los solicitantes de crédito.
- Seleccionar las variables numéricas relevantes para el proceso de integración.
- Construir cinco semillas de integración como referencia para el agrupamiento.
- Clasificar los solicitantes mediante el método de K-medois.
- Analizar las características demográficas y financieras de cada cluster.
- Identificar la distribución geográfica de los solicitantes.
- Comparar los porcentajes de preaprobación y prenegación entre los clusters.
- Representar visualmente los perfiles de los grupos obtenidos.

---

## Base de datos

El proyecto utiliza una base de datos de **solicitantes de crédito en dólares (USD) y su ubicación por municipios**.

La información contiene variables relacionadas con las características personales, financieras y crediticias de los solicitantes.

### Variables utilizadas

Para el proceso de integración multidimensional se seleccionaron las siguientes variables:

| Variable | Descripción |
|---|---|
| `Edad` | Edad del solicitante |
| `Hijos` | Número de hijos |
| `Perscargo` | Número de personas a cargo |
| `Estrato` | Estrato socioeconómico |
| `Ingresos` | Ingresos del solicitante |
| `Egresos` | Egresos del solicitante |
| `Monto (EAD)` | Monto del crédito |
| `Plazo` | Plazo del crédito |
| `Cuota (COP)` | Cuota del crédito |

Adicionalmente, la base contiene información utilizada para analizar la procedencia geográfica y la decisión asociada a cada solicitante, incluyendo municipio, puntaje y probabilidad de incumplimiento.

---

## Metodología

El desarrollo del proyecto se realizó mediante las siguientes etapas:

### 1. Preparación de los datos

Se cargó la información desde un archivo Excel y se consolidaron los datos en un único `DataFrame`.

Posteriormente, los registros fueron reorganizados utilizando una semilla aleatoria (`random_state=42`) y se eliminaron los registros con valores faltantes.

### 2. Selección de variables

Se seleccionaron nueve variables numéricas relacionadas con las características demográficas y financieras de los solicitantes:

- Edad
- Hijos
- Personas a cargo
- Estrato
- Ingresos
- Egresos
- Monto del crédito
- Plazo
- Cuota

### 3. Creación de semillas de integración

Se utilizaron los primeros cinco registros de la base reorganizada como **semillas de integración**.

Estas semillas funcionan como puntos de referencia iniciales para clasificar posteriormente a los solicitantes según la similitud de sus características.

### 4. Agrupamiento mediante K-medois

Se aplicó un proceso de agrupamiento en el que cada solicitante es asignado al cluster cuya semilla presenta la menor distancia relativa respecto a sus variables.

A medida que se procesan los registros, las semillas se actualizan mediante la integración de los nuevos individuos asignados.

El procedimiento genera finalmente **cinco clusters**, correspondientes a las cinco nuevas sucursales planteadas en el caso.

### 5. Caracterización de los clusters

Una vez realizada la agrupación, se calcularon estadísticas descriptivas de las variables utilizadas, incluyendo:

- Media
- Mediana
- Desviación estándar

Esto permite identificar las principales características de cada grupo.

### 6. Análisis de decisiones de crédito

Se construyó una variable de decisión para clasificar a los solicitantes como:

- **Preaprobado**
- **Prenegado**

La clasificación utilizada en el proyecto considera como preaprobado a un solicitante cuando su `Score` es superior a 400 y su `Prob.Default (PD)` es inferior a 0,5.

Posteriormente, se calcularon los porcentajes de preaprobación y prenegación para cada cluster.

### 7. Análisis geográfico

Se analizó la procedencia de los solicitantes mediante la variable `Municipio`, identificando los municipios con mayor presencia dentro de cada cluster.

### 8. Normalización y perfilamiento

Las medias de las variables de cada cluster fueron normalizadas mediante `MinMaxScaler`.

Con esta información se construyeron **gráficos de araña**, utilizados para visualizar y comparar el perfil multidimensional de los cinco grupos.

### 9. Visualización

Finalmente, se generaron diferentes representaciones gráficas para facilitar la interpretación del proceso:

- Perfil de los clusters.
- Número de clientes por cluster.
- Preaprobación vs. prenegación.
- Municipios con mayor número de clientes por cluster.

---

## Herramientas utilizadas

- **Python**
- **Google Colab**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Seaborn**
- **Scikit-learn**
- **GitHub**

---

## Estructura del repositorio

```text
Reto-4-Integracion-Multidimensional-Fintech/
│
├── README.md
├── Reto_4.ipynb
│
└── data/
    └── 4. SolicitantesCrédito(USD)_Municipios.xlsx

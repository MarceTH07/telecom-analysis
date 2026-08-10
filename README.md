# telecom-analysis
Telecom customer analytics project using Python, Pandas and data visualization to clean data, analyze usage patterns, detect outliers and segment customers for retention and plan optimization.
# 📊 ConnectaTel — Customer Behavior & Segmentation Analysis

## 📌 Descripción del proyecto

Este proyecto analiza el comportamiento de los clientes de **ConnectaTel**, una empresa de telecomunicaciones con operaciones en Latinoamérica.

El análisis utiliza información de clientes, planes y consumo de servicios registrada hasta **2024**, con el propósito de transformar los datos disponibles en información útil para la toma de decisiones comerciales.

El proyecto fue desarrollado en **Python** utilizando principalmente **Pandas, Seaborn y Matplotlib** para realizar limpieza de datos, análisis exploratorio, detección de valores atípicos, visualización y segmentación de clientes.

---

## 🎯 Objetivo

El objetivo principal es analizar el comportamiento de los clientes de ConnectaTel para:

- Evaluar la calidad de los datos disponibles.
- Identificar y corregir valores inválidos y fechas inconsistentes.
- Analizar los patrones de consumo de llamadas y mensajes.
- Detectar comportamientos atípicos mediante análisis de outliers.
- Construir perfiles de clientes a partir de su comportamiento.
- Segmentar clientes por edad y nivel de uso.
- Generar insights útiles para retención, optimización de planes y estrategia comercial.

---

## 📂 Datasets utilizados

El análisis utiliza tres datasets:

### `plans.csv`

Contiene información sobre los planes comerciales disponibles, incluyendo:

- nombre del plan;
- mensajes incluidos;
- GB incluidos por mes;
- minutos incluidos;
- tarifa mensual;
- costos adicionales por GB, mensaje y minuto.

### `users_latam.csv`

Contiene información de los clientes:

- identificador del usuario;
- nombre y apellido;
- edad;
- ciudad;
- fecha de registro;
- plan contratado;
- fecha de churn.

### `usage.csv`

Contiene registros de utilización de los servicios:

- identificador del registro;
- identificador del usuario;
- tipo de uso (`call` o `text`);
- fecha;
- duración de llamadas;
- longitud de mensajes.

---

## 🔎 Etapas del análisis

### 1. Carga y exploración de datos

Se cargaron los tres datasets y se analizaron sus dimensiones, columnas, tipos de datos y valores no nulos mediante herramientas como:

- `.head()`
- `.shape`
- `.info()`

### 2. Evaluación de calidad de datos

Se analizaron valores faltantes, valores inválidos y posibles sentinels.

Entre los principales problemas encontrados se identificaron:

- valores faltantes en `city`;
- valores `?` utilizados como sentinel en `city`;
- edades inválidas representadas mediante `-999`;
- fechas de registro posteriores a 2024;
- valores faltantes estructurales en `duration` y `length`.

Se comprobó que los nulos de `duration` y `length` dependen del tipo de registro (`call` o `text`), por lo que se conservaron.

### 3. Limpieza y transformación

Se realizaron diferentes procesos de preparación:

- conversión de columnas a formato fecha;
- reemplazo de edades inválidas utilizando la mediana;
- reemplazo del sentinel `?` por valores nulos;
- identificación y tratamiento de fechas futuras;
- validación de valores faltantes.

### 4. Construcción del perfil de usuario

Los registros de uso fueron agregados por `user_id` para calcular:

- cantidad de mensajes;
- cantidad de llamadas;
- minutos totales de llamadas.

Posteriormente, estas métricas se combinaron con la información de clientes para construir el DataFrame `user_profile`.

### 5. Análisis exploratorio y visualización

Se analizaron las distribuciones de:

- edad;
- cantidad de mensajes;
- cantidad de llamadas;
- minutos de llamadas.

Se utilizaron histogramas diferenciados por tipo de plan para identificar patrones de comportamiento.

### 6. Detección de outliers

Se utilizaron **boxplots** y el método **IQR (Interquartile Range)** para detectar valores extremos.

Los límites superiores obtenidos fueron:

| Variable | Límite superior IQR | Máximo observado |
|---|---:|---:|
| Cantidad de mensajes | 11.50 | 17 |
| Cantidad de llamadas | 10.50 | 15 |
| Minutos de llamada | 61.86 | 155.69 |

Los outliers fueron conservados porque representan comportamientos de consumo plausibles y pueden identificar clientes de alto uso relevantes para el negocio.

### 7. Segmentación de clientes

Se desarrollaron dos modelos simples de segmentación.

#### Segmentación por uso

Los clientes fueron clasificados como:

- **Bajo uso:** menos de 5 llamadas y menos de 5 mensajes.
- **Uso medio:** menos de 10 llamadas y menos de 10 mensajes.
- **Alto uso:** resto de los casos.

#### Segmentación por edad

Los clientes fueron clasificados como:

- **Joven:** menor de 30 años.
- **Adulto:** entre 30 y 59 años.
- **Adulto Mayor:** 60 años o más.

---

## 💡 Principales insights

El análisis muestra que el segmento de **Uso medio concentra la mayor parte de los clientes**, mientras que el grupo de Alto uso representa una proporción menor pero potencialmente relevante desde el punto de vista comercial.

Por edad, la cartera está principalmente concentrada en **Adultos (30–59 años)**, seguida por Adultos Mayores y, finalmente, clientes Jóvenes.

También se identificaron clientes con niveles de consumo considerablemente superiores al comportamiento típico. Estos registros se conservaron porque pueden representar clientes reales de alto consumo y no necesariamente errores.

Los resultados sugieren oportunidades para:

- identificar clientes de Alto uso con plan Básico como posibles candidatos a migración hacia Premium;
- analizar clientes Premium con Bajo uso como potenciales casos de optimización o retención;
- revisar la adecuación de los planes actuales a los distintos niveles de consumo;
- desarrollar estrategias comerciales diferenciadas por edad y comportamiento.

---

## 🛠️ Tecnologías utilizadas

- Python
- Pandas
- Seaborn
- Matplotlib
- Jupyter Notebook / Google Colab

---

## ▶️ Cómo ejecutar el proyecto

El análisis se encuentra desarrollado en un **Jupyter Notebook (`.ipynb`)**.

Puede ejecutarse localmente utilizando Jupyter Notebook/JupyterLab o mediante **Google Colab**.

### Opción 1 — Google Colab

1. Descargar o clonar este repositorio.
2. Abrir Google Colab.
3. Seleccionar **File → Open notebook**.
4. Elegir la pestaña **GitHub**.
5. Introducir la URL del repositorio.
6. Seleccionar el notebook del proyecto.
7. Asegurarse de que los archivos CSV estén disponibles en el entorno.
8. Ejecutar las celdas en orden desde el inicio.

### Opción 2 — Ejecución local

Clonar el repositorio:

    git clone <URL_DEL_REPOSITORIO>

Acceder a la carpeta:

    cd <NOMBRE_DEL_REPOSITORIO>

Instalar las dependencias necesarias:

    pip install pandas seaborn matplotlib jupyter

Abrir Jupyter Notebook:

    jupyter notebook

Finalmente, abrir el archivo `.ipynb` y ejecutar las celdas en orden.

---

## 🔄 Guía de reproducción

Para reproducir correctamente el análisis:

1. Cargar `plans.csv`, `users_latam.csv` y `usage.csv`.
2. Ejecutar la exploración inicial de los datasets.
3. Identificar valores nulos, sentinels y fechas inválidas.
4. Aplicar las transformaciones y limpieza documentadas en el notebook.
5. Agregar las métricas de uso por `user_id`.
6. Combinar las métricas con la información de clientes.
7. Ejecutar el análisis estadístico y las visualizaciones.
8. Detectar outliers mediante IQR.
9. Crear las segmentaciones por edad y nivel de uso.
10. Revisar los insights y conclusiones obtenidos.

> **Importante:** ejecutar las celdas en el orden definido en el notebook, ya que varias transformaciones dependen de resultados generados previamente.

---

## 📈 Conclusión

El proyecto demuestra un flujo completo de **Data Analytics**, desde la exploración y limpieza de datos hasta la construcción de segmentos de clientes y generación de recomendaciones de negocio.

La segmentación obtenida permite transformar información transaccional y demográfica en perfiles accionables que pueden utilizarse como base para estrategias de **retención, migración de planes, optimización de productos y crecimiento comercial**.

---

## 👤 Autor

**Marcela Trejo Huerta**

Data Analytics | Data Science | Business Analytics | PMO & Business Transformation

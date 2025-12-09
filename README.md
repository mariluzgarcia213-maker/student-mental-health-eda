#  Student Mental Health Survey – EDA y Visualización

##  1. Descripción del Dataset

El dataset **Student Mental Health Survey (2024)** recopila información sobre la salud mental de estudiantes universitarios, incluyendo:

- **Bienestar emocional:** ansiedad, depresión, aislamiento, inseguridad frente al futuro.  
- **Factores académicos:** carga de trabajo, presión académica, satisfacción con los estudios.  
- **Hábitos personales:** horas de sueño, actividad deportiva.  
- **Contexto social:** relaciones sociales, presencia o ausencia de discriminación en el campus.  
- **Datos generales:** edad, género, rendimiento académico (CGPA).

El objetivo principal es identificar **qué factores influyen en la salud mental** de los estudiantes y analizar posibles patrones de riesgo.


## Dimensiones del Dataset y Detalles Técnicos

El dataset Student Mental Health Survey contiene un total de 87 filas (estudiantes encuestados) y 21 columnas (variables medidas).
Estas variables incluyen factores emocionales, académicos, sociales y hábitos personales, lo que permite un análisis integral del bienestar estudiantil.

### Dimensiones

Filas: 87 estudiantes

Columnas: 21 variables

### Tipos de datos

El dataset incluye tres tipos principales de datos:

Numéricos (integer / numeric):
Como age, depression, anxiety, academic_workload, academic_pressure, etc.
Se usan para análisis estadísticos, rangos y visualizaciones cuantitativas.

Categóricos (character):
Como gender, average_sleep, sports_engagement, residential_status, etc.
Estas variables representan categorías o grupos.

Factores (factor):
En R, los factores se utilizan para manejar datos categóricos de forma estructurada.

 ¿Por qué se convirtieron algunas columnas de tipo character a factor en R?

Durante el EDA se detectó que varias columnas estaban en formato character, pero realmente representan categorías fijas (ej.: “Male”, “Female”, “2–4 hrs”, “4–6 hrs”, “7–8 hrs”…).

Transformarlas a factor es importante porque:

 Permite un manejo estadístico correcto
R trata los factor levels como categorías y no como texto libre, lo que evita errores en cálculos o gráficos.

 Optimiza las visualizaciones
Librerías como ggplot2 funcionan mejor cuando las variables categóricas son factor, especialmente en:

gráficos de barras,

gráficos de violín,

gráficos de pastel o donut.

 Permite ordenar niveles
Por ejemplo, las horas de sueño pueden ordenarse:
very_low_sleep < low_sleep < normal_sleep

 Reduce errores en modelos posteriores
Si se usa Machine Learning, los factores se codifican correctamente como variables categóricas.

 Columna Objetivo (Target) del Proyecto

Aunque este proyecto se centra en EDA + Visualización, la variable que tiene mayor importancia analítica y podría considerarse target para estudios posteriores es:

 Depression

Escala de 1 a 5 que mide el nivel de depresión del estudiante.

Es la variable más relevante porque:

está directamente relacionada con la salud mental,

permite buscar factores predictivos (sueño, deporte, presión académica…),

sirve para identificar patrones de riesgo en la población estudiantil.
---

##  2. ¿Qué se realizó en este proyecto?

Este proyecto incluye un **análisis exploratorio de datos (EDA)** completo usando **R dentro de Google Colab**, integrando librerías como `ggplot2`, `patchwork` y `dplyr`.

Las tareas realizadas fueron:

###  Importación del dataset desde Kaggle  
Usando Kaggle API dentro de Colab.

###  Limpieza y preparación  
- Conversión de variables categóricas a *factor*.  
- Revisión de valores faltantes y duplicados.  
- Exploración de rangos numéricos y valores únicos.

###  Análisis Exploratorio (EDA)  
- Histogramas de ansiedad, depresión y edad.  
- Tablas de frecuencia para entender categorías.  
- Creación de un dataset reducido con las variables más relevantes.

###  Feature Engineering  
Se crearon nuevas variables útiles para análisis:

- `sleep_group` → Agrupa horas de sueño (very_low_sleep, low_sleep, normal_sleep)  
- `sports_binary` → deporte vs no_deporte  
- `high_depression` → depresión alta (4–5) frente a baja/media  
- Eliminación de columnas irrelevantes para salud mental  

###  Visualizaciones  
Se generaron **5 gráficos representativos** con análisis detallado (ver sección 4).

---

##  3. Estructura del Proyecto

El repositorio debe quedar estructurado de esta manera:

```
📦 student-mental-health-eda
│
├──  README.md
├──  Dataset.ipynb                 # Notebook con análisis EDA
├──  MentalHealthSurvey.csv        # Dataset original usado en Kaggle
│
├──  images                        # Carpeta con gráficas generadas
│     ├── donut_presion_academica.png
│     ├── boxplot_depresion_carga.png
│     ├── heatmap_presion_ansiedad.png
│     ├── barras_discriminacion.png
│     ├── histogramas_emocionales.png  
```

### Importante:
Debes subir **kaggle.json** dentro de la carpeta `sample_data/` en Google Colab para poder descargar datasets desde Kaggle.  

Esto se hace desde:

```
Files → sample_data → Upload → kaggle.json
```

---

##  4. Cómo ejecutar el proyecto desde Google Colab

1. Abrir el notebook `Dataset.ipynb` en Colab.
2. Subir el archivo `kaggle.json` dentro de **sample_data**.
3. Ejecutar todas las celdas en orden:
   - instalación de R y rpy2  
   - instalación de Kaggle API  
   - descarga del dataset  
   - procesamiento, EDA y visualización  

Este proyecto usa código R dentro de Colab gracias al comando:

```python
%load_ext rpy2.ipython
```

Y las celdas R con:

```python
%%R
```

---

##  5. Gráficas más representativas (con análisis)

### **1️ Gráfico DONUT – Distribución de la presión académica**

![Gráfico DONUT – Presión Académica](images/donut_presion_academica.png)

**Análisis:**  
La mayor proporción de estudiantes se encuentra en niveles **alto (4)** y **muy alto (5)** de presión académica. Los niveles 1 y 2 representan una parte pequeña.  
Esto evidencia que la mayoría de los estudiantes experimentan **cargas académicas elevadas**.

---

### **2️ Boxplot – Depresión según carga académica**

![Boxplot Depresión vs Carga Académica](images/boxplot_depresion_carga.png)

**Análisis:**  
A medida que aumenta la carga académica, también aumentan las puntuaciones de depresión.  
La variabilidad es baja cuando la carga es mínima, pero se vuelve amplia cuando la carga es alta, lo que indica **inestabilidad emocional asociada a exigencias académicas fuertes**.

---

### **3️  Mapa de calor – Presión académica vs ansiedad**

![Mapa de calor](images/heatmap_presion_ansiedad.png)

**Análisis:**  
Las combinaciones de presión **4–5** con ansiedad **4–5** son las más frecuentes (zonas más oscuras).  
Esto indica una **correlación directa entre presión académica y ansiedad**.

---
### **4 Grafico de Barras – Discriminación**

**Archivo:** `barras_discriminacion.png`

![Discriminación](images/barras_discriminacion.png)


**Análisis:**  
Aunque la mayoría reporta **no** haber sufrido discriminación, existe un grupo significativo que sí lo ha experimentado.  
Este tipo de experiencias están asociadas con mayor ansiedad y menor satisfacción académica.

---

### **5 Histogramas de edad, ansiedad y depresión**

**Archivo:** `histogramas.png`
![Histogramas](images/histogramas_emocionales.png)


**Análisis:**  
- La mayoría de los estudiantes tiene entre **18 y 22 años**.  
- La ansiedad se distribuye de manera amplia, con picos en niveles 3–4.  
- La depresión muestra un patrón similar, sugiriendo una tendencia generalizada a **niveles moderados-altos de estrés emocional**.

---

##  6. Conclusiones principales

- La presión y la carga académica muestran **relación directa** con ansiedad y depresión.  
- El sueño insuficiente y la falta de deporte agravan los factores de riesgo emocional.  
- La discriminación, aunque menos frecuente, tiene un fuerte impacto negativo.  
- Las relaciones sociales funcionan como **factor protector**, reduciendo los niveles de ansiedad.  

Este análisis permite identificar patrones clave para intervenciones y estrategias de bienestar estudiantil.

---

##  7. Autor

Proyecto desarrollado por **Mariluz García Vera**  
EDA realizado con **R + Python (rpy2)** en Google Colab.


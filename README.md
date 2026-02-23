# 🔍 Material DT-1: Detección de Anomalías en Estudiantes del Semillero Mamba

<!-- badges -->
![Python](https://img.shields.io/badge/Python-3.8+-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

---

## 📋 Descripción General

Este repositorio contiene un análisis completo e integral de **detección de anomalías** en estudiantes del **Semillero Mamba** de la institución **JAQC**. El proyecto utiliza técnicas avanzadas de **Machine Learning no supervisado** para identificar patrones inusuales, inconsistencias y perfiles de riesgo en estudiantes, con el objetivo de proporcionar intervenciones pedagógicas personalizadas.

### 🎯 Objetivo Principal
Identificar estudiantes con patrones de comportamiento **anómalos e inconsistentes** que requieran intervención especial, considerando dimensiones académicas, psicológicas, socioeconómicas y personales.

---

## 📁 Estructura del Repositorio

```
material-DT-1/
│
├── 📄 README.md                     (Este archivo - Inicio del proyecto)
│
├── 📂 Análisis Nuevo/
│   ├── 📂 Ana-1/                    (Proyecto Principal - Análisis Detallado)
│   │   ├── README.md                (Hoja de ruta metodológica completa)
│   │   ├── 01_EDA_Inicial.ipynb     (Análisis exploratorio inicial)
│   │   ├── 02_Preparacion_Features.ipynb (Feature engineering)
│   │   ├── 03_Modelado_Anomalias.ipynb (Modelos de detección)
│   │   ├── 04_Validacion_Analisis.ipynb (Validación y consenso)
│   │   └── 05_Interpretacion_Resultados.ipynb (Resultados finales)
│   │
│   └── 📂 data/
│       └── RespuestasSemillero_completo.json (Datos sin procesar)
│
└── 📂 Análisis Previo/              (Análisis anteriores y experimentación)
    ├── Analisis_Definitivo_Clustering.ipynb
    ├── complete_pipeline_with_shap_explainability.ipynb
    ├── complete_pipeline_with_shap_explainabilityV2.ipynb
    ├── complete_self_contained_pipeline.ipynb
    ├── definitive_clustering_analysis.ipynb
    ├── eda_and_comparative_clustering.ipynb
    ├── EDA_y_Clustering_Comparativo.ipynb
    ├── mamba_student_profiles_complete_analysis.ipynb
    ├── Pipeline_Completo_y_Autocontenido.ipynb
    ├── Pipeline_Final_6_Modelos.ipynb
    ├── Pipeline_Final_GridSearch.ipynb
    ├── Pipeline_Final_Resample100.ipynb
    ├── Pipeline_Final_SklearnResample.ipynb
    ├── MAMBA_Student_Profiles_Results.xlsx
    ├── RespuestasSemillero.xlsx
    └── datos.docx
```

---

## 🚀 Inicio Rápido

### Requisitos Previos
- **Python 3.8+**
- **Jupyter Notebook** o **JupyterLab**
- Librerías requeridas (ver `Instalación`)

### Instalación

1. **Clonar el repositorio:**
```bash
git clone https://github.com/jaquimbayoc7/material-DT-1.git
cd material-DT-1
```

2. **Crear entorno virtual (recomendado):**
```bash
python -m venv venv
# Windows
venv\Scripts\activate
# macOS/Linux
source venv/bin/activate
```

3. **Instalar dependencias:**
```bash
pip install jupyter pandas numpy scikit-learn matplotlib seaborn plotly scipy
```

4. **Navegar al proyecto principal:**
```bash
cd "Análisis Nuevo/Ana-1"
jupyter notebook
```

---

## 📊 Datos

### Fuente
- **Archivo:** `RespuestasSemillero_completo.json`
- **Ubicación:** `Análisis Nuevo/data/`
- **Descripción:** Respuestas completas de estudiantes del Semillero Mamba a un cuestionario multidimensional

### Variables Principales (35 en total)

#### 📚 **Académicas**
- `Q3` - Responsabilidad profesional (1-5)
- `Q6` - Gusto por programación (1-5)
- `Q7` - Horas/día estudiando
- `Q8` - Horas/semana practicando programación
- `Q9` - Días previos al examen que estudia
- `Q33, Q34, Q35` - Calificaciones en cursos de programación

#### 🧠 **Cognitivas & Psicológicas**
- `Q4` - Aptitudes para investigación (0-1)
- `Q5` - Percepción de inteligencia (1-3)
- `Q17` - Impacto del estrés (1-4)
- `Q18` - Reactividad al estrés (1-5)
- `Q19` - Empatía con compañeros (1-4)

#### 💰 **Socioeconómicas**
- `Q11-Q14` - Composición familiar
- `Q15, Q16` - Educación de padres (1-5)
- `Q20` - Horas de trabajo/semana (0-50)
- `Q21` - Apoyo financiero (0-1)
- `Q32` - Estrato socioeconómico (1-6)

#### 🎓 **Personales & Motivacionales**
- `Q1` - Género (0-1)
- `Q2` - Edad
- `Q22` - Relación romántica (0-1)
- `Q23` - Preferencia de carrera (0-4)
- `Q24` - Cambiaría de carrera (0-1)
- `Q25` - Interés en posgrado (0-1)
- `Q28` - Semestre actual
- `Q29` - Edad de ingreso a la carrera
- `Q30, Q31` - Motivación e intereses (texto)

---

## 🔬 Metodología

### 4 Tipos de Anomalías Detectadas

| Tipo | Descripción | Ejemplos |
|------|-------------|----------|
| **Inconsistencias Académicas** | Desajuste entre aptitudes y desempeño | Alto desempeño pero responsabilidad baja |
| **Desbalance Vida Académica** | Conflicto entre trabajo y estudio | Alto trabajo + poco estudio |
| **Desajustes Psicológicos** | Desconexión emocional o motivacional | Estrés extremo + baja empatía |
| **Patrones Inusuales** | Combinaciones raras de variables | Edad extrema para el semestre |

### Modelos de Machine Learning

#### 1. **Isolation Forest** ⭐ (RECOMENDADO)
- Detecta outliers en múltiples dimensiones
- Rápido y eficiente
- Interpretable
- Parámetro: `contamination` (% anomalías esperadas)

#### 2. **Local Outlier Factor (LOF)**
- Detecta anomalías contextuales relativas a vecinos
- Captura "rareza local"
- Parámetro: `n_neighbors` (20-30)

#### 3. **One-Class SVM**
- Aprende frontera del comportamiento normal
- Kernel RBF para relaciones complejas
- Más restrictivo

#### 4. **Autoencoder** (opcional)
- Redes neuronales para captura de patrones complejos
- Error de reconstrucción como métrica de anomalía
- Máxima sofisticación

---

## 📈 Flujo de Trabajo Principal

El proyecto **Ana-1** sigue una estructura de 6 fases:

```
FASE 1: EXPLORACIÓN (EDA Inicial)
├─ Importar librerías y cargar datos
├─ Exploración y descriptivos
├─ Análisis de correlaciones
└─ Identificar variables clave

FASE 2: PREPARACIÓN (Feature Engineering)
├─ Crear features derivadas
├─ Normalización Z-score
└─ Manejo de datos faltantes

FASE 3: MODELADO (Implementar Algoritmos)
├─ Isolation Forest
├─ Local Outlier Factor (LOF)
├─ One-Class SVM
└─ Autoencoder (opcional)

FASE 4: VALIDACIÓN (Consenso y Análisis)
├─ Consenso entre modelos
└─ Análisis de sensibilidad

FASE 5: ANÁLISIS DETALLADO (Interpretación)
├─ Visualización 2D (PCA/TSNE)
├─ Análisis de cada anomalía
├─ Clasificación de tipos
└─ Matriz de decisión

FASE 6: SÍNTESIS (Conclusiones)
├─ Visualizaciones finales
└─ Conclusiones y recomendaciones
```

---

## 📁 Cómo Usar Este Repositorio

### Para Análisis Principal
1. Navega a `Análisis Nuevo/Ana-1/`
2. Lee el [README.md](Análisis%20Nuevo/Ana-1/README.md) para la metodología completa
3. Ejecuta los notebooks en orden:
   - `01_EDA_Inicial.ipynb` - Exploración inicial
   - `02_Preparacion_Features.ipynb` - Feature engineering
   - `03_Modelado_Anomalias.ipynb` - Entrenar modelos
   - `04_Validacion_Analisis.ipynb` - Validar resultados
   - `05_Interpretacion_Resultados.ipynb` - Interpretar anomalías

### Para Análisis Anteriores
- Carpeta `Análisis Previo/` contiene experimentos anteriores con:
  - Clustering comparativo
  - Pipelines con múltiples modelos
  - Análisis con explicabilidad SHAP
  - Búsqueda de hiperparámetros con GridSearch

---

## 🧪 Herramientas y Librerías

### Core de Data Science
```python
pandas          # Manipulación de datos
numpy           # Cálculos numéricos
scikit-learn    # Machine Learning
```

### Visualización
```python
matplotlib      # Gráficos básicos
seaborn         # Visualización estadística
plotly          # Visualización interactiva
```

### Explicabilidad (Opcional)
```python
shap            # SHAP values para interpretabilidad
tensorflow      # Para Autoencoder (opcional)
```

---

## 📊 Resultados Esperados

- **Porcentaje de Anomalías:** 5-20% del semillero (ajustable)
- **Visualizaciones:** 
  - Scatter 2D con anomalías superpuestas
  - Heatmaps de distancia a "normalidad"
  - Radar charts comparativos
  - Dendrogramas de perfiles similares
  - Top variables por anomalía

---

## 🎯 Aplicaciones Pedagógicas

✅ **Intervención Temprana** - Identificar estudiantes en riesgo  
✅ **Mentoría Personalizada** - Diseñar estrategias específicas  
✅ **Retención** - Reducir deserción mediante apoyo  
✅ **Investigación** - Entender factores de anomalía  
✅ **Replicabilidad** - Metodología aplicable a otros contextos  

---

## 📖 Documentación Adicional

| Archivo | Propósito |
|---------|-----------|
| [Ana-1/README.md](Análisis%20Nuevo/Ana-1/README.md) | Hoja de ruta metodológica detallada |
| Notebooks | Código ejecutable con análisis paso a paso |
| JSON/XLSX | Datos sin procesar y resultados |

---

## 🤝 Contribuciones

Este es un proyecto del **Semillero Mamba** para análisis de estudiantes. Contribuciones y mejoras son bienvenidas.

### Cambios Sugeridos
- Agregar nuevos modelos de detección
- Mejorar visualizaciones
- Expandir a otros semesters o cohortes
- Integrar con sistemas de tutoría

---

## 📝 Licencia

Este proyecto está bajo licencia MIT. Ver archivo LICENSE para más detalles.

---

## 📞 Contacto

- **Institución:** JAQC
- **Semillero:** Mamba
- **Repositorio:** https://github.com/jaquimbayoc7/material-DT-1
- **Última Actualización:** 23 de febrero de 2026

---

## 🎓 Referencias

### Conceptos Clave
- **Anomaly Detection** - Detección de anomalías
- **Unsupervised Learning** - Aprendizaje no supervisado
- **Outlier Detection** - Detección de valores atípicos
- **Feature Engineering** - Ingeniería de características
- **Dimensionality Reduction** - Reducción de dimensionalidad

### Recursos Recomendados
- scikit-learn documentation: https://scikit-learn.org/
- Isolation Forest paper: Liu et al. (2008)
- SHAP documentation: https://shap.readthedocs.io/

---

**¿Preguntas o sugerencias?** Abre un issue en GitHub o contacta con el equipo del Semillero Mamba.

**✨ Happy Analyzing!**

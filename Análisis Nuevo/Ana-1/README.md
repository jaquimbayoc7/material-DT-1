# 🔍 Detección de Anomalías en Estudiantes del Semillero Mamba

## 📌 Hoja de Ruta Metodológica Completa

---

## 1. PREGUNTA DE INVESTIGACIÓN

**¿Qué estudiantes del semillero tienen patrones de comportamiento INUSUALES, inconsistentes o potencialmente riesgosos dentro de su contexto académico y socioeconómico?**

### Ejemplos de Anomalías Buscadas:
- Alto estrés + bajo rendimiento académico
- Muy responsable pero calificaciones bajas
- Gran dedicación al estudio pero sin interés en programación
- Trabajo excesivo + estudios simultáneamente
- Altamente inteligente pero poco empático
- Sobre-estimulación académica (muchas horas sin descanso)

---

## 2. HIPÓTESIS PRINCIPAL

Existen estudiantes con perfiles **ANÓMALOS** que requieren intervención pedagógica o apoyo especial, identificables por patrones inconsistentes en sus respuestas multidimensionales.

---

## 3. VARIABLES A UTILIZAR (Todas las 35 Variables)

### 📊 ENFOQUE: Multidimensional (sin una sola variable objetivo)

#### A) VARIABLES ACADÉMICAS
- `Q3` - Responsabilidad profesional (1-5)
- `Q6` - Gusto por programación (1-5)
- `Q7` - Horas/día estudiando
- `Q8` - Horas/semana practicando programación
- `Q9` - Días previos al examen que estudia
- `Q33, Q34, Q35` - Calificaciones en cursos de programación

#### B) VARIABLES COGNITIVAS & PSICOLÓGICAS
- `Q4` - Aptitudes para investigación (0-1)
- `Q5` - Percepción de inteligencia (1-3)
- `Q17` - Impacto del estrés (1-4)
- `Q18` - Reactividad al estrés (1-5)
- `Q19` - Empatía con compañeros (1-4)

#### C) VARIABLES SOCIOECONÓMICAS
- `Q11, Q12, Q13, Q14` - Composición familiar
- `Q15, Q16` - Educación de padres (1-5)
- `Q20` - Horas de trabajo/semana (0-50)
- `Q21` - Apoyo financiero (0-1)
- `Q32` - Estrato socioeconómico (1-6)

#### D) VARIABLES PERSONALES & MOTIVACIONALES
- `Q1` - Género (0-1)
- `Q2` - Edad
- `Q22` - Relación romántica (0-1)
- `Q23` - Preferencia de carrera (0-4)
- `Q24` - Cambiaría de carrera (0-1)
- `Q25` - Interés en posgrado (0-1)
- `Q28` - Semestre actual
- `Q29` - Edad de ingreso a la carrera
- `Q30` - Motivación para investigación (texto)
- `Q31` - Campo importante para desempeño (texto)

---

## 4. TIPOS DE ANOMALÍAS A DETECTAR

### TIPO 1: INCONSISTENCIAS ACADÉMICAS
- Alto desempeño (Q33-35) pero responsabilidad media/baja
- Bajo desempeño pero muy responsable (Q3=5)
- Muchas horas estudio pero poco gusto por programación
- Muy inteligente (Q5) pero malas notas
- Aptitud investigación alta pero bajo rendimiento

### TIPO 2: DESBALANCE VIDA ACADÉMICA
- Alto trabajo (Q20) + pocas horas estudio (Q7)
- Sin apoyo financiero + trabajo máximo
- Sobrecarga: trabajo + estudio + responsabilidades familiares
- Edad muy avanzada/joven para el semestre actual
- Múltiples compromisos sin dedicación equilibrada

### TIPO 3: DESAJUSTES PSICOLÓGICOS
- Muy responsable pero bajo interés en carrera (Q23<2)
- Estrés extremo (Q17-18 máximo) con baja empatía (Q19)
- En relación romántica + estrato bajo + trabajo máximo
- Muy responsable pero cambiaría de carrera (Q24=0)
- Quiere investigar pero sin aptitudes (Q4=0, Q30 importante)

### TIPO 4: PATRONES INUSUALES
- Combinaciones raras de edad + semestre
- Educación parental máxima pero bajo apoyo económico
- Familia numerosa sin trabajadores (Q12 bajo)
- Extremos en una variable (máximo trabajo, máximo estrés, etc)
- Decisiones contradictorias (cambiar carrera pero quiere posgrado)

---

## 5. METODOLOGÍA ESTADÍSTICA

### 5.1 PREPARACIÓN DE DATOS
- Normalización Z-score (media=0, std=1)
- Codificación de variables categóricas (Q10, Q30, Q31)
- Imputación de missing values
- Creación de features derivadas (ratios, sumas, etc)

### 5.2 FEATURE ENGINEERING
- `Carga académica` = Q7 + Q8 + Q9
- `Balance vida` = (Q20 / (Q7 + Q8 + Q9 + 1))
- `Estrés psicológico` = (Q17 + Q18) / 2
- `Apoyo familiar` = Q12 + Q13
- `Consistencia notas` = std(Q33, Q34, Q35)
- `Desempeño promedio` = (Q33 + Q34 + Q35) / 3
- `Índice responsabilidad-resultado` = Q3 / (desempeño + 1)

### 5.3 MODELOS DE DETECCIÓN DE ANOMALÍAS

#### MODELO 1: ISOLATION FOREST
- ⭐ **RECOMENDADO** - Mejor relación interpretabilidad-precisión
- Baseline rápido y eficiente
- No requiere asumir distribuciones
- Detecta outliers en múltiples dimensiones
- Parámetro: `contamination` (% anomalías esperadas)

#### MODELO 2: LOCAL OUTLIER FACTOR (LOF)
- Detecta anomalías locales (relativas a vecinos)
- Útil para clusters con densidades diferentes
- Captura estudiantes "raros" en su grupo
- Parámetro: `n_neighbors` (20-30 típico)
- Revela anomalías contextuales

#### MODELO 3: ONE-CLASS SVM
- Aprende frontera del comportamiento "normal"
- Detecta lo que NO es normal
- Requiere tuning de hiperparámetros
- Kernel RBF para relaciones complejas
- Más restrictivo que Isolation Forest

#### MODELO 4: AUTOENCODER (NEURAL NETWORK)
- Detecta anomalías por error de reconstrucción
- Captura patrones complejos y no lineales
- Recomprimiendo datos a dimensión menor
- Requiere suficientes datos de entrenamiento
- Máxima sofisticación pero más "caja negra"

### 5.4 VALIDACIÓN Y CALIBRACIÓN
- No hay etiquetas "verdaderas" (unsupervised)
- Usar consenso entre modelos
- Validación manual por expertos (docentes)
- Análisis de sensibilidad de parámetros
- Interpretabilidad de cada anomalía detectada

---

## 6. ANÁLISIS E INTERPRETACIÓN

### 6.1 PERFILES DE ANOMALÍAS
Para cada estudiante anómalo cuantificar:
- Score de anomalía (0-1)
- Tipo(s) de anomalía (académica, balance, psicológica, etc)
- Variables más contribuyentes a su anomalía
- Comparación con "promedio" del semillero
- Recomendaciones pedagógicas específicas

### 6.2 AGRUPACIÓN DE ANOMALÍAS
- ¿Hay clusters de anomalías similares?
- ¿Qué tienen en común?
- ¿Son remediables o inherentes?
- ¿Cuál es la acción recomendada para cada tipo?

### 6.3 FACTORES EXPLICATIVOS
- ¿Qué variables causan cada anomalía?
- ¿Son socioeconómicas, psicológicas o académicas?
- ¿Hay factores modificables (estudio) vs fijos (familia)?
- ¿Qué intervenciones podrían normalizarlos?

---

## 7. RESULTADOS ESPERADOS

### Porcentaje de Anomalías: 5-20% del semillero
(Ajustable según parámetro `contamination`)

### Ejemplos de Anomalías Probables:
✓ Estudiante: Responsable (5) + bajo gusto programación (1) + buenas notas  
✓ Estudiante: Trabaja 40h/semana + estudia 3h/día + estrato bajo  
✓ Estudiante: Estrés máximo (5) + inteligencia máxima (3) pero inconsistente  
✓ Estudiante: Edad 18, semestre 1 (normal) pero perfil muy diferente  
✓ Estudiante: Padres universidad + estrato 1 (extremo socioeconómico)  

---

## 8. VISUALIZACIONES CLAVE

- Scatter 2D (PCA o TSNE) mostrando anomalías en el espacio reducido
- Heatmaps mostrando distancia a "normalidad"
- Box plots de variables para anomalías vs estudiantes normales
- Radar charts comparando anomalías vs promedio del semillero
- Matriz de características más influyentes
- Dendrograma de perfiles anómalos similares
- Top 10 variables para cada anomalía detectada

---

## 9. MATRIZ DE DECISIÓN (PARA CADA ANOMALÍA)

| Tipo Anomalía | Riesgo Académico | Acción Recomendada |
|--|--|--|
| **Balance vida** | ALTO | Tutería, reducir trabajo |
| **Psicológica** | MUY ALTO | Psicólogo + tutor |
| **Inconsistencia** | MEDIO | Revisión de motivaciones |
| **Sobre-estimulado** | ALTO | Aprender a priorizar |
| **Sub-estimulado** | BAJO | Aumentar desafíos |

---

## 10. CONCLUSIONES & RECOMENDACIONES

### Para el SEMILLERO:
- Identificar estudiantes que necesitan intervención temprana
- Crear programas de mentoría personalizados
- Detectar talentos ocultos con desempeño bajo

### Para DOCENTES:
- Detectar perfiles especiales con estrategias personalizadas
- Entender causas raíz del bajo rendimiento
- Intervenir antes de que los estudiantes deserten

### Para ORIENTACIÓN ESTUDIANTIL:
- Derivar casos de riesgo a apoyo psicológico/económico
- Identificar necesidades reales de cada estudiante
- Implementar planes de retención

### Para INVESTIGACIÓN:
- ¿Qué factores hacen que un estudiante sea "anómalo"?
- ¿Pueden normalizarse o hay factores estructurales?
- ¿Hay patrones regionales o demográficos en las anomalías?

---

## 📊 FLUJO DE TRABAJO EN EL PROYECTO

```
FASE 1: EXPLORACIÓN (EDA Inicial)
├─ Celda 1: Importar librerías y cargar datos
├─ Celda 2: EDA - Exploración y descriptivos
├─ Celda 3: Análisis de correlaciones
└─ Celda 4: Identificar variables clave

FASE 2: PREPARACIÓN (Feature Engineering)
├─ Celda 5: Crear features derivadas
├─ Celda 6: Normalización Z-score
└─ Celda 7: Manejo de datos faltantes

FASE 3: MODELADO (Implementar Algoritmos)
├─ Celda 8: Modelo 1 - Isolation Forest
├─ Celda 9: Modelo 2 - Local Outlier Factor (LOF)
├─ Celda 10: Modelo 3 - One-Class SVM
└─ Celda 11: Modelo 4 - Autoencoder (opcional)

FASE 4: VALIDACIÓN (Consenso y Análisis)
├─ Celda 12: Consenso entre modelos
└─ Celda 13: Análisis de sensibilidad

FASE 5: ANÁLISIS DETALLADO (Interpretación)
├─ Celda 14: Visualización 2D (PCA/TSNE)
├─ Celda 15: Análisis de cada anomalía
├─ Celda 16: Clasificación de tipos
└─ Celda 17: Matriz de decisión

FASE 6: SÍNTESIS (Conclusiones)
├─ Celda 18: Visualizaciones finales
└─ Celda 19: Conclusiones y recomendaciones
```

---

## 🎯 VENTAJAS PEDAGÓGICAS

✅ **Detección de casos reales** - Practicidad inmediata  
✅ **Múltiples técnicas ML** - Aprender métodos unsupervised  
✅ **Interpretabilidad alta** - Cada anomalía se puede explicar  
✅ **Impacto académico directo** - Ayudar a estudiantes reales  
✅ **Aplicable a otros contextos** - Fraude, fallas en equipos, etc  
✅ **Combina dominio + técnica** - Necesita entender datos + algoritmos  

---

## 📁 ARCHIVOS DEL PROYECTO

```
Ana-1/
├── README.md (este archivo)
├── 01_EDA_Inicial.ipynb (Análisis exploratorio inicial)
├── 02_Preparacion_Features.ipynb (Feature engineering)
├── 03_Modelado_Anomalias.ipynb (Implementación de modelos)
├── 04_Validacion_Analisis.ipynb (Validación y análisis)
└── 05_Interpretacion_Resultados.ipynb (Resultados finales)
```

---

## 📚 REFERENCIAS Y RECURSOS

### Librerías Python Utilizadas
- **pandas** - Manipulación de datos
- **numpy** - Cálculos numéricos
- **scikit-learn** - Machine Learning
  - `IsolationForest` - Detección de anomalías
  - `LocalOutlierFactor` - LOF
  - `OneClassSVM` - SVM de una clase
  - `StandardScaler` - Normalización
- **matplotlib** - Visualización básica
- **seaborn** - Visualización estadística
- **plotly** - Visualización interactiva
- **tensorflow/keras** - Autoencoder (opcional)

### Conceptos Clave
- **Anomaly Detection** (Detección de anomalías)
- **Unsupervised Learning** (Aprendizaje no supervisado)
- **Outlier Detection** (Detección de valores atípicos)
- **Feature Engineering** (Ingeniería de características)
- **Dimensionality Reduction** (Reducción de dimensionalidad)

---

**Última actualización:** 20 de febrero de 2026  
**Semillero:** Mamba  
**Institución:** JAQC  
**Instructor:** [Nombre]


# Proyecto APES: Impacto del Gasto Educativo Contratado (SECOP) y del Presupuesto General de la Nación sobre la Calidad Educativa Oficial en Colombia (2019–2025)

**Autor:** Santiago Hurtado Martínez  
**Asignatura:** Aprendizaje Estadístico (APES) — Escuela Colombiana de Ingeniería Julio Garavito  

---

## Descripción General

Este paquete constituye el **entregable autocontenido y 100 % reproducible** del proyecto. Integra los conjuntos de datos depurados, los cuatro cuadernos interactivos de Jupyter (`Notebooks/`), las tablas y visualizaciones de alta resolución (`Outputs/`) y el artículo académico final (`Reportes/12_Trabajo_Escrito_Final_APES.md`).

Todos los cuadernos resuelven dinámicamente sus rutas relativas, por lo que pueden abrirse y re-ejecutarse de principio a fin (`Restart Kernel and Run All`) en cualquier computador y sistema operativo sin depender de rutas absolutas externas.

---

## Estructura del Entregable

```text
Entregable/
├── README.md                                  # Guía de instalación, arquitectura y ejecución
├── requirements.txt                           # Dependencias de Python (Econometría, DuckDB, ML y SHAP)
├── Data/
│   └── divipola_oficial.csv                   # Catálogo oficial DANE DIVIPOLA (1.102 municipios, 33 departamentos)
├── Notebooks/
│   ├── 00_Marco_Hipotesis.ipynb               # Marco teórico, diseño cuasi-experimental y matriz de hipótesis H1–H5
│   ├── 01_Data_Wrangling.ipynb                # Deduplicación SECOP/ICFES, SQL en DuckDB, clasificador A/B/X y ensamblaje de paneles
│   ├── 02_EDA_Descriptivo.ipynb               # Estadísticos, normalidad, descomposición de varianza, VIF within, COVID-19 y mapas de calor
│   └── 03_Modelado_ML_Econometria.ipynb       # 16 modelos PanelOLS/WLS/PD, Wild Cluster Bootstrap, corte 2025, gobernanza y ML + SHAP
├── Outputs/
│   ├── dataset_maestro_departamental_v4.parquet  # Panel maestro departamental (231 filas × 98 columnas)
│   ├── dataset_maestro_municipal_v4.parquet      # Panel maestro municipal (7.714 filas × 45 columnas)
│   ├── secop_depurado_v2.parquet                 # Universo de 353.273 contratos educativos territoriales únicos (2019–2023)
│   ├── icfes_depurado_v2.parquet                 # Serie censal agregada Saber 11 Oficial Calendario A (2.948.410 estudiantes)
│   ├── Tablas/                                   # Tablas de resultados econométricos, reconciliación, VIF, benchmark ML y SHAP (.csv)
│   └── Figuras/                                  # Gráficos generados por los cuadernos en alta resolución (300 DPI, .png)
└── Reportes/
    └── 12_Trabajo_Escrito_Final_APES.md       # Artículo científico final autocontenido del proyecto
```

---

## Inicio Rápido y Reproducibilidad

1. **Instalar dependencias:**
   ```bash
   pip install -r requirements.txt
   ```

2. **Ejecutar los cuadernos:**
   - Abra cualquiera de los cuadernos de la carpeta `Notebooks/` en **VS Code**, **JupyterLab** o **Jupyter Notebook**.
   - Todas las celdas ya incluyen sus salidas, tablas y gráficos renderizados.
   - Si desea re-ejecutar todo el flujo en vivo, seleccione **`Restart Kernel and Run All Cells`** (el tiempo total de ejecución de los 4 cuadernos es de aproximadamente 25 segundos).

---

## Guía de Cuadernos Interactivos

| # | Cuaderno | Contenido Analítico Ejecutado en Vivo |
|:---:|:---|:---|
| **00** | `00_Marco_Hipotesis.ipynb` | Marco institucional de la financiación educativa en Colombia, diseño de identificación cuasi-experimental, matriz de hipótesis ($H_1$–$H_5$) y verificación automática de integridad del entorno entregable. |
| **01** | `01_Data_Wrangling.ipynb` | Serie de deflactores IPC (base $2019=1,0000$), conciliación pre/post deduplicación de SECOP, consultas SQL en vivo con **DuckDB** sobre los $353.273$ contratos educativos territoriales únicos, clasificador semántico jerárquico (Niveles A, B y X) validado contra UNSPSC 2023 ($70,97\\%$ *recall*), armonización censal de $2.948.410$ estudiantes oficiales de Calendario A y ensamblaje en vivo de los paneles maestros departamental ($N=231$) y municipal ($N=7.714$) con pruebas `assert`. |
| **02** | `02_EDA_Descriptivo.ipynb` | Estadísticos descriptivos univariados, pruebas de normalidad (Shapiro-Wilk y Jarque-Bera), gráficos de distribuciones, descomposición formal de varianza (*Between* vs. *Two-Way Within* y volatilidad por tamaño departamental), cálculo en vivo del $\text{VIF}_{\text{within}} < 1,23$, reconstrucción de la trayectoria COVID-19 (2019–2025), mapas de calor de correlaciones en niveles vs. diferencias ($\Delta Y_{it}$), distancia multivariada de Mahalanobis y sesgo espacial de capitales ($68,59\\%$). |
| **03** | `03_Modelado_ML_Econometria.ipynb` | Estimación en vivo de las **16 especificaciones econométricas de panel** (`PanelOLS` TWFE, WLS ponderado por matrícula base $N_{i,2019}^{\text{oficial}}$, Primeras Diferencias, prueba de exogeneidad dinámica de Wooldridge $X_{i,t+1}$, desglose CAPEX vs. Bienestar, percentil 25 y deserción escolar) con **Wild Cluster Bootstrap** ($1.999$ réplicas de Rademacher), corte transversal 2025 ($\Delta R^2 = +0,0099$), modelos de gobernanza contractual, benchmark de Machine Learning fuera de muestra (`Rolling Origin` y `GroupKFold`) con `Ridge`, `ElasticNet`, `RandomForest` y `GradientBoosting`, descomposición **SHAP (`TreeExplainer`)** y robustez municipal ($N=1.094$ municipios). |

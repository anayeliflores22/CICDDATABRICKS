
# ETL CANTIDAD Y ESTADO DE ALUMNOS EN UN INSTITUTO

Arquitectura Medallion en Azure Databricks

Pipeline automatizado de datos para análisis del estado de alumnos por programa y la cantidad de alumnos en la escuela de SALUD con arquitectura de tres capas y despliegue continuo.
## 🎯 Descripción

Pipeline ETL que transforma datos crudos de matricula, programa y ciclos académicos de un Instituto, implementando la Arquitectura Medallion (Bronze-Silver-Gold) en Azure Databricks con CI/CD completo y Delta Lake para garantizar consistencia ACID.

## ✨ Características Principales

* 🔄 ETL Automatizado - Pipeline completo con despliegue automático via GitHub Actions
* 🏗️ Arquitectura Medallion - Separación clara de capas Bronze → Silver → Gold
* 📊 Modelo Dimensional - Star Schema optimizado para análisis de negocio
* 🚀 CI/CD Integrado - Deploy automático en cada push a master
* 📈 Databricks Dashboards - Visualización
* ⚡ Delta Lake - ACID transactions y time travel capabilities
* 🔔 Monitoreo - Notificaciones automáticas y logs detallados

## 🏛️ Arquitectura

Flujo de Datos

#### 📄 CSV (Raw Data)
    ↓
#### 🥉 Bronze Layer (Ingesta sin transformación)
    ↓
#### 🥈 Silver Layer (Limpieza + Modelo Dimensional)
    ↓
#### 🥇 Gold Layer (Agregaciones de Negocio)
    ↓
#### 📊 BI Dashboards (Visualización)

![Texto descriptivo](Arquitectura.png)


## Capas del Pipeline

![pipeline](pipeline.png)

## 🚀 Instalación y Configuración

### 1️⃣ Clonar el Repositorio

```bash
git clone https://github.com/Enrykiel/databricks_project
cd databricks_project
```

### 2️⃣ Configurar Databricks Token

1. Ir a Databricks Workspace
2. **User Settings** → **Developer** → **Access Tokens**
3. Click en **Generate New Token**
4. Configurar:
   - **Comment**: `GitHub CI/CD`
   - **Lifetime**: `90 days`
5. ⚠️ Copiar y guardar el token

### 3️⃣ Configurar GitHub Secrets

En tu repositorio: **Settings** → **Secrets and variables** → **Actions**

| Secret Name | Valor Ejemplo |
|------------|---------------|
| `DATABRICKS_HOST` | `https://adb-xxxxx.azuredatabricks.net` |
| `DATABRICKS_TOKEN` | `dapi_xxxxxxxxxxxxxxxx` |

### 4️⃣ Verificar Storage Configuration

```python
storage_path = "abfss://raw@storageproject99.dfs.core.windows.net"
```


✅ **¡Configuración completa!**


---

## 💻 Uso

### 🔄 Despliegue Automático (Recomendado)

```bash
git add .
git commit -m "✨ feat: mejoras en pipeline"
git push origin master
```

**GitHub Actions ejecutará**:
- 📤 Deploy de notebooks a `/Workspace/databricks_project/proceso`
- 🔧 Creación del workflow `WF_PROD_ETL_INSTITUTO`
- ▶️ Ejecución completa:  Bronze → Silver → Gold
- 📧 Notificaciones de resultados

### 🖱️ Despliegue Manual desde GitHub

1. Ir al tab **Actions** en GitHub
2. Seleccionar **Deploy ETL Apple Sales And Warranty**
3. Click en **Run workflow**
4. Seleccionar rama `main`
5. Click en **Run workflow**

### 🔧 Ejecución Local en Databricks

Navegar a `/Workspace/databricks_project/proceso` y ejecutar en orden:

```
- 0_preparacion_ambiente.py         → Crear esquema
- 1_ingest_ciclo.py                 → Bronze Layer
- 1_ingest_matricula.py             → Bronze Layer
- 1_ingest_programa.py              → Bronze Layer
- 2_transform_mat_escuela.py        → Silver Layer
- 2_transform_prog_estatus.py       → Silver Layer
- 3_load.py                         → Gold Layer
```

---


## 🔄 CI/CD

### Pipeline de GitHub Actions

```yaml
Workflow: Deploy ETL Apple Sales And Warranty
├── Deploy notebooks → /Workspace/databricks_project/proceso
├── Eliminar workflow antiguo (si existe)
├── Buscar cluster configurado
├── Crear nuevo workflow con 4 tareas
├── Ejecutar pipeline automáticamente
└── Monitorear y notificar resultados
```

### 🔄  Workflow Databricks
![Texto descriptivo](evidencias/WF_PROD_ETL_INSTITUTO.png)



⏰ Schedule: Diario 8:00 AM (Lima)
⏱️ Timeout total: 4 horas
🔒 Max concurrent runs: 1


## 📈 Dashboards
https://github.com/Enrykiel/databricks_project/tree/main/dashboard

## 🔍 Monitoreo

### En Databricks

**Workflows**:
- Ir a **Workflows** en el menú lateral
- Buscar `WF_PROD_ETF_INSTITUTO`
- Ver historial de ejecuciones

**Logs por Tarea**:
- Click en una ejecución específica
- Click en cada tarea para ver logs detallados
- Revisar stdout/stderr en caso de errores

### En GitHub Actions

- Tab **Actions** del repositorio
- Ver historial de workflows
- Click en ejecución específica para detalles
- Revisar logs de cada step

---

## 👤 Autor


### Luis Enrique Cardoso Tineo

[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Enrykiel)
[![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:isc.luiss88000@gmail.com)

**Data Engineering** | **Azure Databricks** | **Delta Lake** | **CI/CD**


---

## 📄 Licencia

Este proyecto está bajo la Licencia MIT - ver el archivo [LICENSE](LICENSE) para más detalles.

---


**Proyecto**: Data Engineering - Arquitectura Medallion  
**Tecnología**: Azure Databricks + Delta Lake + CI/CD  
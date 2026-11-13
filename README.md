# OpenData-ETL
Desarrollo de un sistema que obtenga datos públicos de fuentes seleccionadas, los valide, transforme y almacene de manera reproducible. Permitirá a investigadores reutilizar información integrada sin repetir manualmente los mismos procesos de descarga y limpieza

# Guía de instalación – Tecnologías sugeridas

**Tecnologías sugeridas:** Python, Pandas, Requests, PostgreSQL, SQLAlchemy, FastAPI, Streamlit y GitHub.

Esta guía indica **en qué orden instalar** cada tecnología, **dónde descargar** los programas que no vienen con el sistema y **qué comandos copiar y pegar** para las librerías de Python.

---

## 1. Resumen: orden de instalación

| Orden | Tecnología | Tipo | ¿Se descarga aparte? |
|:---:|---|---|---|
| 1 | Git y cuenta de GitHub | Programa + servicio web | Sí |
| 2 | Python 3.12 | Programa | Sí |
| 3 | PostgreSQL | Programa (base de datos) | Sí |
| 4 | Entorno virtual de Python | Herramienta de Python | No (viene con Python) |
| 5 | Pandas | Librería de Python | No (se instala con `pip`) |
| 6 | Requests | Librería de Python | No (se instala con `pip`) |
| 7 | SQLAlchemy + driver de PostgreSQL | Librería de Python | No (se instala con `pip`) |
| 8 | FastAPI + Uvicorn | Librería de Python | No (se instala con `pip`) |
| 9 | Streamlit | Librería de Python | No (se instala con `pip`) |
---

## 2. Programas que se descargan aparte

### 2.1 Git y GitHub

**Git** es el programa que controla las versiones del código. **GitHub** es el sitio web donde se guarda el repositorio.

| Qué | Enlace de descarga o registro |
|---|---|
| Git (Windows, macOS, Linux) | https://git-scm.com/downloads |
| Cuenta de GitHub (gratuita) | https://github.com/signup |
| GitHub Desktop (opcional, interfaz gráfica) | https://desktop.github.com/ |

En Windows, durante la instalación de Git deja las opciones por defecto.

Verificar la instalación:

```bash
git --version
```

Configurar tu identidad (una sola vez):

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu_correo@ejemplo.com"
```

Clonar el repositorio del proyecto (cambia la URL por la de tu repositorio):

```bash
git clone https://github.com/USUARIO/NOMBRE-DEL-REPOSITORIO.git
cd NOMBRE-DEL-REPOSITORIO
```

---

### 2.2 Python 3.12

| Qué | Enlace de descarga |
|---|---|
| Python (todas las plataformas) | https://www.python.org/downloads/ |

**Importante en Windows:** en la primera pantalla del instalador marca la casilla **«Add python.exe to PATH»** antes de pulsar *Install Now*.

Verificar la instalación:

```bash
python --version
pip --version
```

En Linux o macOS, si `python` no funciona, usa `python3` y `pip3` en todos los comandos de esta guía.

---

### 2.3 PostgreSQL

PostgreSQL es la base de datos relacional del proyecto.

| Qué | Enlace de descarga |
|---|---|
| PostgreSQL (página oficial, todas las plataformas) | https://www.postgresql.org/download/ |
| Instalador para Windows (EDB) | https://www.enterprisedb.com/downloads/postgres-postgresql-downloads |

Durante la instalación en Windows:

1. Deja los componentes por defecto (PostgreSQL Server, pgAdmin 4, Command Line Tools).
2. Define una **contraseña** para el usuario `postgres` y **anótala**.
3. Deja el puerto por defecto: `5432`.

Verificar la instalación:

```bash
psql --version
```

Crear la base de datos del proyecto (te pedirá la contraseña de `postgres`):

```bash
psql -U postgres -c "CREATE DATABASE opendata;"
```



---

## 3. Preparar el entorno de Python

Todos los comandos siguientes se ejecutan **dentro de la carpeta del proyecto**.

### Paso 1. Crear el entorno virtual

```bash
python -m venv .venv
```

### Paso 2. Activarlo

**Windows (PowerShell):**

```powershell
.venv\Scripts\Activate.ps1
```

**Windows (CMD):**

```cmd
.venv\Scripts\activate.bat
```

**Linux / macOS:**

```bash
source .venv/bin/activate
```

Si funciona, verás `(.venv)` al inicio de la línea de la terminal.

> Si PowerShell bloquea el script, ejecuta una sola vez:
> ```powershell
> Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
> ```

### Paso 3. Actualizar pip

```bash
python -m pip install --upgrade pip
```

---

## 4. Instalar las librerías de Python

Con el entorno virtual **activado**, copia y pega cada bloque en orden.

### Opción A. Instalar con el archivo `requirements.txt`


```bash
pip install -r requirements.txt
```
>
> En caso de que no funcione intalar una por una con la opcion B
>

### Opción B. Instalar una por una

#### 4.1 Pandas (análisis y tablas de datos)

```bash
pip install "pandas>=2.2,<4.0"
```

#### 4.2 Requests (descarga de datos desde URLs y APIs)

```bash
pip install requests
```

#### 4.3 SQLAlchemy (acceso a la base de datos)

```bash
pip install "SQLAlchemy>=2.0,<3.0"
```

#### 4.4 Driver de PostgreSQL (conecta SQLAlchemy con PostgreSQL)

```bash
pip install "psycopg[binary]>=3.1,<4.0"
```

#### 4.5 FastAPI y Uvicorn (API REST y servidor)

```bash
pip install "fastapi>=0.115,<1.0"
pip install "uvicorn[standard]>=0.30,<1.0"
```

#### 4.6 Streamlit (interfaz web)

```bash
pip install "streamlit>=1.40,<2.0"
```

### 4.7 Verificar que todo quedó instalado

```bash
pip list
```

Deben aparecer: `pandas`, `requests`, `SQLAlchemy`, `psycopg`, `fastapi`, `uvicorn` y `streamlit`.

Comprobación rápida desde Python:

```bash
python -c "import pandas, requests, sqlalchemy, psycopg, fastapi, uvicorn, streamlit; print('Todo instalado correctamente')"
```

### 4.8 Guardar las dependencias del proyecto

Para que otros puedan reproducir tu entorno:

```bash
pip freeze > requirements.txt
```

> `requests` no está en el `requirements.txt` original del proyecto. Si lo vas a usar, instálalo con el comando 4.2 y agrégalo al archivo.

---


## 5. Posibles problemas

| Problema | Solución |
|---|---|
| `python` no se reconoce como comando | Reinstala Python marcando **Add python.exe to PATH**, o usa `py` en Windows |
| `ModuleNotFoundError` | Activa el entorno `.venv` y vuelve a ejecutar `pip install -r requirements.txt` |
| `pip` no se reconoce | Usa `python -m pip install ...` |
| Error al instalar `psycopg` | Usa la forma `psycopg[binary]` con comillas, como en el paso 4.4 |
| `psql` no se reconoce | Agrega la carpeta `bin` de PostgreSQL al PATH, o usa pgAdmin 4 |
| Error de autenticación en PostgreSQL | Revisa la contraseña en `DATABASE_URL` |
| Puerto 8501 ocupado | `streamlit run app.py --server.port 8502` |
| PowerShell no deja activar `.venv` | `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` |


# Catálogo de fuentes

Dos fuentes principales y dos de apoyo, consultadas el 11 de noviembre de 2026.

| Campo   | F1 · INEC   | F2 · SRI                                                                                                                                                                       |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Conjunto de datos | [Estimaciones y Proyecciones de Población, Revisión 2024](https://www.ecuadorencifras.gob.ec/proyecciones-poblacionales/) | [Catastro RUC por provincia](https://www.sri.gob.ec/datasets), archivo de Loja (SRI_RUC_Loja.zip)  |
| Publicador   | Instituto Nacional de Estadística y Censos  | Servicio de Rentas Internas  |
| Qué contiene  | Población por cantón y año, por sexo y edad, ajustada al Censo 2022 con proyecciones hasta el 2050 | Un registro por contribuyente: provincia, cantón, estado, actividad y fechas |
| Licencia    | [CC BY 4.0](https://www.ecuadorencifras.gob.ec/informacion-censal-cantonal/) |  [CC BY 4.0](https://www.ecuadorencifras.gob.ec/informacion-censal-cantonal/) |
| Formato      | Excel (.xlsx) | CSV comprimido en .zip |
| Estructura     | Tabla agregada, ancha  | Registro a registro, larga `nota: separador` "&#124;" |
| Unidad       | Personas  | Contribuyentes (conteo)  |
| Versión           | Revisión 2024, base Censo 2022  | Version 1/11/2026 (Ultimo registro actualizado)    |
| Diccionario       | Dentro del Excel metadas[^1]   | [Diccionario de variables RUC](https://www.sri.gob.ec/o/sri-portlet-biblioteca-alfresco-internet/descargar/a425b664-828d-4ef4-a103-fe689237d25f/SRI_Diccionario_Catastro.xlsx) |
                                                                                                                                       
[^1] sin embargo muestra indicadores y formulas mas no se encontro un diccionario y solo se puede inferir


## Análisis de compatibilidad

Las fuentes son compatibles a nivel de cantón y año. Las diferencias son de formato, de nivel de detalle y de cómo nombran los territorios; todas se resuelven en la transformación.


| Aspecto                       | F1 · INEC                                              | F2 · SRI                                               | Compatible         | Regla de transformación                                                                                    |
| ----------------------------- | ------------------------------------------------------ | ------------------------------------------------------ | ------------------ | ---------------------------------------------------------------------------------------------------------- |
| Formato de archivo            | Excel con títulos, notas y encabezados en varias filas | CSV dentro de un .zip                                  | Con transformación | Descomprimir el .zip; leer el Excel saltando las filas de título y notas                                   |
| Nivel de detalle              | Agregado: un total por cantón                          | Detallado: una fila por contribuyente                  | Con transformación | Contar contribuyentes por cantón (groupby) antes de unir                                                   |
| Forma de la tabla             | Ancha: los años o grupos van en columnas               | Larga: una fila por registro                           | Con transformación | Pasar el Excel a formato largo (melt)                                                                      |
| Identificación del territorio | Código DPA y nombre                                    | Solo nombre de provincia y cantón, en texto            | No directo         | Normalizar nombres (mayúsculas, sin tildes, sin espacios dobles) y mapearlos al código DPA con la tabla A1 |
| Nombres de cantón             | Nombre oficial                                         | Puede variar en tildes, Ñ o abreviaturas               | Con transformación | Tabla de equivalencias para los casos que no crucen; registrarlos como error                               |
| Fecha                         | Año (entero)                                           | Fechas de inicio, suspensión o reinicio de actividades | Con transformación | Convertir a fecha estándar (AAAA-MM-DD) y extraer el año                                                   |
| Corte temporal                | Serie anual                                            | Foto del catastro al día de la descarga                | Parcial            | Cruzar el conteo actual con la población del año actual; los años pasados solo como aproximación           |
| Estado del registro           | No aplica                                              | Activo, suspendido u otros                             | Con transformación | Contar solo contribuyentes activos para el indicador principal                                             |
| Unidad                        | Personas                                               | Contribuyentes                                         | Sí                 | Guardar la unidad por indicador                                                                            |
| Codificación y separador      | Excel, sin problema                                    | Problemas con el separador "&#124;" y fecha no legible            | Por verificar      | Detectar codificación y separador al leer                                                                  |

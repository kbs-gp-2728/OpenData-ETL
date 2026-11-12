# Planificación: OpenData ETL (Semanas 5 a 14)

**Grupo de Investigación KBS · UTPL**


## Resumen por fases

| Fase | Semanas | Objetivo |
|------|---------|----------|
| 1. Planificación y diseño | 5-6 | Fuentes elegidas, repositorio y esquema de BD definidos |
| 2. Extracción y transformación | 7-8 | Pipeline que lee CSV/Excel de dos fuentes y normaliza |
| 3. Persistencia y validación | 9-10 | Carga en PostgreSQL sin duplicados, reglas de validación y bitácora de ejecuciones |
| 4. Acceso y monitoreo | 11-12 | API REST y tablero de monitoreo |
| 5. Cierre | 13-14 | Pruebas, informe experimental y entrega |

## Cronograma detallado

| Sem. | Fechas | Actividades | Entregable |
|------|--------|-------------|------------|
| **5** | 2-8 nov | Descargar y leer la propuesta. Crear repositorio GitHub (estructura de carpetas, README, `.gitignore`, ramas). Subir esta planificación. Repartir roles. | Repositorio creado y planificación subida |
| **6** | 9-15 nov | Seleccionar dos fuentes públicas (CSV/Excel) y verificar licencia, formato, versión y fecha. Explorar los datos y comparar estructuras, columnas y formatos de fecha. Diseñar el esquema relacional (fuentes, ejecuciones, datos, errores, calidad). Preparar el entorno (Python, PostgreSQL, dependencias). | Catálogo de fuentes v1, análisis de compatibilidad entre fuentes, diagrama entidad-relación |
| **7** | 16-22 nov | Implementar el módulo de extracción (descarga y lectura de CSV y Excel con Requests/Pandas). Registrar metadatos de cada fuente. Pruebas con ambas fuentes. | Extractor funcional para las dos fuentes |
| **8** | 23-29 nov | Implementar la transformación: normalizar nombres de columnas, tipos y fechas. Definir el esquema común entre fuentes. Documentar las reglas de transformación. | Módulo de transformación y documento de reglas v1 |
| **9** | 30 nov-6 dic | Crear tablas en PostgreSQL con SQLAlchemy. Implementar la carga con control de duplicados (por ejemplo, hash o clave natural más versión de fuente). | Carga idempotente en la base de datos |
| **10** | 7-13 dic | Implementar reglas de validación (nulos, rangos, tipos, duplicados). Registrar en la bitácora errores, duración, filas procesadas e indicadores de calidad. Conectar el pipeline completo con un punto de entrada único (CLI) y programar con cron. | Pipeline ETL de extremo a extremo con registro de ejecuciones |
| **11** | 14-20 dic | Desarrollar la API REST con FastAPI: listar fuentes, consultar ejecuciones y consultar datos integrados. Documentación automática (Swagger). | API básica funcionando |
| **12** | 21-27 dic | Tablero de monitoreo en Streamlit (estado de ejecuciones, errores, duración, filas, calidad). *Semana de carga ligera por fiestas.* | Tablero v1 |
| **13** | 28 dic-3 ene | Pruebas del flujo completo (caso de uso del investigador). Corrección de errores. Ejecuciones repetidas para evaluar reproducibilidad y duplicados. Redacción del informe experimental. *Carga ligera.* | Informe experimental borrador y lista de errores corregidos |
| **14** | 4-10 ene | Cierre: documentación final (README, instalación, uso), catálogo de fuentes y reglas definitivo, informe final, preparación de la presentación o demo. Opcional: incorporar una API como fuente si hubo holgura. | Entrega final y demo |

## Hitos de control

- **Fin de semana 6:** fuentes seleccionadas, compatibilidad comprobada y esquema de BD aprobado.
- **Fin de semana 8:** datos de ambas fuentes transformados a un formato común.
- **Fin de semana 10:** pipeline completo ejecutable con registro de ejecuciones.
- **Fin de semana 12:** API y tablero funcionando.
- **Semana 14:** entrega final.

## Mapeo con los productos esperados

| Producto | Semanas |
|----------|---------|
| Pipeline ETL ejecutable y documentado | 7-10, 14 |
| Base de datos y esquema relacional | 6, 9 |
| API básica y tablero de monitoreo | 11-12 |
| Catálogo de fuentes y reglas de transformación | 6, 8, 14 |
| Informe experimental | 13-14 |

## Riesgos y mitigación

| Riesgo | Mitigación |
|--------|------------|
| Las dos fuentes resultan poco compatibles entre sí | Comprobar compatibilidad en la semana 6 y, si falla, cambiar una fuente antes de la semana 7 |
| Cambios de formato o indisponibilidad de la fuente | Guardar copia local versionada de los archivos descargados |
| Retrasos por fiestas de fin de año | Dejar API y tablero cerrados con prioridad antes de la semana 12; semanas 12-13 son de bajo riesgo |
| Falta de tiempo para APIs como fuente | Es opcional; solo se aborda si hay holgura en la semana 14 |

## Roles 

| Integrante | Rol principal |
|------------|---------------|
| Andrés Vallejo | Extracción y fuentes |
| Jorge Guerrero | Transformación y validación con Base de datos y persistencia |
| Kenny Paredes | API y tablero |

## Estructura sugerida del repositorio

```
opendata-etl/
├── README.md
├── PLANIFICACION.md
├── docs/            # catálogo de fuentes, reglas, informe
├── data/raw/        # archivos descargados (ignorados en git si son grandes)
├── src/
│   ├── extract/
│   ├── transform/
│   ├── load/
│   ├── api/
│   └── dashboard/
├── sql/             # esquema
└── tests/
```

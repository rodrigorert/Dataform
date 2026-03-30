# 🚀 Data Warehouse E-commerce con Google Cloud Dataform

Este proyecto implementa una arquitectura profesional de **Analytics Engineering** utilizando **Dataform** de forma nativa en **Google BigQuery**. El objetivo es transformar datos crudos de un e-commerce en un modelo de datos escalable, aplicando las mejores prácticas de ingeniería de datos modernas.

---

## 🏗️ Arquitectura del Proyecto

El flujo de datos sigue la **Medallion Architecture** (Capas de Bronce, Plata y Oro) para asegurar la calidad y trazabilidad:

* **Sources (Capa Raw):** Declaración de tablas de origen (`orders`, `products`, `users`).
* **Staging (Capa Silver):** Limpieza, normalización de esquemas, renombrado de columnas y tipado de datos.
* **Processing (Capa Gold):** Implementación de **tablas incrementales** para optimizar costes y rendimiento en BigQuery.
* **Marts (Capa Analytics):**
    * **Metaprogramación con JS:** Generación dinámica de tablas de ventas regionales (`sales_es`, `sales_fr`, `sales_mx`, etc.) mediante bucles en JavaScript.
    * **Análisis de Cohortes:** Modelo avanzado de retención de clientes para toma de decisiones de negocio.



## 🛠️ Stack Tecnológico

* **Google Cloud Platform (GCP):** Infraestructura en la nube.
* **BigQuery:** Data Warehouse y motor de procesamiento SQL.
* **Dataform (SQLX):** Orquestación, linaje y transformación de datos.
* **JavaScript:** Automatización de código SQL (Principio DRY - Don't Repeat Yourself).
* **GitHub:** Control de versiones y CI/CD con llaves SSH.
* **Antigravity:** Entorno de desarrollo local en VS Code para SQLX.

## 📊 Capacidades Técnicas Implementadas

* ✅ **Tablas Incrementales:** Estrategia de actualización parcial para optimizar el consumo de slots en BigQuery.
* ✅ **Snapshots (SCD Tipo 2):** Captura de cambios históricos en dimensiones críticas (ej. estatus de usuarios).
* ✅ **Calidad de Datos (Assertions):** Tests automáticos de unicidad, valores nulos e integridad referencial.
* ✅ **Seguridad & Ops:** Gestión de permisos mediante sentencias `GRANT` y limpieza de datos históricos vía DML.

---

## 📂 Estructura del Repositorio

```text
```text
├── definitions/
│   ├── marts/
│   │   └── regional_sales.js          # Metaprogramación para tablas regionales
│   ├── ops/
│   │   └── grant_permissions.sqlx     # Gestión de permisos IAM y seguridad
│   ├── processing/
│   │   └── orders_enriched.sqlx       # Lógica incremental de pedidos
│   ├── snapshots/
│   │   └── snp_users_history.sqlx     # Histórico de cambios de usuarios
│   ├── sources/
│   │   ├── raw_orders.sqlx            # Declaración tabla pedidos
│   │   ├── raw_products.sqlx          # Declaración tabla productos
│   │   └── raw_users.sqlx             # Declaración tabla usuarios
│   └── staging/
│       ├── stg_orders.sqlx            # Limpieza de pedidos
│       ├── stg_products.sqlx          # Limpieza de productos
│       ├── stg_users_enriched.sqlx    # Enriquecimiento de usuarios
│       ├── stg_users.sqlx             # Limpieza base de usuarios
│       └── test_stg_users_enriched.sqlx # Tests de calidad (Assertions)
├── includes/
│   └── constants.js                   # Variables globales y constantes
├── init.py                            # Script de inicialización
├── setup.sql                          # Script SQL de carga inicial
├── setup_v2.sql                       # Script SQL de carga actualizado
└── workflow_settings.yaml             # Configuración del proyecto Dataform
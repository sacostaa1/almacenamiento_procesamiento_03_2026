# Taller A — Almacenamiento y Procesamiento de Datos

## Estructura

```
Taller_a/
├── subtaller_1/
│   └── instructivo_aws_s3.md          # Guía paso a paso AWS + S3
├── subtaller_2/
│   └── taller_sql.ipynb               # Notebook de repaso SQL
└── subtaller_3/
    ├── data/
    │   └── ventas_ecommerce.json      # Dataset de prueba (30 registros)
    └── taller_spark_medallion.ipynb   # Notebook Spark + Medallion
```

## Subtaller 1 — AWS y S3 (Free Tier)
Instructivo completo para:
- Crear una cuenta de AWS desde cero
- Configurar seguridad básica (MFA, usuario IAM)
- Operar S3: crear buckets, subir/bajar archivos, URLs pre-firmadas
- Usar AWS CLI para operaciones desde terminal
- Configurar alertas de facturación para no incurrir en costos

## Subtaller 2 — Repaso de SQL
Notebook de Jupyter con SQLite (no requiere instalación de base de datos externa).

**Temas cubiertos:**
- SELECT, WHERE, LIKE, IN, BETWEEN
- ORDER BY, LIMIT
- COUNT, SUM, AVG, MAX, MIN
- GROUP BY, HAVING
- INNER JOIN, LEFT JOIN (2 y 3 tablas)
- Subconsultas (WHERE, FROM)
- Funciones de texto y fecha
- Ejercicios integradores con soluciones

**Requisitos:** `pip install pandas`

## Subtaller 3 — Apache Spark + Arquitectura Medallion
Notebook de Jupyter que implementa un pipeline ETL completo con PySpark.

**Temas cubiertos:**
- Conceptos clave de Spark (RDD, DataFrame, lazy evaluation)
- SparkSession y configuración local
- Capa Bronze: ingesta de JSON, metadata, Parquet
- Capa Silver: limpieza, validación, columnas derivadas
- Capa Gold: KPIs mensuales, ventas por categoría, ranking de clientes
- Spark SQL y Window Functions
- Instructivo completo para migrar a AWS S3 + Glue + Athena

**Requisitos:** `pip install pyspark`

**Dataset:** `ventas_ecommerce.json` — 30 órdenes de e-commerce con clientes colombianos, múltiples productos (electrónica, muebles, libros), fechas Jan–Mar 2024.

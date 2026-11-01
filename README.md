### Reporsitorio editado de la version generada por Copilot

RetailPro es un proyecto de análisis de datos orientado al sector retail, diseñado para transformar información de ventas en insights accionables para los equipos comerciales y de gestión.

### Objetivos del Proyecto

Centralizar análisis de ventas en SQL Server Management Studio 22
Identificar productos de alto valor y alta demanda
Detectar concentración de riesgo y oportunidades de bundle
Generar información útil para equipos de ventas y gerencia

### Herramientas

SQL Server Management Studio 22 (SSMS 22)
GitHub - Versionado
Power BI - Dashboard comercial
Draw.io - Modelo DER (ventas, clientes, productos, categorias)
Bocetos - Diseño de visualizaciones
Copilot - Asistente IA

### Estructura

RetailPro/
│
├── sql/
│   ├── top_productos_facturacion.sql
│   ├── ventas_mensuales.sql
│   ├── indicadores_comerciales.sql
│
├── docs/
│   ├── modelo_datos.md
│   └── diccionario_datos.md


### Cómo Ejecutar los scripts SQL
Con el objetivo de identificar los productos que generan más ingresos analizando el comportamiento comercial mensual, visualizando Ranking de productos, Facturación por producto, Unidades vendidas, Facturación mensual, Número de pedidos y Ticket promedio

#### Crear la base de datos
SQL
CREATE DATABASE RetailPro_DB;
GO
USE RetailPro_DB;
GO

#### Crear la tabla de ventas
CREATE TABLE ventas (
    id_venta INT IDENTITY(1,1) PRIMARY KEY,
    id_producto INT,
    fecha_venta DATE,
    cantidad INT,
    precio_unitario DECIMAL(10,2)
);

#### Top 5 Productos por Facturación
SELECT TOP 5
    id_producto,
    SUM(cantidad) AS unidades_vendidas,
    SUM(cantidad * precio_unitario) AS total_facturado
FROM ventas
GROUP BY id_producto
ORDER BY total_facturado DESC;

#### Ventas Mensuales
SELECT
    MONTH(fecha_venta) AS mes,
    SUM(cantidad * precio_unitario) AS total_facturado,
    COUNT(*) AS cantidad_pedidos,
    AVG(cantidad * precio_unitario) AS ticket_promedio
FROM ventas
GROUP BY MONTH(fecha_venta)
ORDER BY mes;

###  KPIs Principales

#### Facturación Total
SELECT
    SUM(cantidad * precio_unitario) AS facturacion_total
FROM ventas;

#### Ticket Promedio
SELECT
    AVG(cantidad * precio_unitario) AS ticket_promedio
FROM ventas;

#### Producto Más Vendido
SELECT TOP 1
    id_producto,
    SUM(cantidad) AS unidades_vendidas
FROM ventas
GROUP BY id_producto
ORDER BY unidades_vendidas DESC;

### Hallazgos de Negocio
Los análisis permiten responder preguntas como:¿Qué productos generan más ingresos?/¿Qué productos tienen más volumen de ventas?/¿Existe dependencia de pocos productos para sostener la facturación?/¿Cuál es el ticket promedio de los clientes?/¿Qué meses presentan mejor rendimiento comercial?

### Roadmap
Dashboard Power BI con semáforo concentración, Segmentación por ticket y Análisis por categorías

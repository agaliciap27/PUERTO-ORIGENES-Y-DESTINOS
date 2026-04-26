# PUERTO-ORIGENES-Y-DESTINOS
Análisis exploratorio de datos de importaciones y exportaciones del puerto 2025
# Análisis de Movimiento Portuario 2025

Análisis exploratorio de datos de importaciones y exportaciones 
de un puerto mexicano usando SQL.

## Herramientas
- PostgreSQL 18
- pgAdmin 4

## Base de datos
- **importaciones**: 539,485 registros
- **exportaciones**: 128,196 registros

## Análisis realizados
1. Top 10 tipos de carga más importados por tonelaje
2. Top 10 países destino de exportaciones
3. Top 10 países origen de importaciones
4. Mes con mayor movimiento (importaciones + exportaciones)
5. Top 5 entidades destino de carga importada

## Aprendizajes técnicos
- Uso de funciones de agregación: `SUM()`, `COUNT()`
- Limpieza de datos con `SPLIT_PART()`
- Combinación de tablas con `UNION ALL`
- Subconsultas

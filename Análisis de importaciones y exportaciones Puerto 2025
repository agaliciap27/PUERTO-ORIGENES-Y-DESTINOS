-- ============================================================
-- PROYECTO: Análisis de Movimiento Portuario - 2025
-- AUTOR: Andrea Galicia 
-- FUENTE: Datos de operaciones portuarias, México 2025
-- DESCRIPCIÓN: Análisis exploratorio de datos de importaciones
--              y exportaciones del puerto - 2025
-- HERRAMIENTAS: PostgreSQL 18 / pgAdmin 4
-- NOTA: Datos anonimizados para uso académico/portafolio
-- ============================================================

-- Tabla de Importaciones
CREATE TABLE importaciones (
    id          SERIAL PRIMARY KEY,
    mes         VARCHAR(20),
    tipo_carga  VARCHAR(100),
    producto    VARCHAR(200),
    pais_origen VARCHAR(100),
    puerto_origen VARCHAR(100),
    tonelaje    NUMERIC(15,3),
    entidad_destino VARCHAR(100)
);

ALTER TABLE importaciones 
ALTER COLUMN tipo_carga TYPE VARCHAR(500);


-- Tabla de Exportaciones
CREATE TABLE exportaciones (
    id          SERIAL PRIMARY KEY,
    mes         VARCHAR(20),
    tipo_carga  VARCHAR(100),
    producto    VARCHAR(200),
    entidad_origen VARCHAR(100),
    tonelaje    NUMERIC(15,3),
    pais_destino  VARCHAR(100),
    puerto_destino VARCHAR(100)
);


ALTER TABLE exportaciones 
ALTER COLUMN tipo_carga TYPE VARCHAR(500);


SELECT COUNT (*) FROM importaciones;

SELECT * FROM importaciones LIMIT 10;

SELECT COUNT (*) FROM exportaciones;

SELECT 'importaciones' AS tabla, COUNT(*) AS total FROM importaciones
UNION ALL
SELECT 'exportaciones', COUNT(*) FROM exportaciones;

-- ============================================================
-- ANÁLISIS 1: Top 10 tipos de carga más importados por tonelaje
-- ===========================================================
--La mercancía más importada de México son:
--1. Contenedores vacíos, 2. material eléctrico, 3. Autopartes, 4. Productos laminados & 5.Aluminio y sus manufacturas
--Nota: se tomó, "SIN DECLARAR" como contenedores vacíos. 
--"SAID TO CONTAIN AIR CONDITIONERS" se clasifica como material eléctrico. 
--El top 10 refleja que los principales productos importados son: contenedores vacíos,
-- material eléctrico, autopartes, productos laminados y aluminio.

SELECT SUM (tonelaje) AS "TOTAL" , tipo_carga
FROM importaciones 
GROUP BY tipo_carga 
ORDER BY "TOTAL" desc
LIMIT 10;

-- ============================================================
-- ANÁLISIS 2: Top 10 países destino de exportaciones
-- ============================================================
--Los países a los que más exporta México son:
--1.China, 2.Colombia,3. Corea del Sur, 4.Japón & 5. Panama. 

SELECT SUM(tonelaje) AS "TONELADAS", pais_destino 
FROM exportaciones 
GROUP BY pais_destino 
ORDER BY "TONELADAS" DESC
LIMIT 10;


-- ============================================================
-- ANÁLISIS 3: Top 10 países origen de importaciones
-- ============================================================
--Los países con mayor movimiento de TONELADAS de importación son:
--China, Corea del Sur, Chile, Japon y Taiwan. 

SELECT SUM (tonelaje) AS "TONELADAS", pais_origen 
FROM importaciones
GROUP BY pais_origen 
ORDER BY  "TONELADAS" desc
LIMIT 10;

-- ============================================================
-- ANÁLISIS 4A: Mes con mayor movimiento total (importaciones + exportaciones)
-- ============================================================
-- Se uso UNION ALL para combinar ambas tablas y calcular el movimiento total por mes sin importar el tipo de operación. 


SELECT mes, SUM(tonelaje) AS "TOTAL"
FROM (
SELECT mes, tonelaje FROM importaciones
UNION ALL
SELECT mes, tonelaje FROM exportaciones
) 
AS movimiento_total
GROUP BY mes
ORDER BY "TOTAL" DESC
LIMIT 3;


--Mes con más movimiento en el 2025 IMPORTACIÓN
--Se usó SPLIT_PART para limpiar la columna mes que contiene "MES TERMINAL"
SELECT 
    SPLIT_PART(mes, ' ', 1) AS mes_limpio,
    SUM(tonelaje) AS "TONELAJE"
	FROM importaciones
	GROUP BY mes_limpio
	ORDER BY "TONELAJE" desc
	LIMIT 5;

-- Mes con más movimiento en el 2025 EXPORTACIÓN tomando en cuenta la TERMINAL
-- SSA y CONTECON son las TERMINALES con mayor movimiento
--Junio fue el mes con mayor movimiento con la terminal SSA,
--Octubre con un movimiento de 141386.100 ton con la terminal de CONTECON. 

SELECT mes, SUM (tonelaje) as "TONELAJE"
FROM exportaciones
GROUP BY mes
ORDER BY "TONELAJE" desc
LIMIT 3;


--Movimiento por mes
--Se usó SPLIT_PART para limpiar la columna mes que contiene "MES TERMINAL"
--Los meses que representaron mayor carga para el puerto respecto a la exportación en 2025 fueron:
--1. Junio, 2. Octubre, 3. Diciembre
SELECT 
    SPLIT_PART(mes, ' ', 1) AS mes_limpio,
    SUM(tonelaje) AS "TONELAJE"
	FROM exportaciones
	GROUP BY mes
	ORDER BY "TONELAJE" desc
	LIMIT 3;

-- ============================================================
-- ANÁLISIS 5: Top 5 entidades destino de importaciones
-- ============================================================
--¿A qué estados de México llega más carga importada?
-- Las entidades a las que más llega carga son 
--1. Colima, 2. Ciudad de México, 3. Nuevo León, 4. Jalisco y 5. Guanajuato; 
--Los cuales son los centros de manufactura y consumo más grandes del país

SELECT SUM (tonelaje) AS "Toneladas", entidad_destino
FROM importaciones
GROUP BY entidad_destino
ORDER BY "Toneladas" desc
LIMIT 5;

-- ============================================================
-- FIN DEL ANÁLISIS 
-- ============================================================

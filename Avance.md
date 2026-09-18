# Reporte de Avance Semanal - Módulo de Base de Datos

**Alumno:** J  
**Proyecto:** Extratron (Proyecto Integrador)  
**Periodo:** Semana 1 a Semana 2  

---

## 1. Resumen de Actividades Realizadas

### **Semana 1: Investigación, Entorno y Primeras Pruebas**
* **Evaluación de Docker vs DBeaver:** Durante el inicio se investigó la implementación del entorno de base de datos utilizando Docker para estandarizar el contenedor de PostgreSQL.
* **Pruebas de Conexión a Servidor:** Me conecté exitosamente mediante **DBeaver** a un servidor PostgreSQL remoto desplegado por un compañero de equipo.
* **Creación de la Primera Tabla de Prueba:** Se diseñó y ejecutó la creación de una tabla sencilla directamente en el servidor remoto para validar que las modificaciones de un integrante fueran visibles en tiempo real por los demás miembros del equipo.

### **Semana 2: Manejo de Datos Masivos (INEGI DENUE) y Pruebas Locales**
* **Descarga e Inspección de Datos Masivos:** Se descargó el dataset del **DENUE (INEGI)** correspondiente a cerca de **1,000,000 de registros en formato CSV** para la preparación de las tablas geográficas reales del proyecto.
* **Resolución de Problemas de Importación:** Ante fallas en la asignación de esquemas/tablas mediante la interfaz de DBeaver en el servidor remoto, se configuró una instancia local en mi laptop personal para realizar pruebas exitosas de carga del CSV masivo.
* **Ajuste y Familiarización con DBeaver:** Aprendizaje práctico en la configuración de *data mappings*, tipos de columnas y manejo de *encodings* en importaciones masivas.

---

## 2. Acuerdos de Equipo y Estado del Proyecto
* **Conectividad con API (Ruvalcaba):** Durante las semanas 1 y 2, Ruvalcaba presentó problemas técnicos continuos de red/autenticación para lograr la conexión entre el servidor de PostgreSQL. Debido a esto, la integración de la API se retrasó para la siguiente fase y el trabajo se centró en la estabilidad de la Base de Datos, carga de datos locales y creación de usuarios así como la seguridad 
* **Estandarización del Cliente:** Se acordó adoptar **DBeaver** como el gestor gráfico oficial para el equipo debido a su flexibilidad para gestionar múltiples conexiones (local y remota).

---

## 3. Conceptos Estudiados y Teoría Aplicada
* **Virtualización y Contenedores (Docker):** Concepto de aislamiento de servicios, imágenes de PostgreSQL, puerto por defecto (`5432`) y la dependencia de extensiones como `VT-x/AMD-V` en la BIOS del sistema operativo.
* **Normalización y Tipos de Datos PostgreSQL:** Uso de datos de texto amplio (`TEXT`, `VARCHAR`), tipos numéricos de precisión para coordenadas (`NUMERIC`, `DOUBLE PRECISION`) y fechas (`TIMESTAMP`).
* **Carga Masiva (Bulk Loading):** Estrategia para procesar archivos CSV pesados (~1M de filas) optimizando lecturas por bloque (*chunk size*) para evitar la saturación de memoria en el cliente de base de datos.

---

## 4. Librerías y Herramientas Utilizadas
* **DBeaver Community:** Utilizado como la herramienta principal para la creación de esquemas, consultas SQL e importación de archivos `.csv`.
* **PostgreSQL:** Sistema gestor de bases de datos relacionales utilizado en el servidor y en la laptop local.
* **Docker Desktop:** Herramienta de contenedorización puesta a prueba durante la fase inicial.

---

## 5. Código CREADO por el Alumno (Ejemplos Reales)

### A. Creación de Tabla de Prueba en Servidor Remoto (Validación de Equipo)
```sql
-- Tabla sencilla creada en DBeaver para confirmar sincronización en el servidor
CREATE TABLE test_conexion (
    id SERIAL PRIMARY KEY,
    nombre_integrante VARCHAR(50) NOT NULL,
    fecha_conexion TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    estatus TEXT
);

-- Inserción de prueba realizada en DBeaver
INSERT INTO test_conexion (nombre_integrante, estatus) 
VALUES ('J', 'Conexión exitosa al servidor remoto desde DBeaver');

-- Consulta de verificación
SELECT * FROM test_conexion;

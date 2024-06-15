# Implementacion de la base de datos


A partir de este punto, procedimos a implementar nuestra base de datos en MySQL. Utilizamos las estructuras optimizadas y normalizadas que diseñamos previamente, 
asegurándonos de que cada tabla reflejara adecuadamente las entidades y relaciones definidas durante el proceso de modelado. Tener en cuenta que se realizo la importacion de los datos por medio de codigo MySQL.


## Paso 1: Creación de la Base de Datos y las Tablas

Primero, vamos a crear la base de datos y varias las tablas tomadas de la normalización.

### Crear la Base de Datos

```sql
CREATE DATABASE dataincident2;
USE dataincident2;
```
### Crear las Tablas

```sql
CREATE TABLE eventos (
    `IdEvento` INT AUTO_INCREMENT PRIMARY KEY,
    `Fecha_del_evento` DATETIME,
    `Numero_servicio` INT,
    `Estacion` VARCHAR(100),
);
CREATE TABLE ubicaciones (
    `IdUbicacion` INT AUTO_INCREMENT PRIMARY KEY,
    `Barrio` VARCHAR(100),
    `Estrato` INT,
    `UPZ` VARCHAR(100),
    `Localidad` VARCHAR(100)
);
CREATE TABLE servicio (
    `IdServicio` INT AUTO_INCREMENT PRIMARY KEY,
    `Servicio` INT,
    `Clase_de_servicio` VARCHAR(100),
    `Origen_de_la_causa` VARCHAR(100),
    `Hora_reporte` DATATIME,
    `Tiempo_de_respuesta` INT,
);
CREATE TABLE afectados (
    `IdAFECTADOS` INT AUTO_INCREMENT PRIMARY KEY,
    `HombresExpuestos` INT,
    `MujeresExpuestas` INT,
    `MenoresNinasExpuestas` INT,
    `MenoresNinosExpuestos` INT,
    `HombresAfectados` INT,
    `MujeresAfectadas` INT,
    `MenoresNinasAfectadas` INT,
    `MenoresNinosAfectados` INT,
    `HombresRescatados` INT,
    `MujeresRescatadas` INT,
    `MenoresNinasRescatadas` INT,
    `MenoresNinosRescatados` INT,
    `HombresHeridos` INT,
    `MujeresHeridas` INT,
    `MenoresNinasHeridas` INT,
    `MenoresNinosHeridos` INT,
    `HombresSinSignos` INT,
    `MujeresSinSignos` INT,
    `MenoresNinasSinSignos` INT,
    `MenoresNinosSinSignos` INT,
);

CREATE TABLE Causa (
    `IdCausa` INT AUTO_INCREMENT PRIMARY KEY,
    `Origen_de_la_causa` VARCHAR(255),
    `Descripcion` VARCHAR(255)
);
CREATE TABLE Estacion (
    `IdEstacion` INT AUTO_INCREMENT PRIMARY KEY,
    `UbicacionEstacion` VARCHAR(255),
    `NombreEstacion` VARCHAR(255)
);
CREATE TABLE Estrato (
    `IdEstrato` INT AUTO_INCREMENT PRIMARY KEY,
    `Estrato` VARCHAR(255),
    `Descripcion` VARCHAR(255)
);
```





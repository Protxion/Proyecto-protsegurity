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
    `IdUbicacion` INT,
    `IdCausa` INT,
    `IdEstacion` INT,
    FOREIGN KEY (`IdUbicacion`) REFERENCES ubicaciones(`IdUbicacion`),
    FOREIGN KEY (`IdCausa`) REFERENCES Causa(`IdCausa`),
    FOREIGN KEY (`IdEstacion`) REFERENCES Estacion(`IdEstacion`)
);
CREATE TABLE ubicaciones (
    `IdUbicacion` INT AUTO_INCREMENT PRIMARY KEY,
    `Barrio` VARCHAR(100),
    `Estrato` INT,
    `UPZ` VARCHAR(100),
    `Localidad` VARCHAR(100),
    `IdEstrato` INT,
    FOREIGN KEY (`IdEstrato`) REFERENCES Estrato(`IdEstrato`)
);
CREATE TABLE servicio (
    `IdServicio` INT AUTO_INCREMENT PRIMARY KEY,
    `IdEvento` INT,
    `Servicio` INT,
    `Clase_de_servicio` VARCHAR(100),
    `Hora_reporte` DATETIME,
    `Tiempo_de_respuesta` INT,
    FOREIGN KEY (`IdEvento`) REFERENCES eventos(`IdEvento`)
);
CREATE TABLE afectados (
    `IdAFECTADOS` INT AUTO_INCREMENT PRIMARY KEY,
    `IdEvento` INT,
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
    FOREIGN KEY (`IdEvento`) REFERENCES eventos(`IdEvento`)
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

## Paso 2: Importación de los datos

Se realizo la importación por medio de de codigo MySQL

Primero buscaremos la carpeta donde debemos dejar nuestros archivos CSV para luego ser cargados.

### Busqueda de carpeta aceptada por MySQL

```sql
SHOW VARIABLES LIKE 'secure_file_priv';
```
Resultado entregado:
<p aling="center">
    <img src="https://github.com/Protxion/Proyecto-protsegurity/assets/170147724/b8a0c1a8-51d4-4147-bc7a-914f8bfa02de">
</p>

A continuación, cargamos nuestros archivos CSV en la ruta designada para que pudiéramos importar los datos correspondientes a las tablas ya creadas en nuestra base de datos. 
Este paso fue crucial para poblar la base de datos con la información real, permitiéndonos comenzar a trabajar con datos concretos.
Aseguramos que los archivos CSV estuvieran bien formateados y que los datos estuvieran limpios para evitar errores durante el proceso de importación.

![image](https://github.com/Protxion/Proyecto-protsegurity/assets/170147724/33b0a208-e777-4110-b258-01d847a1765e)

### Importacion de tablas

```sql
LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/eventos.csv'
INTO TABLE eventos
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 LINES;
```
```sql
LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/afectados.csv'
INTO TABLE afectados
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 LINES;
```
```sql
LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/ubicaciones.csv'
INTO TABLE ubicaciones
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 LINES;
```
```sql
LOAD DATA INFILE 'C:/ProgramData/MySQL/MySQL Server 8.0/Uploads/servicioss.csv'
INTO TABLE servicio
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\r\n'
IGNORE 1 LINES
(@IdServicio, @Servicio, @Clase_de_servicio, @Origen_de_la_causa, @Hora_reporte, @Tiempo_de_Respuesta)
SET IdServicio = NULLIF(@IdServicio, ''),
    Servicio = @Servicio,
    Clase_de_servicio = @Clase_de_servicio,
    Origen_de_la_causa = @Origen_de_la_causa,
    Hora_reporte = STR_TO_DATE(@Hora_reporte, '%h:%i:%s %p'),
    Tiempo_de_Respuesta = STR_TO_DATE(@Tiempo_de_Respuesta, '%h:%i:%s %p');
```



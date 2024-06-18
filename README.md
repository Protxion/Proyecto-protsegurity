<a name="readme-top"></a>

# Proyecto-protsegurity

> Este proyecto se centra en la creacion de una aplicacion de seguridad avanzada, con el uso de I.A, realizamos un estudio a casos atendidos por bomberos en la ciudad de Bogota, para asi determinar incidentes comunes, tiempos de respuesta etc... Utilizando una base de datos robusta y bien estructurada, se recopilaron y organizaron datos detallados sobre diversos tipos de incidentes, desde incendios hasta emergencias médicas y rescates. La base de datos permite un almacenamiento eficiente y una consulta rápida de la información, facilitando la identificación de patrones, la evaluación de la respuesta de los bomberos y la implementación de mejoras operativas. Este enfoque basado en datos proporciona una visión integral de la frecuencia, localización y naturaleza de los incidentes, mejorando la capacidad de respuesta y planificación estratégica de los servicios de emergencia en Bogotá.

## Built With

- Sql

## Authors

👤 **Santiago Sandoval Urrego**

- GitHub: [@Protxion](https://github.com/Protxion)

👤 **Jhon Alejandro Buitrago**

- GitHub: [@Alecjandro](https://github.com/Alecjandro)

## Show your support

Give a ⭐️ if you like this project!

### Problema:
> La gestión eficiente y segura de grandes volúmenes de datos es un desafío crítico para un sistema de seguridad doméstica basado en IA. Se necesita una infraestructura de base de datos que soporte el almacenamiento, procesamiento y análisis de datos en tiempo real provenientes de múltiples fuentes (cámaras, micrófonos, sensores de movimiento).

### Solución:
> Desarrollar una base de datos robusta y escalable que permita la integración y gestión de datos multimodales (imágenes, audio, datos de sensores) para mejorar la detección de incidentes y la respuesta en tiempo real. La base de datos debe ser capaz de soportar consultas complejas y análisis predictivos para optimizar continuamente la precisión del sistema de seguridad.

### Objetivo Principal:
> Implementar una base de datos eficiente y escalable que soporte la infraestructura de un sistema de seguridad doméstica basado en IA, permitiendo el almacenamiento, procesamiento y análisis en tiempo real de datos multimodales.

### Gestión Eficiente de Datos:
> Diseñar una base de datos que maneje grandes volúmenes de datos de diversas fuentes de manera eficiente.
Análisis en Tiempo Real:
Facilitar el análisis y la respuesta en tiempo real mediante técnicas avanzadas de procesamiento de datos.
Seguridad y Privacidad:
Asegurar la protección de datos sensibles y la privacidad de los usuarios mediante medidas de seguridad robustas.
Herramientas y Métodos
Herramientas Utilizadas:

### Bases de Datos Relacionales (SQL):

> Aporte: Estructuran y gestionan datos transaccionales con integridad y relaciones bien definidas.
Aplicación: Manejan datos estructurados, como registros de eventos y metadatos de sensores.

### Bases de Datos NoSQL:

> a) Ofrecen flexibilidad y escalabilidad para manejar datos no estructurados y semiestructurados.
Aplicación: Almacenan grandes volúmenes de datos de imágenes y audio, así como logs de sensores.
Herramientas de Análisis de Big Data:

> B) Permiten el procesamiento y análisis de grandes volúmenes de datos.
Aplicación: Facilitan el análisis predictivo y la detección de patrones en los datos históricos.
Infraestructura en la Nube:

> C) Proporciona escalabilidad y disponibilidad para la base de datos.
Aplicación: Soporta la expansión y accesibilidad global del sistema de seguridad.
Aplicaciones de la Base de Datos
Aplicaciones:

### Almacenamiento y Recuperación de Datos:
> Facilita el acceso rápido y seguro a datos históricos y en tiempo real.
Análisis Predictivo y Detección de Patrones:
Utiliza datos históricos para predecir y prevenir futuros incidentes.
Integración con Sistemas de IA:
Proporciona datos a los algoritmos de IA para mejorar la precisión y la respuesta.
Gestión de Alertas y Notificaciones:
Almacena y procesa datos para generar alertas y notificaciones en tiempo real.
Requisitos y Características de la Base de Datos
Requisitos:

### Escalabilidad:
> Capaz de manejar un creciente volumen de datos a medida que se agregan más usuarios y sensores.
Flexibilidad:
Soporte para diferentes tipos de datos (imágenes, audio, texto).
Granularidad:
Almacenamiento de datos detallados y específicos para análisis profundo.
Seguridad:
Protección de datos sensibles y aseguramiento de la privacidad del usuario.
Disponibilidad:
Alta disponibilidad para garantizar que los datos estén accesibles en cualquier momento.
Características:

### Distribución Geográfica:
> Bases de datos distribuidas globalmente para reducir latencias y mejorar la disponibilidad.
Redundancia y Respaldo:
Implementación de mecanismos de respaldo y recuperación para asegurar la continuidad del servicio.
Optimización para Consultas Complejas:
Estructuras de índices y optimización de consultas para mejorar la eficiencia en la recuperación de datos.

#### Distribucion del trabajo:
- Investigación y Análisis del Tema: Santigo Sandoval-Alejandro Buitrago
- Diseño de la Base de Datos: Alejandro Buitrago
- Implementación de la Base de Datos: Alejandro Buitrago
- Pruebas y Validación: Santiago Sandoval
- Conclusiones y Futuros Aportes: Santiago Sandoval


# Consultas

### Obtener todos los incidentes
```sql
SELECT * FROM eventos;
```
### Obtener todos los servicio de tipo "INCENDIOS"
```sql
SELECT * FROM servicio WHERE Clase_de_servicio LIKE '%INCENDIOS';
```
### Contar el número de incidentes por estación
```sql
SELECT Estacion, COUNT(*) AS Numero_de_servicio 
FROM eventos
GROUP BY Estacion;
```
### Obtener el número total de hombres y mujeres expuestos en todos los incidentes
```sql
SELECT SUM(HOMBRES_EXPUESTOS) AS total_hombres_expuestos, SUM(MUJERES_EXPUESTAS) AS mujeres_expuestas 
FROM afectados;
```
### Obtener todos los incidentes reportados en un rango de fechas específico
```sql
SELECT * FROM eventos
WHERE Fecha_del_evento BETWEEN '2020-01-01' AND '2020-05-04';
```
### Obtener la media de tiempo de respuesta para los incidentes de tipo "Incendio"
```sql
SELECT AVG(TIME_TO_SEC(Tiempo_de_respuesta)) / 60 AS Tiempo_de_respuesta
FROM servicio 
JOIN eventos ON eventos.IdEvento = Servicio.idServicio
WHERE servicio LIKE '%INCENDIOS';
```
### Obtener todos los incidentes con más de 5 personas expuestas
```sql
SELECT * FROM eventos
JOIN afectados ON afectados.IdAFECTADOS = afectados.IdAFECTADOS 
WHERE HOMBRES_EXPUESTOS + MUJERES_EXPUESTAS + MENORES_NINAS_EXPUESTAS + MENORES_NINOS_EXPUESTOS > 5;
```
### Obtener el incidente con el mayor número de personas heridas
```sql
SELECT * FROM eventos 
JOIN afectados ON afectados.IdAFECTADOS = afectados.IdAFECTADOS 
ORDER BY HOMBRES_EXPUESTOS + MUJERES_EXPUESTAS + MENORES_NINAS_EXPUESTAS + MENORES_NINOS_EXPUESTOS DESC 
LIMIT 1;
```
### Obtener el porcentaje de incidentes por tipo de servicio
```sql
SELECT servicio, COUNT(idServicio) * 100.0 / (SELECT COUNT(*) FROM eventos) AS Porcentaje
FROM eventos 
JOIN servicio ON idServicio = idServicio
GROUP BY servicio;
```
### Obtener los 5 barrios con más incidentes reportados
```sql
SELECT ubicaciones.Barrio, COUNT(eventos.IdEvento) AS Numero_incidentes
FROM eventos
JOIN ubicaciones ON ubicaciones.IdUbicacion = ubicaciones.IdUbicacion
GROUP BY ubicaciones.Barrio
ORDER BY Numero_incidentes DESC
LIMIT 5;
```
### Encontrar el incidente con el mayor tiempo de respuesta en cada localidad
```sql
SELECT servicio.*, ubicaciones.Localidad
FROM servicio
JOIN ubicaciones ON servicio.idServicio = ubicaciones.IdUbicacion
WHERE (ubicaciones.Localidad, servicio.Tiempo_de_respuesta) IN (
    SELECT Localidad, MAX(Tiempo_de_respuesta)
    FROM servicio
    JOIN ubicaciones ON servicio.idServicio = ubicaciones.IdUbicacion
    GROUP BY Localidad
);

```
### Obtener la suma total de hombres y mujeres expuestos por barrio y clase de servicio
```sql
SELECT ubicaciones.Barrio, servicio.Clase_de_servicio, 
       SUM(afectados.HOMBRES_EXPUESTOS) AS total_hombres_expuestos, 
       SUM(afectados.MUJERES_EXPUESTAS) AS total_mujeres_expuestas
FROM servicio
JOIN ubicaciones ON servicio.idServicio = ubicaciones.IdUbicacion
JOIN afectados ON servicio.idServicio = afectados.IdAFECTADOS
GROUP BY ubicaciones.Barrio, servicio.Clase_de_servicio;
```

### Obtener la tendencia trimestral de incidentes con origen de causa "Falsa alarma" durante el año 2020
```sql
SELECT QUARTER(eventos.Fecha_del_evento) AS trimestre, 
       COUNT(*) AS Numero_de_incidentes
FROM eventos
JOIN servicio ON eventos.IdEvento = servicio.idServicio
WHERE servicio.Servicio LIKE '%FALSA_ALARMA' AND YEAR(eventos.Fecha_del_evento) = 2020
GROUP BY trimestre
ORDER BY trimestre;
```

### Obtener los 3 barrios con el mayor número de incidentes de tipo "Rescate" y el total de personas afectadas en ellos
```sql
SELECT ubicaciones.Barrio, COUNT(eventos.IdEvento) AS Numero_de_incidentes, 
       SUM(afectados.HOMBRES_EXPUESTOS + afectados.MUJERES_EXPUESTAS + afectados.MENORES_NINAS_EXPUESTAS + afectados.MENORES_NINOS_EXPUESTOS) AS total_afectados
FROM eventos
JOIN ubicaciones ON eventos.IdEvento = ubicaciones.IdUbicacion
JOIN afectados ON eventos.IdEvento = afectados.IdAFECTADOS
JOIN servicio ON eventos.IdEvento = servicio.idServicio
WHERE servicio.Servicio LIKE '%Rescate'
GROUP BY ubicaciones.Barrio
ORDER BY Numero_de_incidentes DESC
LIMIT 3;
```
### Obtener la relación entre el tiempo de respuesta y el número de personas afectadas por origen de causa "Falla electrica" en los diferentes estratos socioeconómicos
```sql
SELECT ubicaciones.Estrato, 
      AVG(TIME_TO_SEC(servicio.Tiempo_de_respuesta)) / 60 AS Tiempo_de_respuesta,
      SUM(afectados.HOMBRES_EXPUESTOS + afectados.MUJERES_EXPUESTAS + afectados.MENORES_NINAS_EXPUESTAS + afectados.MENORES_NINOS_EXPUESTOS) AS total_afectados
FROM servicio
JOIN ubicaciones ON servicio.idServicio = ubicaciones.IdUbicacion
JOIN afectados ON servicio.idServicio = afectados.IdAFECTADOS
WHERE servicio.Servicio LIKE '%FALLA_ELECTRICA'
GROUP BY ubicaciones.Estrato
ORDER BY Tiempo_de_respuesta DESC;
```
# Conclusiones del proyecto, para bases de datos
> El estudio realizado sobre los incidentes atendidos por el cuerpo de bomberos en Bogotá ha proporcionado una visión profunda y detallada de la naturaleza y frecuencia de las emergencias en la ciudad. A través de una base de datos robusta y bien estructurada, se recopilaron datos esenciales que permitieron identificar patrones significativos en los incidentes, tales como las áreas con mayor incidencia de emergencias, los tipos más comunes de incidentes y los tiempos de respuesta promedio.
Este análisis detallado ha facilitado la evaluación de la eficiencia operativa del cuerpo de bomberos, destacando tanto sus fortalezas como las áreas que necesitan mejoras. Por ejemplo, se identificaron zonas geográficas que requieren una mayor presencia de recursos. Además, la base de datos ha permitido una consulta rápida y eficiente de la información, lo que mejora la capacidad de planificación y la toma de decisiones estratégicas.
Los resultados de este estudio demuestran la importancia de una gestión de datos efectiva para optimizar la respuesta a emergencias y mejorar la seguridad pública. Al identificar patrones y tendencias en los incidentes, el cuerpo de bomberos puede implementar estrategias más precisas y efectivas, mejorar la asignación de recursos y reducir los tiempos de respuesta. En conclusión, este proyecto resalta la necesidad de inversiones continuas en tecnología de la información y capacitación, fortaleciendo así la capacidad de respuesta del cuerpo de bomberos y contribuyendo a una Bogotá más segura y resiliente.

# Planes a futuro

### Expansión y Actualización de la Base de Datos:
> Integración con otras entidades de emergencia: Ampliar la base de datos para incluir información de otras entidades de emergencia en Bogotá, como la policía y servicios médicos de urgencia, para tener una visión más completa de la respuesta a incidentes en la ciudad.
### Modelos predictivos: 
> Desarrollar algoritmos de inteligencia artificial y modelos predictivos que analicen los datos históricos para prever futuros incidentes.
### Asignación dinámica: 
> Utilizar los datos para optimizar la asignación de recursos, asegurando que las áreas con mayor incidencia de emergencias tengan una cobertura adecuada de personal y equipos.
### Estudios conjuntos:
> Realizar estudios conjuntos con otras entidades de emergencia y universidades para identificar áreas de mejora y desarrollar nuevas estrategias de respuesta.
### Entrenamiento basado en datos: 
> Desarrollar programas de capacitación que utilicen los datos recopilados para entrenar a los bomberos en escenarios realistas y basados en patrones reales de emergencias.
### Análisis de causas raíz: 
> Realizar estudios detallados sobre las causas raíz de los incidentes más comunes, ayudando a desarrollar programas de prevención más efectivos.
### Aplicaciones móviles: 
> Desarrollar aplicaciones móviles para que el personal de emergencia pueda acceder y actualizar datos en el campo, mejorando la eficiencia y la coordinación.
### Infraestructura tecnológica: 
> Invertir en infraestructura tecnológica avanzada para soportar el almacenamiento y procesamiento de grandes volúmenes de datos.
### Estudio de coordinación: 
> Analizar cómo se coordinan las respuestas a emergencias entre los servicios publicos. 

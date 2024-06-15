# Diagrama EER

Un Diagrama de Entidad-Relación (ERD, por sus siglas en inglés) es una herramienta visual utilizada en la modelización de bases de datos para describir la estructura lógica de las bases de datos de una manera comprensible. 

Los ERD representan las entidades que serán almacenadas en la base de datos, las relaciones entre estas entidades y los atributos de cada entidad. Este tipo de diagrama es fundamental para el diseño conceptual de bases de datos.

# Normalización 

La normalización en bases de datos es un proceso utilizado para organizar los datos en una base de datos relacional. Su objetivo principal es reducir la redundancia de datos y mejorar la integridad de los datos.

El proceso implica dividir una base de datos en dos o más tablas y definir relaciones entre las tablas. La normalización se logra aplicando una serie de reglas conocidas como formas normales.

## Proyecto

Aplicando los conceptos anteriores a nuestro proyecto, comenzamos con una data cruda que inicialmente no había sido sometida a ningún método de normalización. A partir de esta data, procedimos a crear un diagrama EER (Enhanced Entity-Relationship),
lo que nos permitió visualizar la estructura de la base de datos y las relaciones entre las distintas entidades.
Este enfoque sin normalización nos permitió observar cómo evolucionaban los datos en su estado más básico y nos dio una visión clara de las posibles redundancias y dependencias que podrían ser optimizadas en etapas posteriores.

<p align="center">
  <img src="https://github.com/Protxion/Proyecto-protsegurity/assets/170147724/14dec3ce-2e3c-4c50-a31a-bae0138d5f7f" alt="DataCruda" />
</p>

Ya aplicando los metodos de normalización a nuestro diagraama EER, se logro trasnformar la estructura de la base de datos eliminando las redundancias y mejorando la integridad de los datos.

Pasamos por las distintas formas normales, comenzando con la Primera Forma Normal (1NF), donde aseguramos que cada columna contenía datos atómicos y eliminamos los grupos repetitivos.
Luego, avanzamos a la Segunda Forma Normal (2NF) eliminando las dependencias parciales, y finalmente a la Tercera Forma Normal (3NF) para eliminar las dependencias transitivas.

Aqui se encuentra el resultado de la aplicaion de estas 3 formas:

<p align="center">
  <img src="https://github.com/Protxion/Proyecto-protsegurity/assets/170147724/dfe54c0d-d578-47c5-8292-5e4caa640278" alt="resultado">
</p>

Relaciones entre las tablas:

-Evento a Ubicación: Relación Uno a Uno.
-Evento a Servicio: Relación Uno a Muchos.
-Evento a PersonasAfectadas: Relación Uno a Uno.
-Evento tiene una relación de Muchos a Uno con Causa.
-La tabla Ubicacion tiene relaciones de Muchos a Uno con Estrato
-La tabla Evento tiene una relación de Uno a Muchos con Estacion.

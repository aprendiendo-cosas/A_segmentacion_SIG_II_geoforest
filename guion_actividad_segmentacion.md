# Instrucciones para completar el ejercicio entregable de la asignatura "SIG II": Segmentación del territorio a partir de variables biofísicas"




> + **_Versión_**: 2022-2023
> + **_Asignatura_** : SIG II (Máster GEOFOREST). 
> + **_Autores_**: Francisco J. Ruíz-Gómez (ruizgomezfj@gmail.com), Cristina Acosta Muñoz (cristina.acostamunoz@gmail.com), Mª Ángeles Varo (mavaro@uco.es), Curro Bonet-García (fjbonet@uco.es)




## Objetivos

Esta actividad tiene como finalidad última el afianzamiento de los conocimientos adquiridos durante el desarrollo de la asignatura. Se trata de que los estudiantes reproduzcan una parte importante de las técnicas vistas en clase, pero aplicadas a una zona de estudio concreta: el pinar de la Yunquera, en el Parque Nacional de la Sierra de las Nieves. Durante la actividad, los estudiantes adquirirán conocimiento nuevo usando procesos cognitivos superiores (abstracción, transferencia de conocimientos) con un mayor grado de contextualización. Cada estudiante aportará una respuesta diferente al problema planteado. 

Los objetivos específicos de esta actividad son: 

 + Disciplinares (tienen que ver con la ecología y con las ciencias forestales): 
   + Aplicar el concepto de cartografía de la diversidad biológica a un caso concreto. 
   + Definir un flujo de trabajo que permita integrar distintas fuentes de información para obtener un resultado único.
   + Decidir el peso asignado a cada una de las variables anteriores. 
 + Instrumentales (tienen que ver con el manejo de herramientas digitales):
   + Poner en práctica los conocimientos de SIG adquiridos en el máster.
   + Afianzar los conocimientos de R adquiridos para aplicarlos a un contexto espacial diferente al visto en clase.
   + Publicar los resultados en un mapa web.

Los objetivos de aprendizaje anteriores se satisfarán mediante un ejercicio práctico: Segmentación del territorio con la herramienta QGis mediante la aplicación de algortimos de optimización multiobjetivo basados en inteligencia artificial, incluyendo una capa de biodiversidad extraída de GBIF. 



## Secuencia de pasos a dar en el ejercicio

Una parte importante del aprendizaje a adquirir consiste en construir un flujo de trabajo coherente a partir de las sesiones teórico-práticas que hemos realizado en la asignatura. Por eso a continuación no se detallan los pasos a dar de manera concreta. Solo se aportan fases generales. También se incluyen enlaces para descargar la información necesaria en cada caso.



**1. Obtención de un mapa de biodiversidad del "Pinar de Yunquera"**

- [Aquí](https://github.com/aprendiendo-cosas/A_segmentacion_SIG_II_geoforest/raw/2022-2023/geoinfo/limite_yunquera.zip) puedes descargar el límite de la zona de estudio. El sistema de coordenadas es el EPSG 25830.
- [Este](https://github.com/aprendiendo-cosas/A_segmentacion_SIG_II_geoforest/raw/2022-2023/geoinfo/vegetacion_yunquera.zip) enlace contiene un mapa de vegetación de la zona de estudio. Recuerda que en este caso deberás de construir un mapa de vegetación usando los polígonos del mapa anterior como "subrrogados" de las comunidades ecológicas. 
- Descarga todos los datos de presencia de especies en la zona de estudio en el portal de [GBIF](https://www.gbif.org/). En [este](https://youtu.be/6OOusJU4ljs?t=1456) vídeo puedes ver cómo se hace eso. El vídeo es muy largo, así que no avances más allá de donde se explica este asunto. Comprobarás que el mapa que tiene GBIF para descargar los datos es poco amigable. Así que te costará un poco encontrar la zona de estudio. Esta zona se encuentra en el extremo occidental de la costa mediterránea andaluza, a pocos kilómetros de la costa. La siguiente imagen muestra una visualización aproximada de la zona que has de seleccionar con la herramienta del portal de GBIF. Fíjate en las referencias geográficas del mapa para seleccionar tú una zona parecida: ciudad de Marbella al sur, embalses al norte y al oeste de la zona, etc.

![contorno_gbif](https://github.com/aprendiendo-cosas/A_segmentacion_SIG_II_geoforest/raw/2022-2023/imagenes/contorno_zona_gbif.png)



- Aplica el código de R que vimos en la sesión del mapa de biodiversidad para generar dicho mapa en la nueva zona de estudio. Tendrás que modificar ligeramente el código para que funcione en estas nuevas condiciones. Recuerda que necesitarás asignar a cada punto de GBIF el código del polígono del mapa de vegetación en el que se encuentra. Eso implica que cada polígono debe de tener un campo con valores únicos. Comprueba si esto es así y si no, genéralo tú. 
- El resultado del script de R es un fichero de formas vectorial. Para usarlo en el ejercicio de segmentación del territorio, debe de estar en formato raster. Así que transfórmalo a un Raster con las siguientes características:
  - Formato tiff (geotiff)
  - Resolución de pixel de 10x10 m
  - Banda alfa a partir del índice de Shannon (campo H)
- Recorta la capa del índice de Shannon con la de la zona de estudio que obtuviste en la sesión de clase en la que hablamos de segmentación.



**2. Segmentación del territorio**

Deberás de construir un raster virtual usando cuatro capas que puedes descargar del guión correspondiente y del moodle:

+ Densidad de pinsapo: Aporta información sobre la vegetación. 

+ Orientaciones: Aporta información sobre el estrés abiótico derivado de la situación de solana y umbría.

+ Distancia a canales: Aporta información sobre zonas de posible compensación hídrica.

+ Índice de Shannon (H): se obtiene siguiendo el procedimiento establecido en el punto anterior.

Después de obtener las capas anteriores, realiza la segmentación con Orfeo y con los siguientes parámetros:

+ Método: meanshift

+ Radio espacial de búsqueda: 15 m

+ Umbral de convergencia: 1

+ Área umbral: 50 ha



**3. Publicación del mapa resultante en internet**

+ Publica el mapa resultante de la segmentación y las capas parciales en internet. Puedes usar qgis2web o QGIS Cloud. Para ello deberás de poner en práctica lo visto en la sesión correspondiente.




## Material a entregar

Una vez realizados los pasos anteriores deberás de construir un documento de texto que contenga los siguientes elementos:

+ Esquema general del flujo de trabajo que has seguido para completar el ejercicio. Puedes usar cualquier herramienta digital que consideres (ej. powerpoint, [drawio](https://www.draw.io/), etc.) 
+ Composición de mapa con los resultados de segmentación obtenidos. Puedes construirlo con QGIS, ArcGIS, R o como quieras.
+ Enlace al mapa web que hayas creado durante el ejercicio. 
+ Además, deberás responder a las siguientes preguntas:
  + ¿Consideras que el resultado es consistente con la realidad que conoces del terreno?. Justifica tu respuesta.
+ ¿Cuál de las capas (variables) utilizada aparenta tener más influencia en el resultado final? ¿por qué crees que pasa eso?
  + ¿Para qué aspectos de la gestión del territorio crees que sería de utilidad la cartografía obtenida?
+ ¿Cómo mejorarías el resultado? Incorpora alguna sugerencia sobre mejoras técnicas y/o nuevas variables a incorporar.

Una vez elaborado el documento, súbelo a [este](https://moodle.uco.es/m2223/mod/assign/view.php?id=183036) enlace (también lo tienes en el Moodle de la asignatura). El plazo de entrega es hasta el **8 de enero a las 23:59**.



## Evaluación del aprendizaje

Para evaluar y calificar el ejercicio realizado se utilizará una rúbrica que consta de los criterios y niveles que se muestran a continuación:

+ **Criterio 1: Flujo de trabajo presentado**. Este criterio pretende evaluar si el estudiante ha adquirido visión de conjunto suficiente como para resumir en un único esquema los procesos ejecutados.

  + No entrega flujo de trabajo o éste carece de sentido alguno: **0**
  + El flujo de trabajo no contiene los elementos básicos para ser entendido y aplicado: **1**
  + En el esquema aparecen los elementos fundamentales de los procedimientos realizados: **2**
  + Excelente diagrama que muestra con detalle todos los elementos y procedimientos de análisis, y/o incorpora detalles novedosos: **3**

+ **Criterio 2: Comprensión de los procesos ecológicos y forestales subyacentes**. Este criterio evalúa en qué medida el estudiante ha entendido los conceptos teóricos que sustentan las técnicas aplicadas.

  + En las respuestas no hay mención alguna a conceptos ecológicos o forestales: **0**
  + En las respuestas se mencionan algunos conceptos ecológicos o forestales, pero no se elaboran adecuadamente: **1**
  + Buena comprensión de los procesos ecológicos y forestales. Se describen bien los procesos estudiados en las sesiones teórico-prácticas. **2**
  + Excelente comprensión de los conceptos teóricos o incorpora algún concepto nuevo no visto en clase. **3**
+ **Criterio 3: Manejo de técnicas de procesamiento de información ambiental**

  + El estudiante no ha conseguido realizar los análisis requeridos: **0**
  + No ha finalizado el trabajo aunque hay información parcial: **1**
  + El estudiante ha conseguido finalizar los procesos requeridos pero el resultado final es poco coherente temáticamente: **2**
  + Los resultados denotan que el estudiante ha ejecutado con solvencia todos los procedimientos requeridos: **3**

+ **Criterio 4: Presentación del trabajo**

  + No entrega o la presentación es muy deficiente: **0**
  + El trabajo está desordenado, mal maquetado o tiene problemas importantes de diseño: **1**
  + La presentación es aceptable aunque mejorable: **2**
  + Estupenda presentación del trabajo. Detalles muy bien cuidados. **3**

La calificación final del ejercicio se obtendrá de transformar la puntuación obtenida a base 10 

calificacion = (puntuacion*10) / 12




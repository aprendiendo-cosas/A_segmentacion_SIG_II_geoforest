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

- Aquí puedes descargar el límite de la zona de estudio. El sistema de coordenadas es el EPSG 25830.
- Este enlace contiene un mapa de vegetación de la zona de estudio. Recuerda que en este caso deberás de construir un mapa de vegetación usando los polígonos del mapa anterior como "subrrogados" de las comunidades ecológicas. **FALTA ESTO**
- Descarga todos los datos de presencia de especies en la zona de estudio en el portal de [GBIF](https://www.gbif.org/). En [este](https://youtu.be/6OOusJU4ljs?t=1456) vídeo puedes ver cómo se hace eso. El vídeo es muy largo, así que no avances más allá de donde se explica este asunto. Comprobarás que el mapa que tiene GBIF para descargar los datos es poco amigable. Así que te costará un poco encontrar la zona de estudio. Esta zona se encuentra en el extremo occidental de la costa mediterránea andaluza, a pocos kilómetros de la costa. La siguiente imagen muestra una visualización aproximada de la zona que has de seleccionar con la herramienta del portal de GBIF. **FALTA ESTO**
- Aplica el código de R que vimos en la sesión del mapa de biodiversidad para generar dicho mapa en la nueva zona de estudio. Tendrás que modificar ligeramente el código para que funcione en estas nuevas condiciones. Recuerda que necesitarás asignar a cada punto de GBIF el código del polígono del mapa de vegetación en el que se encuentra. Eso implica que cada polígono debe de tener un campo con valores únicos. Comprueba si esto es así y si no, genéralo tú. 
- El resultado del script de R es un fichero de formas vectorial. Para usarlo en el ejercicio de segmentación del territorio, debe de estar en formato raster. Así que transfórmalo a Raster con las siguientes características:
  - Formato tiff (geotiff)
  - Resolución de pixel de 10x10 m
  - Banda alfa a partir del índice de Shannon (campo H)
- Recorta la capa del índice de Shannon con la de la zona de estudio que obtuviste en la sesión de clase en la que hablamos de segmentación.



**2. Segmentación del territorio**

Deberás de construir un raster virtual usando cuatro capas:

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

¿les pedimos esto, Cristina?


## Material a entregar

Una vez realizados los pasos anteriores deberás de construir un documento de texto que contenga los siguientes elementos:

+ Composición de mapa con los resultados de segmentación obtenidos. 

+ Esquema general del flujo de trabajo que has seguido para completar el ejercicio. Puedes usar cualquier herramienta digital que consideres (ej. powerpoint, [drawio](https://www.draw.io/), etc.) 

+ Además, deberás responder a las siguientes preguntas:

  + ¿Consideras que el resultado es consistente con la realidad que conoces del terreno?. Justifica turespuesta.

  + ¿Cuál de las capas (variables) utilizada aparenta tener más influencia en el resultado final? ¿por qué crees que pasa eso?

  + ¿Consideras adecuada la resolución del mapa de diversidad obtenido? Razona tu respuesta.

  + ¿Para qué aspectos de la gestión del territorio crees que sería de utilidad la cartografía obtenida?

  + ¿Cómo mejorarías el resultado? Incorpora alguna sugerencia sobre mejoras técnicas y/o nuevas variables a incorporar.


Una vez elaborado el documento, súbelo a este enlace. **VER SI LO PONEMOS EN TURNITIN**

## Evaluación del aprendizaje

Para evaluar y calificar el ejercicio realizado se utilizará una rúbrica que consta de los criterios y niveles que se muestran a continuación:
+ **Criterio 1: Grado de completitud del flujo de trabajo presentado**. Este criterio pretende evaluar si el estudiante ha adquirido visión de conjunto suficiente como para resumir en un único esquema los procesos ejecutados.
+ **Criterio 2: Comprensión de los procesos ecológicos y forestales subyacentes**. Este criterio evalúa en qué medida el estudiante ha entendido los conceptos teóricos que sustentan las técnicas aplicadas.
  + En las respuestas no hay mención alguna a conceptos ecológicos o forestales: **0**
  + En las respuestas se mencionan algunos conceptos ecológicos o forestales, pero no se elaboran adecuadamente: **1**
  + Buena comprensión de los procesos ecológicos y forestales. Se describ bien los estudiados en las sesiones. **2**
  + Excelente comprensión de los conceptos teóricos. Además se incorpora alguno nuevo no visto en clase. **3**
+ **Criterio 3: Manejo de técnicas de procesamiento de información ambiental**
+ **Criterio 4: Presentación del trabajo**








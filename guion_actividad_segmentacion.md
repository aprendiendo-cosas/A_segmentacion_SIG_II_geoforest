# Instrucciones para completar el ejercicio entregable de la asignatura "SIG II": Segmentación del territorio a partir de variables biofísicas"



> + **_Tipo de material_**: <span style="display: inline-block; font-size: 12px; color: white; background-color: #8D26F5; border-radius: 5px; padding: 5px; font-weight: bold;"> Tarea</span>
>+ **_Versión_**: 2024-2025
>+ **_Asignatura_** : SIG II (Máster GEOFOREST). 
>+ **_Autores_**: Antonio J. Molina Herrera (o22mohea@uco.es) y Curro Bonet-García (fjbonet@uco.es)




## Objetivos

Esta actividad tiene como finalidad última el afianzamiento de los conocimientos adquiridos durante el desarrollo de la asignatura. Se trata de que los estudiantes reproduzcan una parte importante de las técnicas vistas en clase, pero aplicadas a una zona de estudio concreta: Sierra Bermeja, en la provincia de Málaga. Durante la actividad, los estudiantes adquirirán conocimiento nuevo usando procesos cognitivos superiores (abstracción, transferencia de conocimientos) con un mayor grado de contextualización. Cada estudiante aportará una respuesta diferente al problema planteado. 

Los objetivos específicos de esta actividad son: 

 + Disciplinares (tienen que ver con la ecología y con las ciencias forestales): 
   + Entrenar la capacidad de elegir y procesar variables temáticas potencialmente útiles para satisfacer un ojbetivo concreto.
   + Mejorar la capacidad de espacializar variables relevantes a partir de datos puntuales.
   + Definir un flujo de trabajo que permita integrar distintas fuentes de información para obtener un resultado único.
   + Decidir el peso asignado a cada una de las variables anteriores. 
 + Instrumentales (tienen que ver con el manejo de herramientas digitales):
   + Poner en práctica los conocimientos de SIG adquiridos en el máster.
   + Afianzar los conocimientos de R, de GEE y de otros instrumentos adquiridos para aplicarlos a un contexto espacial diferente al visto en clase.
   + Aprender a diseñar un flujo de trabajo útil para lograr un objetivo concreto.

Los objetivos de aprendizaje anteriores se satisfarán mediante un ejercicio práctico con el siguiente enunciado:

> Tras el incendio ocurrido en Sierra Bermeja (provincia de Málaga) en 2021, la Junta de Andalucía decide iniciar un proyecto de restauración de la zona quemada. Para ello, encarga a los estudiantes de GEOFOREST que realicen una zonificación (o estratificación) del territorio en virtud de una serie de variables ambientales: intensidad del fuego, radiación solar, biodiversidad previa al incendio, etc.





## Secuencia de pasos a dar en el ejercicio

Para satisfacer la demanda que se hace en la sección anterior, tendrás que dar los siguientes pasos:



**1. Crear un flujograma (flujo de trabajo) con las variables y técnicas de integración que consideres adecuadas**

Una parte importante del aprendizaje a adquirir consiste en construir un flujo de trabajo coherente a partir de las sesiones teórico-práticas que hemos realizado en la asignatura. Puedes basarte en el esquema inicial que se describe en la sesión introductoria ([aquí](https://raw.githack.com/aprendiendo-cosas/Te_introduccion_SIG_II_geoforest/2024_2025/guion_introduccion_SIG_II_geoforest.html) el guión) o empezar uno tú mismo/a. Te sugerimos que uses la aplicación [draw.io](https://www.drawio.com/blog/diagrams-offline) para hacer el flujograma. 

Recuerda que los objetivos que hay en el flujo de trabajo tienen diferentes significados en función de su geometría:

+ Rombos: indican procesamientos de cualquier tipo. 
+ Rectángulos: fuentes de datos no espaciales.
+ Trapecios: fuentes de datos espaciales.

Además, las flechas que se usan para conectar los objetos denotan una direccionalidad temporal. Es decir, muestran hacia dónde se ejecuta el flujograma.

Deberás de crear un flujograma con tu propuesta de procesos para satisfacer la pregunta del enunciado. En este flujograma tendrás que elegir las variables que consideras relevantes para tu estudio. Puedes seleccionar las que estudiamos en clase o proponer otras diferentes. En cualquier caso, el foco está en el aprendizaje y no tanto en los resultados que obtengas. Es el momento de experimentar, preguntar dudas, etc. 



**2. Obtención de un mapa de biodiversidad de la Sierra Bermeja**

El hecho de que hablemos aquí de esta variable no quiere decir que debas de usarla obligatoriamente. Es tu elección. Aquí solo te damos indicaciones para que la consideres en tu estudio. Lo que sí tendrás que hacer es generar el mapa de biodiversidad de Sierra Bermeja aunque no la uses para la segmentación. Para ello ten en cuenta lo siguiente:

- [Este](https://github.com/aprendiendo-cosas/A_segmentacion_SIG_II_geoforest/raw/2024_2025/geoinfo/vegetacion_sierra_bermeja.zip) enlace contiene un mapa de vegetación de la zona de estudio. Recuerda que en este caso deberás de construir un mapa de vegetación usando los polígonos del mapa anterior como "subrrogados" de las comunidades ecológicas. 
- Descarga todos los datos de presencia de especies en la zona de estudio en el portal de [GBIF](https://www.gbif.org/). En [este](https://youtu.be/6OOusJU4ljs?t=1456) vídeo puedes ver cómo se hace eso. El vídeo es muy largo, así que no avances más allá de donde se explica este asunto. Comprobarás que el mapa que tiene GBIF para descargar los datos es poco amigable. Así que te costará un poco encontrar la zona de estudio. Esta zona se encuentra en el extremo occidental de la costa mediterránea andaluza, a pocos kilómetros de la costa. La siguiente imagen muestra una visualización aproximada de la zona que has de seleccionar con la herramienta del portal de GBIF. Fíjate en las referencias geográficas del mapa para seleccionar tú una zona parecida: ciudad de Estepona al sur, embalses al norte y al oeste de la zona, etc.

![contorno_gbif](https://raw.githubusercontent.com/aprendiendo-cosas/A_segmentacion_SIG_II_geoforest/2024_2025/imagenes/contorno_zona_gbif.png)



- Aplica el código de R que vimos en la sesión del mapa de biodiversidad para generar dicho mapa en la nueva zona de estudio. Tendrás que modificar ligeramente el código para que funcione en estas nuevas condiciones. Recuerda que necesitarás asignar a cada punto de GBIF el código del polígono del mapa de vegetación en el que se encuentra. Eso implica que cada polígono debe de tener un campo con valores únicos. Comprueba si esto es así y si no, genéralo tú. 
- El resultado del script de R es un fichero de formas vectorial. Para usarlo en el ejercicio de segmentación del territorio, debe de estar en formato raster. Así que transfórmalo a un Raster con las siguientes características:
  - Formato tiff (geotiff)
  - Resolución de pixel de 10x10 m
  - Campo a partir del cual generar el raster: H
- Recorta la capa del índice de Shannon con la de la zona de estudio que obtuviste en la sesión de clase en la que trabajamos con GEE y delimitamos con detalle la zona del incendio.



**2. Segmentación del territorio**

Deberás de construir un raster que segmente el territorio en zonas homogéneas desde el punto de vista de las variables que hayas elegido. Para hacer esto deberás de elegir una de las dos siguientes opciones:

+ Zonificación para abordar tareas de restauración en la primera fase tras el incendio. Estas actuaciones, como sabes, están dirigidas a minimizar la pérdida de suelo. Si eliges esta opción deberás de usar variables relacionadas con este objetivo.
+ Zonificación para abordar las tareas de restauración de la vegetación. En una segunda fase se pueden realizar acciones de restauración de la cubierta vegetal. En este caso se usarán variables diferentes para zonificar el territorio. Si eliges esta opción tendrás que justificar las variables elegidas.




## Material a entregar

Una vez realizados los pasos anteriores deberás de construir un documento que se asemeje a un informe técnico para que la Junta de Andalucía (promotora del estudio) puede planificar en base a éste donde focalizar sus esfuerzos de restauración en la zona. El documento deberá contener los siguientes elementos:
+ Introducción y objetivos del informe.
+ "Abordaje" metodológico del caso de estudio:
  + Esquema general del flujo de trabajo que has seguido para completar el ejercicio. Puedes usar cualquier herramienta digital que consideres (ej. powerpoint, [drawio](https://www.draw.io/), etc.).
  + Descripción de los métodos utilizados, errores cometidos, principales aprendizajes, etc.
  + Descripción del método o de los métodos de integración de variables que elijas. Debes de justificarlotodo lo mejor posible usando conceptos ecológicos y forestales.
  + Propuestas de mejora que se te ocurran. Nuevas variables o técnicas analíticas diferentes.
+ Resultado final:
  + Composición de mapa con los resultados de segmentación obtenidos. Puedes construirlo con QGIS, ArcGIS, R o como quieras.
  + Otros que se te ocurran que ayuden a la comprensión del mapa final y que apoyen tu discusión final (último apartado de cierre)
+ Breve discusión del mapa final.
+ Fuentes de información utilizadas. Incluye aquí enlaces a las conversaciones con ChatGPT u otra IA que hayas usado en tu trabajo. Normalmente todas ellas tienen un botón de compartir.

  

Una vez elaborado el documento, súbelo a [este](https://moodle.uco.es/m2425/mod/assign/view.php?id=189068) enlace (también lo tienes en el Moodle de la asignatura). El plazo de entrega es hasta el **8 de enero a las 23:59**.



## Forma de proceder durante la elaboración del trabajo

El objetivo final de esta actividad es promover el aprendizaje profundo. Sabemos que ese aprendizaje se consigue estudiando, trabajando y equivocándose. De hecho, el error es la principal fuente de aprendizaje. Bueno, en realidad es el esfuerzo que ponemos en saber por qué nos hemos equivocado lo que provoca el aprendizaje. Y en ese proceso es recomendable estar acompañado por alguien que ya se ha equivocado antes... Esos álguienes somos los profesores de la asignatura. Así que, os recomendamos que nos preguntéis todo lo que necesitéis y que escribáias en vuestra memoria todos los pasos que vayáis dando, incluyendo los errores cometidos. 

Según la filosofía anterior, estaremos encantados de leer vuestros trabajos antes de que hagáis la entrega final. Podéis enviarlos para que los revisemos y los devolveremos con comentarios. 

Además, os recomendamos que trabajéis juntos y que os ayudéis entre vosotros. Esto es importante porque las personas que tienen un nivel de conocimientos parecidos aprenden mejor juntos. Pero es importante que la entrega final sea individual. Es decir, podéis compartir el trabajo, pero la redacción y elaboración del material final debe de ser individual. Si os copiais lo vamos a ver y no os va a  gustar. Si honestamente consideráis que algunos trabajos se parecen mucho, por favor, hacédnoslo saber y veremos cómo proceder.



## Evaluación del aprendizaje

Para evaluar y calificar el ejercicio realizado se utilizará una rúbrica que consta de los criterios y niveles que se muestran a continuación:

+ **Criterio 1: Flujo de trabajo presentado**. Este criterio pretende evaluar si el estudiante ha adquirido visión de conjunto suficiente como para resumir en un único esquema los procesos ejecutados.

  + No entrega flujo de trabajo o éste carece de sentido alguno: **0**
  + El flujo de trabajo no contiene los elementos básicos para ser entendido y aplicado: **1**
  + En el esquema aparecen los elementos fundamentales de los procedimientos realizados: **2**
  + Excelente diagrama que muestra con detalle todos los elementos y procedimientos de análisis, y/o incorpora detalles novedosos: **3**

+ **Criterio 2: Comprensión de los procesos ecológicos y forestales subyacentes**. Este criterio evalúa en qué medida el estudiante ha entendido los conceptos teóricos que sustentan las técnicas aplicadas. Esto se evaluará en función de la justificación de la selección de variables y su procesamiento. 

  + En el texto descriptivo no hay mención alguna a conceptos ecológicos o forestales: **0**
  + En el texto descriptivo se mencionan algunos conceptos ecológicos o forestales, pero no se elaboran adecuadamente: **1**
  + Buena comprensión de los procesos ecológicos y forestales. Se describen bien los procesos estudiados en las sesiones teórico-prácticas. **2**
  + Excelente comprensión de los conceptos teóricos o incorpora algún concepto nuevo no visto en clase. **3**
+ **Criterio 3: Manejo de técnicas de procesamiento de información ambiental**

  + El estudiante no ha conseguido realizar los análisis requeridos: **0**
  + No ha finalizado el trabajo aunque hay información parcial: **1**
  + El estudiante ha conseguido finalizar los procesos requeridos pero el resultado final es poco coherente temáticamente: **2**
  + Los resultados denotan que el estudiante ha ejecutado con solvencia todos los procedimientos requeridos. Además lo ha documentado y ha experimentado con métodos diferentes: **3**

+ **Criterio 4: Presentación del trabajo**

  + No entrega o la presentación es muy deficiente: **0**
  + El trabajo está desordenado, mal maquetado o tiene problemas importantes de diseño: **1**
  + La presentación es aceptable aunque mejorable: **2**
  + Estupenda presentación del trabajo. Detalles muy bien cuidados. **3**

La calificación final del ejercicio se obtendrá de transformar la puntuación obtenida a base 10 

calificacion = (puntuacion*10) / 12





****

[Aquí](https://github.com/aprendiendo-cosas/A_escalas_shannon_Andalucia_SIG_II_geoforest/archive/refs/tags/2024_2025.zip) puedes descargar un archivo .zip que contiene este guión en formato html y todo el material que incluye.

****
Haz click [aquí](https://github.com/aprendiendo-cosas/A_escalas_shannon_Andalucia_SIG_II_geoforest/releases) para ver cómo ha cambiado este guión en los distintos cursos académicos.

****
 <p xmlns:cc="http://creativecommons.org/ns#" >El contenido de este repositorio se puede utilizar bajo la siguiente licencia:  <a  href="https://creativecommons.org/licenses/by-nc-sa/4.0/?ref=chooser-v1"  target="_blank" rel="license noopener noreferrer"  style="display:inline-block;">CC BY-NC-SA 4.0<img  style="height:22px!important;margin-left:3px;vertical-align:text-bottom;"   src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"  alt=""><img  style="height:22px!important;margin-left:3px;vertical-align:text-bottom;"   src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"  alt=""><img  style="height:22px!important;margin-left:3px;vertical-align:text-bottom;"   src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1"  alt=""><img  style="height:22px!important;margin-left:3px;vertical-align:text-bottom;"   src="https://mirrors.creativecommons.org/presskit/icons/sa.svg?ref=chooser-v1"  alt=""></a></p> 

<p>Esta licencia no aplica a enlaces a artículos, libros o imágenes no originales. Estos productos tienen su licencia correspondiente.</p>

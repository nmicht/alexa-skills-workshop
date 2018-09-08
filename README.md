# Alexa Skills Workshop
Workshop to create Alexa Skills

## Pasos para crear un skill usando un ejemplo pre-armado

### 1. Crear cuentas de developer y aws en Amazon.   
https://developer.amazon.com/  
https://aws.amazon.com/    
*Nota:* La creación de cuenta en AWS requiere los datos de la tarjeta de crédito y una llamada a tu número para confirmación.

### 2. Crea un lambda usando el template de factskill  
Usaremos el servicio de lambdas de AWS para la lógica de nuestro skill, y aún mejor, usaremos una función ya creada.
 1. Ingresar a la consola de amazon https://console.aws.amazon.com/console/home
 1. Seleccionar la Region  
 Nota: De momento, solo se tiene soporte en
oregon, north virgnia, irlanda, tokio  
 1. Ir al servicio de lambdas  
 Services -> lambda
 1. Click en Create function
 1. Selecciona la opción "Serverless Application Repository" lo cual nos dará la opción de elegir de un repositorio de funciones armadas por otras personas.
 1. Selecciona "alexa-skills-kit-nodejs-factskill"
 1. Elige un nombre para tu aplicación (puedes usar el que ya viene por default)


### 3. Deployea y Testea tu Skill
 1. Click en "deploy".  
 Este proceso puede tardar un poco, a fin de cuentas, pues AWS esta haciendo toda la chamba para montar el servicio.
 1. Cuando termine, click en "Test App"
 1. Elegir de la lista de funciones, la que acaba de crear.

### 4. Configura en el lambda los roles y otros detalles
 1. El entry handler indica cual es el método a ejecutar de la función. En este caso lo mantenemos ya que ejecutaremos del archivo index, el método handler.
 1. El timeout es el tiempo que se le da de vida a la ejecución. Por default son 7secs, y esto podrías cambiarlo, pero solo te recomiendo hacerlo a menos que a mas, luego no queremos cargos indeseados.


### 5. Obten el ARN  
ARN (amazon resource name) es un identificador único para cada lambda, y con este podremos asociar a nuestro skill el lambda a ejecutar.  
 1. Para obtenerlo, en la vista de tu lambda, hasta arriba muy cerca del menú de AWS, a la derecha de los breadcumbs lo verás.
 2. Copialo.


### 6. Crear el Alexa Skill
Ahora si, a lo que nos concierne, a crear un skill de Alexa.
 1. Ingresa a https://developer.amazon.com/alexa/console/  
 1. Click en "Create Skill"
 1. Asigna un nombre a tu skill
 2. Elige el idioma para tu skills
 1. Elige el modelo, en este caso, elegirmos el modelo **custom**, con ello tendremos ya intents y utterances armados.
 1. Click en el botón superior "Create skill"
 1. Selecciona el template, que para este ejercicio elegimos "fact skill" pues nuestro skill precisamente va a arrojar datos curiosos.
 1. Click en "Choose"
 1. Listo, ya tienes un skill creado, revisa el menú superior así como las opciones en cada área para que te familiarices.

### 7. Relacionar tu skill con tu lambda
Ahora necesitamos indicar a nuestro skill con cual servicio se va a conectar para trabajar. En nuestro caso usaremos nuestro lambda, por lo cual necesitamos el ARN obtenido en el paso 5.
 1. En el menú superior elige "Build"
 1. En menu lateral izquierdo elige la opción "Endpoint"
 1. Dado elegimos un template pre-armado, ya tiene elegida la opción para utilizar un lambda.
 1. En el campo "Default Region" deberás pegar el ARN que obtuviste en el paso 5.
 1. Click en el botón superior "Save Endpoints"

### 8. Definir el nombre para invocar al skill
Para que las personas puedan invocar a tu skill debes definir un comando, o mejor
dicho, un nombre para tu skill.  
Recuerda que al final, lo que el usuario dirá será algo como:
> "Alexa, abre datos del espacio"  


donde `datos del espacio` es el nombre que se definió para invocación.
 1. Dentro de la sección de "Build", en el menú del lado izquierdo elige "Invocation"
 1. En el campo "Skill Invocation Name" define el nombre que deseas usar para que los usuarios abran tu skill.

*Nota:* Puedes leer la documentación de la manera en que Alexa entiende las invocaciones en https://developer.amazon.com/docs/custom-skills/understanding-how-users-invoke-custom-skills.html

### 9. Guadar el modelo y construirlo
Ahora ya tienes listo el modelo de tu skill, falta guardarlo y construirlo para poder comenzar a probarlo.  
 1. Click en el botón superior "Save Model"
 1. Click en el botón superior "Build Model"

*Nota 1:* El tiempo de construcción tomará tiempo.  
*Nota 2:* Debes reconstruir tu modelo cuando hagas cambios en la configuración de tu skill, tal como intents o utterances.

### 10. Probar tu skill funcionando
En el menú superior, tienes la opción "Test" dentro de la cuál tienes un simulador de Alexa. Magia!
 1. Click en el menú superior "Test"
 1. Activa los test dando click en el switch
 1. Elige el idioma en el cual has configurado tu skill
 1. Escribe, o da click en el micrófono y habla con Alexa, ejemplo:
 > "Abre datos del espacio"

*Nota 1:* Debes notar que no es necesario decir Alexa.  
*Nota 2:* El simulador no cierra la sesión a los 8 segundos tal como lo hace Alexa.

### 11. Agregar otros perfiles de idioma a tu skill
El template que estamos usando, así como la lógica para nuestro skill esta en inglés, pero podemos agregar mas idiomas.
 1. Dentro de la pestaña build, hay un dropdown para elegir idiomas, elige la opción "Language Settings".
 1. Del lado derecho, click en "Add New Language"
 1. Elige todos los idiomas que quieras activar y puedas programar para tu skill.
 1. Click en el botón superior "Save"

*Nota:* Se pueden agregar múltiples perfiles de idioma, pero para los regionalizados, solo uno por idioma. Ejemplo, solo puedes tener Spanish (MX) o Spanish (ES) pero no ambos.

### 12. Modifica tu lambda para responder distinto en cada idioma
El código pre-generado para nuestro skill de momento tiene un array con distintas frases en inglés.  
El reto ahora es agregar un arreglo con frases en español y responder con un random de ese arreglo en español.

Seguro en este momento estarás un poco confundido porque no hemos mencionado nada del ASK NodeJS SDK.

Por lo pronto, puedes ver los cambios en [index.js]( https://github.com/nmicht/alexa-skills-workshop/blob/master/index.js), lee el código, trata de entenderlo y ya verás que no es tan complejo. En el siguiente punto te explico los detalles.

---

## Cómo funcionan los skills y el ASK SDK

### 1. ¿Cómo funcionan los skills de Alexa?
El usuario le da un comando de voz a Alexa, y entonces, Alexa lo procesa convirtiendo el request en un JSON con un formato bien definido.  
Ese JSON le es enviado a tu skill desde el cuál vas a evaluar el tipo de request, cierta información extra y con ellos entregarás una respueta a Alexa.  
La respuesta que debes entregar a Alexa será también a través de un JSON con un formato definido.

Para entender los datos que el JSON contiene así como su formato puedes leer mas en https://developer.amazon.com/docs/custom-skills/request-and-response-json-reference.html

El formato de una instrucción a Alexa se podría dividir en 4 partes:
* wake word  
* launch  
* invocation name  
* utterance  

Si tomamos cada una de estas partes para armar una petición tendríamos

> "Alexa, abre datos del espacio y dime cosas de marte"

* wake word = Alexa  
* launch = abre  
* invocation name = datos del espacio  
* utterance = dime cosas de marte  

### 2. ¿Qué hace el ASK SDK?
Para facilitarnos la vida a los programadores flojos, podemos utilizar el SDK que provee de las herramientas para procesar y manipular los JSON de request y response.  

Ejemplos de algunos métodos:

**canHandle**   
Es un método que podría entenderse como un if para evaluar si puedes o no lanzar cierto handler. Esto es el previo a la funcionalidad de tu handler.  
Tu método recibe el request, que en nuestro caso se llama `handlerInput`, y al final debe devolver un booleano.  

**handle**    
Este es el método que lleva la lógica de tu código para manejar la petición del usuario.  
El método recibe el request, que en nuestro caso se llama `handlerInput` y debe devolver un response object, el cual se arma con `handlerInput.responseBuilder`.  

Puedes leer mas del SDK en https://ask-sdk-for-nodejs.readthedocs.io/en/latest/


### 10. Crea slots  
Los slots son variables que puedes usar en tus intents, ejemplo, planeta y entonces el usuario dira el nombre de un planeta, de este modo, no repites intents.  
En el intent, el slot se pone entre llaves  

### 11. Crea Slot Types  
Define la lista de tus variables con sus posibles valores, sinonimos e inclusive IDs  
No olvides asignar el slot type a tu slot



---

## Consejos para la creación de skills
`utterance - situation - response - prompt`

- siempre considerar el contexto (situation)
- evaluar a detalle la pregunta que se le hace al usuario dado de que de eso depende la pregunta
- hay que crear un guion
- dilo en voz alta
- dale la libertad al usuario de hablar como el quiera
- mapa de enunciados (utterance map) para ver todas las frases que puede decir el usuario
- consistencia, variabilidad y aprendizaje
- cosas triviales como hola, hoy es lunes, es mas facil y lindo
- tu skill siempre disponible
- ponerle formas a las situaciones y categorizarlas
- pruebas, pruebas y muchas pruebas

## Notas:  
- Se tiene una ventana de 8seg para la interacción  
- Formato de una instruccion
- Si se va a dejar la sesion abierta, siempre terminar con una pregunta
- El simulador no tiene el timer de 8 segundos, por lo que el contexto es el mismo que hace 10 mins. Para forzar hay que cerrar el test

## Mas material

- Documentacion de invocaciones https://developer.amazon.com/docs/custom-skills/understanding-how-users-invoke-custom-skills.html
- Blog https://developer.amazon.com/blogs/alexa
- Foros https://forums.developer.amazon.com  
- Feature Requests https://alexa.uservoice.com
- Tranmisiones en vivo https://www.twitch.tv/amazonalexa
- Programa para ganar un Alexa https://developer.amazon.com/es/alexa-skills-kit/alexa-developer-preview-program
- Créditos en AWS si tienes un skill publicado https://developer.amazon.com/alexa-skills-kit/alexa-aws-credits
- Linkear tu skill con Amazon https://developer.amazon.com/blogs/post/Tx3CX1ETRZZ2NPC/Alexa-Account-Linking-5-Steps-to-Seamlessly-Link-Your-Alexa-Skill-with-Login-wit

## Gracias

Gracias a Memo @memodoring y a Carlos @softwarechido por tan buen workshop.  

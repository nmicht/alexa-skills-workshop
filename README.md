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

### 8. invocation y test
poner el nombre que va a dar el usuario para la invocacion  
build model  
despues del build click en test  
encender el test y comenzar a hacer pruebas

9. Agregar mas idiomas  
Dentro de la pestaña build, hay un dropdown para elegir idiomas  
Se pueden agregar todos los perfiles de idiomas que se desean.  

10. Crea slots  
Los slots son variables que puedes usar en tus intents, ejemplo, planeta y entonces el usuario dira el nombre de un planeta, de este modo, no repites intents.  
En el intent, el slot se pone entre llaves  

11. Crea Slot Types  
Define la lista de tus variables con sus posibles valores, sinonimos e inclusive IDs  
No olvides asignar el slot type a tu slot

## Formato de una instruccion
wake word = alexa  
launch = ask, open  
invocation name = restaurant finder  
utterance = for breakfast  

## ASK SDK

canHandle   
Es un if para evaluar antes del handler  
se recomienda mucho usar el errorHandler  

handle    
la logica de codigo  
handlerInput para armar la respuesta con el responseBuilder  

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
wake word = alexa  
launch = ask, open  
invocation name = restaurant finder  
utterance = for breakfast  
- Documentacion de invocaciones https://developer.amazon.com/docs/custom-skills/understanding-how-users-invoke-custom-skills.html
- Si se va a dejar la sesion abierta, siempre terminar con una pregunta
- El simulador no tiene el timer de 8 segundos, por lo que el contexto es el mismo que hace 10 mins. Para forzar hay que cerrar el test

## Mas material

@memodoring (memo)  
@softwarechido (carlos)  

forums.developer.amazon.com  
alexa.uservoice.com

twitch.tv/amazonalexa

alexa developer preview <- google it

alexa aws credits <- google it /  100dlls al mes

developer.amazon.com/blogs/alexa

alexa accont linkin de sebasien sormacq <-- google it

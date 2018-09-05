# alexa-skills-workshop
Workshop to create Alexa Skills

## Pasos para crear un skill
1. Crear cuentas de developer y aws
developer.amazon.com  
aws.amazon.com  
La creación de AWS requiere una llamada y tu tarjeta de credito.  

2. Crea tu lambda
No olvides que solo puedes usar una de estas regiones  
oregon, north virgnia, irlanda, tokio  
services -> lambda -> create function -> serverless application repository  
Para el training usaremos: alexa-skills-kit-nodejs-factskill  

3. Deployea y Testea
Hacer click en deploy y luego en test app  

4. Configura rol y otros detalles
Se puede editar el rol, los tags, los parámetros, etc  
El handler es tu punto de inicio, es decir, el archivo y el método a ejecutar  

5. Obten el ARN
ARN es (amazon resource name), identificador único de lambda y es lo que necesitas obtener  

6. Crear el Alexa Kit
Alexa skill kit -> create skill  
custom - ingles  
tempate = fact skill  

7. Asignar tu ARN
en el endpoint (panel del lado izquierdo) tiene seleccionada lambda y en el default region, pegar el ARN  
save endpoints

8. invocation y test
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

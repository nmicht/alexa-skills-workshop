# alexa-skills-workshop
Workshop to create Alexa Skills

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


Notas:  
- Se tiene una ventana de 8seg para la interacción  
- Formato de una instruccion
wake word = alexa  
launch = ask, open  
invocation name = restaurant finder  
utterance = for breakfast  
- Documentacion de invocaciones https://developer.amazon.com/docs/custom-skills/understanding-how-users-invoke-custom-skills.html

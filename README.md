Plataphorma
===========

Meteor pet project created to teach my students the following Meteor functionality: 

* Collection's publish/subscribe 
* Deps.autorun 
* Meteor.methods/call 
* Integration of non-Meteor code in compatibility folder (HTML5 games Alien Invasion and Froot Wars)
* Usage of allow to control client access to collections

![ScreenShot](/screenshot.png)


Plataphorma offers the possibility to run 2 different HTML5 games: Alien Invasion and Froot Wars. 

On the right side of the screen the best players of each game are shown, updated in real time each time a signed in player finishes a game. If no game is selected, the best players overall are shown.

On the left side of the screen a chatroom for the current game is available. Only signed in users can post messages. If no game is selected a general chatroom is shown.

The original code of the two HTML5 games integrated in this project is available here:
* Alien Invasion: https://github.com/cykod/AlienInvasion
* Froot Wars: http://www.wrox.com/WileyCDA/WroxTitle/Professional-HTML5-Mobile-Game-Development.productCd-1118301323,descCd-DOWNLOAD.html

Bootstrap style (file bootstrap.min.css) provided by http://bootswatch.com


Running the project
-------------------

A live version of this code is running here: http://plataphorma.meteor.com

To run the project locally, clone the repo and run ```meteor``` inside it. You can see in .meteor/packages that this Meteor project uses these packages:
* ```meteor remove autopublish```
* ```meteor remove insecure```
* ```meteor add bootstrap```
* ```meteor add accounts-ui```
* ```meteor add accounts-password```

//Click en botón de juego
Para iniciar un juego se utiliza el template Template.choose_game.events en client.js donde utiliza jQuery para detectar si se pulsa o no el juego y si es afirmativo se llama al servidor con Session.set.

//Se escribe mensaje chat sin estar autenticado
Si se intenta escribir un mensaje sin estar autentificado la aplicación no te lo permite, para comprobar si lo estas o no en la linea 68 de server.js se comprueba si estas autentificado.

//Se escribe mensaje chat estando autenticado
Si se intenta escribir un mensaje estando autentificado la aplicación te lo permite, para comprobar si lo estas o no en la linea 68 de server.js se comprueba si estas autentificado. Si la respuesta es afirmativa la función Messages.allow nos permite insertar y borrar mensajes usando nuestra ID. 

//Se termina partida con puntuación alta sin estar autenticado
Se recoge las puntuaciones generadas por cada juego, en Alien Invasion (linea 367-game.js) y en froot-wars (tienen en cuenta las calorias de cada alimento). Para mostrar la puntuación de cada juego, en el caso de froot-wars dibuja en el canvas la puntuación(score) recogida(linea 116-game.js). Si el usuario no esta autenticado se comprueba en la linea 164 de client.js donde si user es distinto de true no se guarda la puntuación por lo tanto la función de la linea 10 de server.js no almacena la puntuación de ese usuario "anónimo" y por lo tanto no la publica.

//Se termina partida con puntuación alta estando autenticado
Se recoge las puntuaciones generadas por cada juego, en Alien Invasion (linea 367-game.js) y en froot-wars (tienen en cuenta las calorias de cada alimento). Para mostrar la puntuación de cada juego, en el caso de froot-wars dibuja en el canvas la puntuación(score) recogida(linea 116-game.js). Si el usuario esta autenticado se comprueba en la linea 164 de client.js donde user es true por lo tanto se guarda la puntuación y la función de la linea 10 de server.js muestra dicha puntuación si está entre las 5 mejores.

//¿Qué sale en la consola cuando te autenticas(sign in)?
En la consola te devuelve un valor current user con una clave cifrada que es el identificador único que tiene cada user dentro de la base de datos del servidor. La variable current user pasa de estar a null a dicho valor.

//¿Qué sale en la consola cuando sales(sign out)?
En la consola te devuelve un valor current user con una clave cifrada que es el identificador único que tiene cada user dentro de la base de datos del servidor. La variable current user pasa de estar de dicho valor a null.

# Ejercicio-03 - Crear aplicación Angular

Crear un proyecto node con Angular que solo contenga una página html con un Hello World. Incluir alguna imagen.

## Pasos para la realización del Ejercicio-03
Primero es necesario instalar Angular en nuesto equipo:

```sh
npm install -g @angular/cli
```
Luegos, creamos un nuevo proyecto Angular con:

```sh
ng new nombre-del-proyecto
```

Cambiar el HTML y crear un componente para mostrar.

```sh
#Generamos un nuevo componente 
ng generate component image
```
Dentro de la carpeta app, se creará una nueva carpeta con el nombre que le hemos dado anteriormente, dentro de ahí, se generará un archivo html que es donde podremos crear lo que queramos.
Para que el componente se muestre en el html principal, nos dirigimos al index.html y añadimos la linea <app-name></app-name> donde ¨name¨ será el nombre que le hemos asignado a nuestra componente.

Con esto último hemos hecho posible que el componente creado se muestre en la página principal de nuestro proyecto Angular.

Finalmente, ejecutarlo con `npm run start`, en este caso se ha añadido `npm run start -dev` que abre el navegador automáticamente y refresca si hay cambios.


<br/>
  <p align="center">
    <img src="">
  </p>
<br/>


[< Lab 01 - Introducción a Docker](../Ejercicio-02/) | [ Lab - 03 Una pequeña práctica, un "Hola Mundo" por supuesto. >](../Ejercicio-03)
<p align="center">
    <img src="../resources/header.png">
</p>

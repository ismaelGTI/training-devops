# Ejercicio-02 - Crear aplicación Angular

Crear un proyecto node con Angular que solo contenga una página html con un Hello World. Incluir alguna imagen.

## Pasos para la realización del Ejercicio-02
Primero es necesario instalar Angular en nuesto equipo:

```sh
npm install -g @angular/cli
```
Luegos, creamos un nuevo proyecto Angular con:

```sh
ng new nombre-del-proyecto
```

![Captura_1](resources/1.PNG)

Cambiar el HTML y crear un componente para mostrar.

```sh
#Generamos un nuevo componente 
ng generate component image
```
Dentro de la carpeta app, se creará una nueva carpeta con el nombre que le hemos dado anteriormente, dentro de ahí, se generará un archivo html que es donde podremos crear lo que queramos.
![Componente](resources/component-image.png)

Para que el componente se muestre en el html principal, nos dirigimos al index.html y añadimos la linea <app-name></app-name> donde ¨name¨ será el nombre que le hemos asignado a nuestra componente.

![añadir componente](resources/add-component.png)

Con esto último hemos hecho posible que el componente creado se muestre en la página principal de nuestro proyecto Angular.

Finalmente, ejecutarlo con `npm run start`, en este caso se ha añadido `npm run start -dev` que abre el navegador automáticamente y refresca si hay cambios.

![Captura_2](resources/2.PNG)


[< Ejercicio-01 - Crear aplicación Spring Boot](../Ejercicio-01/) | [ Ejercicio-03 - Dockerizar aplicaciones >](../Ejercicio-03/)

# Ejercicio-03 - Dockerizar aplicaciones

Dockerizar la aplicación creada en el ejercicio 1 y 2 y publicarlas en el Container Registry. Crear Dockerfile docker build o podman build docker run o podman run.

#### **Dockerizar la aplicación Angular**

* Instalar **[Docker](https://docs.docker.com/get-docker/)** o **[Podman](https://podman.io/getting-started/installation)**.
* Los comandos de Docker y Podman son intercambiables, simplemente escribe podman en lugar de docker para ejecutar el mismo comando. También puedes crear un alias.
  ```
  alias docker=podman
  ```
* Crear el Dockerfile correspondiente a la aplicación.
  ```dockerfile
  #Node v16
  FROM node:16-alpine as build-step 
  RUN mkdir -p /training-angular
  WORKDIR /training-angular
  COPY package.json /training-angular
  RUN npm install
  COPY . /training-angular
  RUN npm run build --prod

  FROM nginx:1.17.1-alpine
  COPY --from=build-step /training-angular/dist/hello-world /usr/share/nginx/html
  ```
* Crear el archivo .dockerignore
* Crear la imagen Docker con: 
  ```properties
  docker build -t training-angular . 
  ```
* Ejecutar el contenedor con:
  ```properties
  docker run -d -it -p LOCAL_PORT:CONTAINER_PORT training-angular
  ```
  Ejemplo: al ejecutar ```docker run -d -it -p 800:80 training-angular``` abriendo en el navegador ```localhost:800``` veríamos:  

   ![App dockerizada en ejecución](resources/3dockerized-ag-app.PNG)
   
#### **Dockerizar la aplicación Spring Boot**

* Comprobar que el bundle es correcto con Maven:
  ```properties
  mvn clean package
  java -jar target/training-spring-boot-0.0.1-SNAPSHOT.jar
    ```
  Si ejecuta correctamente en ```localhost:8080``` se puede empezar con la Dockerización

* Creación del Dockerfile:  
  Añadir un nombre final para el .jar al pom.xml:
  ```xml
  <build>
    ...
    <finalName>training-spring-boot</finalName>
    ...
  </build>
  ```
  Crear el Dockerfile:
  ```dockerfile
  FROM openjdk:11
  ADD target/training-spring-boot.jar /usr/share/training-spring-boot.jar
  CMD ["java", "-jar", "usr/share/training-spring-boot.jar"]
  ```
* Hacer build del Dockerfile:
  ```properties
  docker build -t training-spring-boot .
  ```
* Ejecutar el contenedor:
  ```properties
   docker run -tdi -p LOCAL_PORT:CONTAINER_PORT training-spring-boot
  ```
  
## Pasos para la realización del Ejercicio-03

#### **Dockerizar la aplicación Angular**

* Crear el Dockerfile correspondiente a la aplicación.

Para que funcione correctamente, deberemos cambiar el último comando "COPY" y en el path "/training-angular/dist/hello-world" deberemos modificar .../dist/hello-world por lo que nos salga en el atributo "outputPath" del archivo angular.json.
  ```dockerfile
  #Node v16
  FROM node:16-alpine as build-step 
  RUN mkdir -p /training-angular
  WORKDIR /training-angular
  COPY package.json /training-angular
  RUN npm install
  COPY . /training-angular
  RUN npm run build --prod

  FROM nginx:1.17.1-alpine
  COPY --from=build-step /training-angular/dist/hello-world /usr/share/nginx/html
  ```
  
 * Crear el archivo .dockerignore
```.dockerignore
.git
.firebase
.editorconfig
/node_modules
/e2e
/docs
.gitignore
*.zip
*.md
```
* Crear la imagen Docker con: 
  ```properties
  docker build -t training-angular . 
  ```
* Ejecutar el contenedor con:
  ```properties
  docker run -d -it -p LOCAL_PORT:CONTAINER_PORT training-angular
  ```
  Ejemplo: al ejecutar ```docker run -d -it -p 800:80 training-angular``` abriendo en el navegador ```localhost:800``` veríamos:  
  
  ![App dockerizada en ejecución](resources/3dockerized-ag-app.PNG)
  

#### **Dockerizar la aplicación Spring Boot**

* Comprobar que el bundle es correcto con Maven:

Para que funcione la segunda instrucción debemos cambiar el nombre del .jar al equivalente dentro de la carpeta /target/ de nuestro proyecto.
  ```properties
  mvn clean package
  java -jar target/training-spring-boot-0.0.1-SNAPSHOT.jar
    ```
  Si ejecuta correctamente en ```localhost:8080``` se puede empezar con la Dockerización

* Creación del Dockerfile:  
  Añadir un nombre final para el .jar al pom.xml:
  ```xml
  <build>
    ...
    <finalName>training-spring-boot</finalName>
    ...
  </build>
  ```
  Crear el Dockerfile:
  ```dockerfile
  FROM openjdk:11
  ADD target/training-spring-boot.jar /usr/share/training-spring-boot.jar
  CMD ["java", "-jar", "usr/share/training-spring-boot.jar"]
  ```
* Hacer build del Dockerfile:
  ```properties
  docker build -t training-spring-boot .
  ```
* Ejecutar el contenedor:
  ```properties
   docker run -tdi -p LOCAL_PORT:CONTAINER_PORT training-spring-boot
  ```
  
  En este ejemplo usamos los puertos 8080:8080, por lo que al buscar en el navegador "localhost:8080/helloWorld" nos aparecerá lo siguiente:
  
  ![App dockerizada en ejecución](resources/1endpoint-no-param.PNG)
  
  [< Ejercicio-02 - Crear aplicación Angular](../Ejercicio-02/) | [ Ejercicio-04 - Publicar imágenes en Container Registry >](../Ejercicio-04)

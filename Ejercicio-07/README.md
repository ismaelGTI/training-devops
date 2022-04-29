# Ejercicio-07 - Crear un helm chart

Crear un Helm Chart para cada aplicación.

Desplegar en AKS usando el Helm Chart.

# Pasos para la realización del Ejercicio 7

En primer lugar comentar que ha sido desplegado localmente en Minikube.


## Aplicación con angular

Para crear el Helm Chart, nos dirigimos a la carpeta donde queremos crearlo localmente y ejecutamos el siguiente comando:

```sh
#En training-angular se pondría el nombre del paquete helm que queremos
Helm create training-angular
```
Una vez creado el paquete, tendremos varios archivos en la carpeta por defecto, en este caso nos interesa la carpeta templates, que es donde sustituiremos los .yaml creados por defecto por los de nuestro servicio.

Seguidamente, ejecutamos minikube en local y escribimos en nuestra terminal el siguiente comando que nos permitirá instalar el helm chart anterior:

```sh
helm install training-angular training-angular/ -n training
```
*Training-angular es el nombre del pod a crear en nuestro minikube y training-angular/ el directorio de nuestro helm chart

*[NOTA] Este paso previo deberá realizarse tambien con el servicio de Spring-boot

Ya instalados los servicios, con el comando ```kubectl get pods -n training ``` (training es el namespace donde he instalado el chart) podemos ver los pods ejecutándose y si todo va bien debería verse de esta manera

![image](https://user-images.githubusercontent.com/57345200/165062585-616fb6a6-68b2-47f9-981e-9f5306d57489.png)

## Aplicación con spring-boot

```sh
#En training-spring-boot se pondría el nombre del paquete helm que queremos
Helm create training-spring-boot
```
Una vez creado el paquete, tendremos varios archivos en la carpeta por defecto, en este caso nos interesa la carpeta templates, que es donde sustituiremos los .yaml creados por defecto por los de nuestro servicio.

Seguidamente, ejecutamos minikube en local y escribimos en nuestra terminal el siguiente comando que nos permitirá instalar el helm chart anterior:

```sh
helm install training-spring-boot training-spring-boot/ -n training
```
*Training-spring-boot es el nombre del pod a crear en nuestro minikube y training-spring-boot/ el directorio de nuestro helm chart

## Testeo de ambas aplicaciones

Finalmente, ejecutamos ```kubectl --namespace training port-forward $POD_NAME 8080:$CONTAINER_PORT ``` para crear un tunel y poder acceder el servicio desplegado desde el navegador.


[< Ejercicio-06 - Desplegar en AKS ](../Ejercicio-06/) | [ Ejercicio-08 - Crear pipeline >](../Ejercicio-08)

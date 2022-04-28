# Ejercicio-08 - Crear pipeline

Crear una pipeline con las stages: Build, Docker Build, Publish Container Registry, Deploy AKS

## Pasos para la realización del Ejercicio-08

En vez de crear un pipeline como indica el ejercicio, se ha instalado en minikube un helm chart con jenkins ya que es una herramiente muy utilizado por los devops. Los pasos para instalar el packete con helm son los siguientes:

1) Nos dirigiremos a la página oficial de helm y buscaremos dentro de los charts el oficial de jenkins, cuya URL es https://artifacthub.io/packages/helm/jenkinsci/jenkins

2) Comenzamos obteniendo el Repo Info
```sh
helm repo add jenkins https://charts.jenkins.io
helm repo update
```

3) Buscamos más información del repositorio
```sh
helm search repo jenkins
```

4) Instalamos el chart en el namespace default, si queremos añadirlo a otro namespace añadiremos al comando -n [NOMBRE_NAMESPACE]
```sh
# Helm 3
helm install jenkins jenkins/jenkins
```

5) En caso de querer desinstalar el chart
```sh
helm uninstall jenkins
```

6) Seguir los pasos indicados por consola para obtener la contraseña de inicio de sesión en jenkins y hacer un tunel para poder entrar a través del navegador con la dirección 127.0.0.1:8080

[< Ejercicio-07 - Crear un helm chart](../Ejercicio-07/) | [< Ejercicio-09 - Usar librería global >](../Ejercicio-09/)


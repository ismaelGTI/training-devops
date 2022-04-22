# Ejercicio-06 - Desplegar en AKS

Desplegar en AKS

Crear yaml para el deployment Crear yaml para el configmap Crear yaml para el service Crear yaml para el ingress

### Pasos para la realización del Ejercicio 6

* Obtener credenciales de cluster de pre
  ```properties
  az login
  az aks get-credentials --resource-group=rg-training --name=aks-devops-training-pre --subscription=azure-subscription --admin
  ```
* Archivos YAML de Training Angular:
  * Deployment:
    ```yaml
    apiVersion: apps/v1 
    kind: Deployment 
    metadata: 
      name: training-angular
      namespace: training
    spec: 
      selector: 
        matchLabels: 
          app: training-angular
      replicas: 1
      template: 
        metadata: 
          labels: 
            app: training-angular 
        spec: 
          containers: 
          - name: training-angular 
            image: lorenreinad/my-repo:training-angular
            ports: 
            - containerPort: 80
          imagePullSecrets: 
            - name: acr-access 
    ```
  * Service:
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: training-angular
      namespace: training
    spec:
      type: ClusterIP
      ports:
      - name: http
        port: 80
        protocol: TCP
      selector:
        deployment-label-key: training-angular
    ```
  * Ingress:
    ```yaml
    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
      name: training-angular
      namespace: training
    spec:
      defaultBackend:
        service:
          name: training-angular
          port:
            number: 80
      rules:
      - http:
          paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: training-angular
                port:
                  number: 80
    ```
* Archivos YAML de Training Spring Boot:
  * Deployment:
    ```yaml
    apiVersion: apps/v1 
    kind: Deployment 
    metadata: 
      name: training-spring-boot
      namespace: training
    spec: 
      selector: 
        matchLabels: 
          app: training-spring-boot
      replicas: 1
      template: 
        metadata: 
          labels: 
            app: training-spring-boot
        spec: 
          containers: 
          - name: training-spring-boot 
            image: lorenreinad/my-repo:training-spring-boot
            ports: 
            - containerPort: 80 
          imagePullSecrets: 
            - name: acr-access
    ```
  * Service:
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: training-spring-boot
      namespace: training
    spec:
      type: ClusterIP
      ports:
      - name: http
        port: 80
        protocol: TCP
      selector:
        deployment-label-key: training-spring-boot
    ```
  * Ingress:
    ```yaml
    apiVersion: networking.k8s.io/v1
    kind: Ingress
    metadata:
      name: training-spring-boot
      namespace: training
    spec:
      defaultBackend:
        service:
          name: training-spring-boot
          port:
            number: 80
      rules:
      - http:
          paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: training-spring-boot
                port:
                  number: 80
    ```
  * Ejecutar los .yaml en el cluster

[< Ejercicio-05 - Desplegar clúster Kubernetes](../Ejercicio-05/) | [ Ejercicio-07 - Crear un Helm Chart >](../Ejercicio-07)

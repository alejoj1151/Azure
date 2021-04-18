# Azure

Para crear un namespace nuevo kubectl create -f aks/namespace-dev.json


### Lista de comandos

* Azure CLI
  * az acr create --resource-group NOMBRE_GRUPO_RECURSO --name ACR_NOMBRE --sku Basic --admin-enabled true
  * az acr login --name ACR_NOMBRE
  * az acr list --resource-group NOMBRE_GRUPO_RECURSO
  * az acr list --resource-group NOMBRE_GRUPO_RECURSO --query "[]. {acrLoginServer: loginServer}" --output table
  * az acr repository list --name ACR_NOMBRE --output table
  * az aks get-credentials --name NOMBRE_RECURSO_AKS --resource-group NOMBRE_GRUPO_RECURSO --subscription "ID_SUSCRIPCION_RECURSO_AKS"
  * az aks update --name NOMBRE_AKS  --resource-group NOMBRE_GRUPO_RECURSO --attach-acr ACR_NOMBRE

  Comandos de Azure ACR Repository https://docs.microsoft.com/en-us/cli/azure/acr/repository?view=azure-cli-latest

* Kubernetes
  * kubectl get nodes
  * kubectl get namespaces
  * kubectl create -f "UBICACION\NOMBRE_ARCHIVO.json"
  * kubectl create -f "UBICACION_NOMBRE_ARCHIVO_MANIFEST.yml"
  * kubectl describe pods --namespace NOMBRE_ESPACIO_TRABAJO
  * kubectl get deployments --namespace NOMBRE_ESPACIO_TRABAJO
  * kubectl get service --namespace NOMBRE_ESPACIO_TRABAJO --watch
  * kubectl --record deployment.apps/NOMBRE_DEPLOYMENT_SERVICE set image deployment.v1.apps/NOMBRE_DEPLOYMENT_SERVICE NOMBRE_IMAGEN=NUEVA_IMAGEN --namespace soluciones
  * kubectl rollout undo deployment.v1.apps/NOMBRE_DEPLOYMENT_SERVICE --namespace NOMBRE_ESPACIO_TRABAJO

* Docker
  * docker tag NOMBRE_IMAGEN ARC_LOGIN_SERVER_NOMBRE/aplicaciones/NOMBRE_IMAGEN:VERSION
  * docker images
  * docker push ARC_LOGIN_SERVER_NOMBRE/aplicaciones/NOMBRE_IMAGEN:VERSION

### Conceptos

* Azure
  * Azure Container Registry ACR: Recurso usado para almacenar las imagenes de los componentes ya dockerizados
  * Azure Kubernetes Service AKS: Servicio de Kubernetes de azure

* Kubernetes

- Controladores:

  * Deployment: Iniciar la aplicación en contenedor
  * Service: Definición puerto de la aplicación por el cual este va a salir etc
  * Ingress: Por donde salen las peticiones, asociar el path con el puerto, el host por el cual va a responder etc.

- Parámetros:

  * ClusterIP: Servicios solo son accesibles por pods/servicios que se encuentran en el mismo cluster
  * NodePort: Clientes pueden acceder a los servicios por la misma LAN. Por ejemplo servicios AKS ubicados en otros nodo pero en mismo grupo de recursos
  * LoadBalancer: Servicios accesibles a travez de internet externa

  * livenessProbe: Definición prueba que hace Kubernetes a nivel de container, sobre el path definido valida si el contenedor si este liste para recibir peticiones
  * readinessProbe: Definición prueba que hace Kubernetes a nivel de aplicación, igual que el anterior pero este solo es a nivel de aplicación

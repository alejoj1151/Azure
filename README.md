# Azure

Para crear un namespace nuevo kubectl create -f aks/namespace-dev.json


### Lista de comandos

* Azure CLI
  * az acr create --resource-group NOMBRE_GRUPO_RECURSO --name ACR_NOMBRE --sku Basic --admin-enabled true
  * az acr login --name ACR_NOMBRE
  * az acr list --resource-group NOMBRE_GRUPO_RECURSO --query "[]. {acrLoginServer: loginServer}" --output table
  * az acr repository list --name ACR_NOMBRE --output table
  * az aks get-credentials --name NOMBRE_RECURSO_AKS --resource-group NOMBRE_GRUPO_RECURSO --subscription "ID_SUSCRIPCION_RECURSO_AKS"
  * az aks update --name NOMBRE_AKS  --resource-group NOMBRE_GRUPO_RECURSO --attach-acr ACR_NOMBRE

* Kubernetes
  * kubectl get nodes
  * kubectl get namespaces
  * kubectl create -f "UBICACION\NOMBRE_ARCHIVO.json"
  * kubectl create -f "UBICACION_NOMBRE_ARCHIVO_MANIFEST.yml"
  * kubectl describe pods --namespace NOMBRE_ESPACIO_TRABAJO
  * kubectl get service --namespace NOMBRE_ESPACIO_TRABAJO --watch

* Docker
  * docker tag NOMBRE_IMAGEN ARC_LOGIN_SERVER_NOMBRE/aplicaciones/NOMBRE_IMAGEN:VERSION
  * docker images
  * docker push ARC_LOGIN_SERVER_NOMBRE/aplicaciones/NOMBRE_IMAGEN:VERSION

### Conceptos

* Azure
  * Azure Container Registry ACR: Recurso usado para almacenar las imagenes de los componentes ya dockerizados
  * Azure Kubernetes Service AKS: Servicio de Kubernetes de azure

* Kubernetes
  * ClusterIP: Servicios solo son accesibles por pods/servicios que se encuentran en el mismo cluster
  * NodePort: Clientes pueden acceder a los servicios por la misma LAN. Por ejemplo servicios AKS ubicados en otros nodo pero en mismo grupo de recursos
  * LoadBalancer: Servicios accesibles a travez de internet externa

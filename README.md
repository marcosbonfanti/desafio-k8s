# desafio-k8s
This is the basic configuration for the Kubernetes deployment of a frontend and backend app
We assume that
- This is not meant to be used in a production environment
- There is no node selection
- There is no management of DNS by Kubernetes cluster
- There is no need of a SSL connection
  
## This manifest will create
- A namespace for all the Kubernetes resources needed for the applicatio
- One Kubernetes deployment used for the frontend, with two replicas
- One Kubernetes deployment used for the backend, with two replicas and the setting of the environment variable needed for the DB connection
- One ingress controller, for expose the app, and for the traffic redirection between the frontend and the backend
- Also there is another manifest mongodb.yml, in case you want to deploy the mongo-db instance in your cluster. Note: This is not configured to persist data, for this, you should use StatefulSets instead of deployment


## Prerequisites
- A running Kubernetes cluster
- Set the environment variable in drixit-api Deployment, with the URL of your choice
  
## Deployment
- kubectl apply -f manifest.yml 
- One way to have a deployment without downtime, is with the Rolling update strategy, adding to the deployment resource 
```yaml    
    strategy:
    rollingUpdate:
      maxUnavailable: 0
    type: RollingUpdate
```    
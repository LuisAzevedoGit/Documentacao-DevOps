## namespace

organize resources in namespaces, is like a virtual cluster inside a cluster
k8 give us by default 4 namespaces

-  kubernetes dashboard: only with minikube
-  kube-system: don t create or modify, system processes, master and kubectl processes
- kube-public: publicely accessible data, a configmap, wich contains cluster information
- kube-node-lease: heartbeats of nodes, each node has asssociated lease object in namespace, determines the availability of a node
- default: resources you create are located here

kubectl crete namespace [name]

we using to simplify the oveerview, so we group the resources, structure your components
conflicts many teams, same application
resource sharing: stagin and development
resource sharing: blue/green deployment
access and resource limits on namespaces, you can define for example team A only can work with project with namespace x, a team b only work with namespace project y. we can limit the resource per namespace for example project x have this quantity of cpu, this quantity of ram,...

make it clear pls


you can t access most resources from another namespace example:
you have a configmap with namespace A, and you are working with resource with namespace B, this resources cannot access the config map, to have access you need to replicate the configmap with namespace b

you can share a service in another namespace

components wich can t be created within a namespace: volume, node
    live globally in a cluster
    can t isolate them


create components with namespace:
kubectl apply -f teste.yaml --namespace=my-namespace
or inside of configuration file (best practice)

apiVersion: v1
kind: ConfigMap
metadata:
  name: deploy-app
  namespace: my-namespace
data:
  db_url: mysql-service.database


we can change the active namespace for example if you don t change the main is defaul, but with kubens you can change example:
kubens my-namespace
kubens #to check the exists namespace and the active [green]

## Ingress
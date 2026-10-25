## 2. O que é o Kubernetes

Sistema de **código aberto** para **implantar (deploy), escalar e gerir** aplicações containerizadas, em qualquer lugar.

Simplifica a gestão de milhares de containers de forma automática: atualizações, criação de novos containers e recuperação de falhas.

O Kubernetes trabalha com **estado desejado**: nós definimos como a aplicação deve estar (por exemplo, a correr em 3 pods) e, se um falhar, o Kubernetes cria um novo para repor o estado.


high availability or no downtime
scalability or high performance
disaster recovery - backup and restore

---
Componentes of kubernetes: 
## 3. Pods

O **Pod** é a menor unidade do Kubernetes e contém um ou mais containers.

- Normalmente usa-se **1 pod com 1 container**.
- Por vezes um container depende de outro, e nesse caso colocam-se **vários containers no mesmo pod**.

como os pods comunicam entre si? cada pod tem um virtual ip. --> quandos os pods morrem, é gerado um novo com um novo ip address --> ira acontecer falhas na comunicaçao, necessario definir um ip estatico (services)

```
┌──────────── pod ────────────┐
│  ┌──────── container ─────┐ │
│  │                        │ │
│  │      nginx :80         │ │ ◄── tráfego pela porta 80
│  │                        │ │
│  └────────────────────────┘ │
└─────────────────────────────┘
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: my-container
      image: nginx:latest
      ports:
        - containerPort: 80
```

> Raramente se criam pods diretamente. No dia a dia trabalha-se com centenas ou milhares de pods, e gerir cada um à mão seria o mesmo que gerir containers diretamente. Por isso usam-se **workloads**.

---


## service and ingress:
service: permanent ip address, lifecycle of pod and service are not connected, portanto se um pod morrer o service mantem se e atribuira o mesmo ip ao pod novo.

para a aplicaçao ter acesso via browser -> necessario um external service

ingress: transforma o endereço ip da pagina em algo mais seguro (https) e adiciona o dominio, por exemplo transforma http://124.89.100.22:8080 em https://my-app-luis.pt


## ConfigMap and secrets
external configuration of your application: url, username, password
  DB_URL = mongo_db_service
Dont put password on config map --> not good practise, insecure

para isso utilizamos os secrets:
secrets: usados para guardar secret data 
  a informaçao é encoded base64
use it as environment variables or as a properties file


## data storage
if a pod da database is restored, the data is gone --> problem
to do it is using a volumes --> attached a physical drive into your database
  drive could be: local(kubernetes) ou remote (outside of the k8 cluster: cloud, on premise storage)

## deployment and sttatefulset

if a containers fails, the app will be down, and the user cannot access it. so it will generates a down time.
  to solve it, you need to replicate, you need to use deployment

deployment: blueprint for my-app pods, you create deployments not pods, abstraction off pods

portanto se um pod falhar, atraves do service e do deployment, a informaçao sera reancaminhada (loadbalancer) para outro pod ativo

atençao nao podemos usar deployments para a database containers: uma vez que os databases tem states, usamos os statefulset

stateful is used for stateful apps: elastic, mongodb, mysql,...

db are often hosted outside of k8 cluster (because using stateful is not a simple operation)


## worker machine in k8 cluster

each node has multiple pods on it
3 processes must be installed on every node
worker node do the actual work

every worker need to have installed: 
container runtime - docker for example
kubelet - interacts with both the container and node, assing resources to a pod, kubelet starts the pod with a container inside
kube proxy - forwards the requests, make sure the communications works

## master nodes

4 processes that runs on every master node

API Server: cluster gateway (gets the update, query from client), acts as a gatekeeper for authentication, only 1 entrypoint into the cluster (+security)
  some request --> api server --> validates request --> other processes --> pod 

scheduler: see the resources that are need from the new pod, after that will check the workers node resources usages, and the less busy will be choice and the pod will be create on that, So the scheduler decides on which node the new pod should be scheduled
  schedule new pod --> api server --> scheduler --> where to put the pod? --> kubelet

control manager: detects cluster state changes eg: crash on pods.
  controller manager --> scheduler --> kubelet --> pod

etcd: is the cluster brain,   cluster changes get stored in the key value store
  what resoureces are available? DId the cluster state change? is the cluster healthy?
  etcd stores key values, this key values are cluster status
    aplication data is not stored in etcd

we usualy use more than one master nodes


## example cluster set up

2 master nodes  - are more important, but process less information so need less resources(cpu, ram, storage)
3 worker nodes - need more resources

if we want to add a new master/node server:
1- get new bare server
2- intastall all the master/worker node processes
3 - add it to the cluster

## minikube and kubectl

minikube - master and node processes run on one machine, is usefull to test something without needing much resources and it will be fast, and less complex than test on production
  creates a virtuall box on your laptop
  node runs in that virtual box
  testing purposes

kubectl: to interact with cluster


## minikube hands on

start cluster:
minikube start --driver=docker (na primeira vez)

apos isso usar:
minikube start
e 
minikube stop
se quisermos recomeçar tudo de novo: minikube delete e depois minikube start --driver=docker


minikube status

replicaset is managing the replicas of a pod

lfoa@lfoa-Legion-5-15ACH6H:~/Desktop/Documentacao-DevOps$ kubectl create deployment nginx-nome --image=nginx
deployment.apps/nginx-nome created
lfoa@lfoa-Legion-5-15ACH6H:~/Desktop/Documentacao-DevOps$ kubectl get pods
NAME                         READY   STATUS    RESTARTS   AGE
nginx-nome-8cdbb694f-j2hpp   1/1     Running   0          9s
lfoa@lfoa-Legion-5-15ACH6H:~/Desktop/Documentacao-DevOps$ kubectl get replicaset
NAME                   DESIRED   CURRENT   READY   AGE
nginx-nome-8cdbb694f   1         1         1       17s
lfoa@lfoa-Legion-5-15ACH6H:~/Desktop/Documentacao-DevOps$ kubectl get deployment
NAME         READY   UP-TO-DATE   AVAILABLE   AGE
nginx-nome   1/1     1            1           28s



nginx-nome            -     8cdbb694f   -   j2hpp 
nome do deployment      id do replicaset    id do pod


layers of abstraction
deployment manages a ...
replicaset manages a ...
pod manages a ...
container

kubectl exec -it nginx-nome-8cdbb694f-j2hpp -- bin/bash  --> aceder ao terminal do pod, bom para debugging



----------------------------------------------------visto 55min de video-------------------------------------
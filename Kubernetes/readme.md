Kubernetes

deploy tradicional:

app rodavam em servidor fisico, num sistema operativo
hardware -- operating system --- app 1, app 2,...
se uma app consumir muito, pode prejudicar as outras apps.
Sem isolamento de recursos.
Desperdiçar recursos.

Para evitar que isto acontece: comprar novos servidores ---> muito caro.



maquinas virtuais: executar varias vm em uma unica cpu de um servidor fixo.
isolamento das aplicaçoes por vm
mais segurança. informaçoes de uma app nao podem ser acessadas por outras app
mellhora a utilizaçao de recursos.

hardware --> operating system --> hypervisor --> vm1 {operating system -> bin/library --> app 1, app 2}
                                             -->  vm2 {operating system -> bin/library --> app 1, app 2}


containers: 
parecidos com as vm mas tem isolamento mais flexivel, compartilha o sistema operacional entre as aplicaçoes.
sao bem mais leves que VMs.

hardware --> operating system --> container runtime --> container1 {bin/library --> app 1}
                                                     --> container2 {bin/library --> app 2}



kubernetes: simplefica o gestão(atualizar, gerar novo containers, falha nos containers.) milhares de containers  de forma automatica
é um sistema de codigo aberto para implantar (deploy), escalonar e gerenciar aplicativos conteinerizados em qualquer lugar.

o kubernetes gerencia pods.

Pod: é a menor unidade de kubernet, um pod contem um ou mais containers.
Normalmente utiliza-se um pod com um containers mas por vezes um container pode precisar de o outro e aí utilizamos um pod para n contaires.

exemplo de um arquivo yaml:

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



---pod---------------
| |-containeine--|  |
| |              |  |    
| |    nginx  80 |  |  <------ trafego pela porta 80
| |--------------|  |    
|-------------------|     

raramente criamos pods diretamente no kubernentes --> trabalhamos diariamente com centenas...milhares... de pods, pois senao nao se criava pods e fazia se a gestao diretamente nos containers portanto:

usa workloads: uma aplicaçao vai ser representada por uma workloads com varios pods associados a aplicaçao. portanto uma workloads tem um ou varios pods associados e agrupados.

uma wokrload é basicamente uma aplicaçao em execuçao.

recursos de workloads que gerencia os pods:
replicaSet -> numero de pods
deployment -> gerencia replicaset (mais utilizado)
state ful set -> explicar
daemon set -> explicar

o kubernetes trabalha por estados: por exemplo nos definimos que uma aplicaçao tem de trabalhar de tal jeito, por exemple correr em 3 pods se um falhar o kubernetes cria um novo.


um servidor em kubernetes chama se node/nos:
    um node hospeda varios pods.
    dois nodes nao podem ter o mesmo nome, cada um tem um unico nome.



----------------node--------------------|
|       pod                             |                                                               
|                   pod                 |
|       pod                             |
|                          pod          |  
|                                       |
|---------------------------------------| 


cluster um conjunto de node/nos que vao conversar entre si:
    um cluster é composto por control plane e o workernodes(onde esta as apps).
    control plnae: servidor principal que faz as gestao dos workers, pods. COmpomenentes geralmente rodam em varios computadores

utilizamos o control plane espalhados por varios computadores pois caso pare, todos os nos deixam de funcionar, logo é importante ter redundancia no control plane.

na aws usamos o Amazon EKS cluster:

EKS account: a aws gere o control plane
    api server instances
    Etcd instances

customer account:
    amazon eks add ons: karpenter, eks pod identity, kube-proxy, cni, ebs csi driver, load balancer controller, coreDNS
    ec2 instances
    supporting aws services: application loa nalancer, EBS VOlumes, network load balancer


node: kubelet, K-proxy, container runtime


hands on:

kubctl [command]

saber em qual cluster kubernete estou? em empresas é muito comum tem multi clusters.

kubcetl config current-station
    retorna o kubernet que estas a trbaalhar

get: mostra um recurso que queres ver
kubcetl get nodes
kubcetl get nodes -o wide
kubcetl get pods
kubcetl get pods -o wide


criar um pod: usar o arquivo.yaml
kubectl apply -f arquivo.yaml
se criar outro pod, temos de ter atençao ao metadata, name: nao podem ter o mesmo nome 


kubectl delete pod "nome do pod"

(estudar o que é namespaces)


alias k = kubetctl (meter uma bind que k corresponde a kubetctl --> os comandos passam a ser por exemplo: k get ...)


replica set:



apiVersion: v1
kind: ReplicaSet
metadata:
  name: my-replicaset
  labels:
    tier: my-app
spec:
  replicas: 3 #quantas replicas, 3 pods no caso 
  selector: #seleciona os pods que pertencem a label tier=my-app
    matchLabels: 
      tier: my-app
  template: #passamos o template do pod que queremos criar
    metadata:
      labels:
        tier: my-app
    spec:
      containers:
      - name: my-container
        image: nginx:latest
        ports:
        - containerPort: 80


apos isso: kubetctl apply -f "replicaset.yaml

kubetctl get rs (ver replicaset)
kubetctl delete rs "nome"
    
se fizermos delete a um pod: kubectl delete po frontend-4vgqm, o replica set vai criar um novo automaticamente


Deployment gestor de replicas set, importante para atualizar as imagens em varios pods.

kubetctl apply -f deployment.yaml

kubetctl get deployment -o wide

kubetctl describe deployment my-deployment
tmb pode ser com pods, replicasset, nodes, ... seguindo a mesma estrutura kubetctl describe "objeto" "nome do objeto"

se atualizarmos as imagens de deployment e fizermos o apply o que acontece:
ele "mata" os pods antigos e cria novos pods atualizados
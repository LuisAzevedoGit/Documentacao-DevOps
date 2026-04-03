# ☁️ AWS Notes (DevOps Path)
## 📌 Introdução

Amazon Web Services (AWS) é uma plataforma de cloud computing que permite criar, gerir e escalar infraestrutura e aplicações sem necessidade de hardware físico.

---

## 🧠 Conceitos Principais
* Região (Region): Localização geográfica dos data centers (ex: eu-west-1)
* EC2: Máquinas virtuais na cloud
* S3: Armazenamento de objetos (ficheiros)
* IAM: Gestão de utilizadores e permissões
* VPC: Rede privada na cloud
* Security Group: Firewall da AWS

---

## 🧱 Serviços Essenciais
### 💻 EC2 (Elastic Compute Cloud)
Criar servidores virtuais
Controlar CPU, RAM, disco
Aceder via SSH



### 📦 S3 (Simple Storage Service)
Armazenar ficheiros
Backup e hosting estático
Alta durabilidade


### 🔐 IAM (Identity and Access Management)
Criar utilizadores e roles
Definir permissões (policies)

👉 Boa prática:

NÃO usar root account
### 🌐 VPC (Virtual Private Cloud)
Criar rede isolada
Definir subnets, routing
### 🔥 Security Groups
Firewall da AWS
Controla portas abertas

👉 Exemplo:

22 → SSH
80 → HTTP
443 → HTTPS

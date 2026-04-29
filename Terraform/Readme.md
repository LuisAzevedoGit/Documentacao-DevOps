# 🌍 Terraform Notes (DevOps Path)

## 📌 Introdução

Terraform é uma ferramenta de **Infrastructure as Code (IaC)** que permite criar, gerir e versionar infraestrutura através de código.

Com Terraform, podes automatizar:

* Criação de servidores
* Redes
* Bases de dados
* Serviços cloud

---

## 🧠 Conceitos Principais

| Conceito | Descrição                                        |
| -------- | ------------------------------------------------ |
| Provider | Plataforma onde crias recursos (AWS, Azure, GCP) |
| Resource | Elemento da infraestrutura (VM, DB, rede)        |
| State    | Ficheiro que guarda o estado atual da infra      |
| Module   | Bloco reutilizável de código                     |
| Variable | Permite parametrizar configurações               |
| Output   | Mostra valores após deploy                       |

---

## 📦 Estrutura Básica

Ficheiros principais:

```
.
├── main.tf
├── variables.tf
├── outputs.tf
├── terraform.tfstate
```

---

## ⚙️ Comandos Essenciais

```bash
terraform init     # Inicializa o projeto
terraform plan     # Mostra o que será criado/modificado
terraform apply    # Aplica as mudanças
terraform destroy  # Remove toda a infraestrutura
```

---

## 🌐 Providers

Exemplo com AWS:

```hcl
provider "aws" {
  region = "eu-west-1"
}
```

---

## 🧩 Recursos (Resources)

Exemplo: criar uma VM

```hcl
resource "aws_instance" "vm" {
  ami           = "ami-123456"
  instance_type = "t2.micro"

  tags = {
    Name = "MinhaVM"
  }
}
```

---

## 🔄 Variáveis

```hcl
variable "instance_type" {
  default = "t2.micro"
}

resource "aws_instance" "vm" {
  ami           = "ami-123456"
  instance_type = var.instance_type
}
```

---

## 📤 Outputs

```hcl
output "public_ip" {
  value = aws_instance.vm.public_ip
}
```

---

## 🧱 Módulos (Reutilização)

```hcl
module "vpc" {
  source = "./modules/vpc"
}
```

👉 Permite reutilizar código entre projetos

---

## 🧪 Exemplo Prático

Criar um bucket S3:

```hcl
resource "aws_s3_bucket" "bucket" {
  bucket = "meu-bucket-unico-123"

  tags = {
    Name = "MeuBucket"
  }
}
```

---

## 🔄 Workflow Terraform

1. Escrever código `.tf`
2. Executar:

   ```bash
   terraform init
   terraform plan
   terraform apply
   ```
3. Terraform cria a infraestrutura automaticamente

---

## 🌐 Remote State

Evita guardar estado localmente em produção.

Exemplo com S3:

```hcl
terraform {
  backend "s3" {
    bucket = "terraform-state"
    key    = "global/state.tfstate"
    region = "eu-west-1"
  }
}
```

---

## ⚠️ Boas Práticas

* Usar **remote state**
* Nunca commitar `terraform.tfstate`
* Usar variáveis para ambientes (dev, prod)
* Executar sempre `terraform plan` antes de `apply`
* Separar código em módulos
* Versionar tudo com Git

---

## 🚀 Casos de Uso

* Provisionamento de infraestrutura cloud
* Ambientes replicáveis (dev/staging/prod)
* Automação DevOps
* Deploy multi-cloud
* Integração com CI/CD

---

## ❌ Limitações

* Não substitui ferramentas de configuração (ex: Ansible)
* Não é ideal para deploy de aplicações diretamente

---

## 🔗 Integração com CI/CD

Terraform pode ser usado com:

* GitHub Actions
* GitLab CI
* Jenkins

Exemplo simples (GitHub Actions):

```yaml
- name: Terraform Init
  run: terraform init

- name: Terraform Plan
  run: terraform plan

- name: Terraform Apply
  run: terraform apply -auto-approve
```

---

## 🧠 Resumo

Terraform permite:

* Automatizar infraestrutura
* Reduzir erros manuais
* Escalar ambientes facilmente
* Manter tudo versionado

---

## 📚 Próximos Passos

* Criar projeto AWS básico
* Aprender módulos
* Configurar remote state
* Integrar com CI/CD
* Explorar multi-environment setups

---

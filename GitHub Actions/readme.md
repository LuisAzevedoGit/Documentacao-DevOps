# ⚙️ GitHub Actions Notes (DevOps Path)

## 📌 Introdução
GitHub Actions é uma ferramenta de CI/CD integrada no GitHub que permite automatizar workflows como build, testes e deploy diretamente no repositório.

---

## 🧠 Conceitos Principais

| Conceito | Descrição |
|--------|---------|
| Workflow | Processo automatizado (ex: build + deploy) |
| Job | Conjunto de passos executados no mesmo ambiente |
| Step | Tarefa individual dentro de um job |
| Action | Bloco reutilizável (plugin) |
| Runner | Máquina onde o workflow corre |

---

## 📦 Estrutura Básica

Os workflows ficam na pasta:
.github/workflows/



### Exemplo:

```yaml
name: My First Workflow

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Run script
        run: echo "Hello DevOps"
```
## 🚀 Eventos (Triggers)
| Evento            | Função            | Exemplo            |
| ----------------- | ----------------- | ------------------ |
| push              | Quando há push    | `on: push`         |
| pull_request      | Quando há PR      | `on: pull_request` |
| schedule          | Execução agendada | cron job           |
| workflow_dispatch | Execução manual   | botão no GitHub    |


## 🧩 Jobs e Steps
```yaml
jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Step 1
        run: echo "Hello"

      - name: Step 2
        run: echo "World"
```





## 🔄 Actions (Reutilização)
Usar actions públicas:
```yaml
- name: Checkout repository
  uses: actions/checkout@v3
```
Exemplo com Node.js:
```yaml
- name: Setup Node
  uses: actions/setup-node@v3
  with:
    node-version: '18'
```
## 🌐 Variáveis e Secrets
Variáveis:
```yaml
env:
  APP_NAME: myapp
```
Secrets (seguras)

Configuradas no GitHub → Settings → Secrets
```yaml
env:
  API_KEY: ${{ secrets.API_KEY }}
```
### 🧪 Exemplo Prático
```yaml
name: Node CI

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: 18

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
```
## 🔄 Múltiplos Jobs
```yaml
jobs:
  build:
    runs-on: ubuntu-latest

  deploy:
    runs-on: ubuntu-latest
    needs: build
```
👉 needs garante ordem de execução

## ⏱️ Agendamentos (Cron)
on:
  schedule:
    - cron: "0 0 * * *"

👉 Corre todos os dias à meia-noite

## ⏪ Debug e Logs

Ver logs no GitHub:

Repo → Actions → Workflow → Job → Logs
Debug:
- name: Debug
  run: echo "Debugging..."



# 🚀 Exemplo Completo de GitHub Actions (Node.js + Docker + Deploy)

```yaml
name: Full DevOps Workflow

# Eventos que disparam o workflow
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
  workflow_dispatch: # permite disparar manualmente

jobs:
  # 1️⃣ Build e Instalação
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Cache Node Modules
        uses: actions/cache@v3
        with:
          path: ~/.npm
          key: ${{ runner.os }}-node-${{ hashFiles('package-lock.json') }}
          restore-keys: |
            ${{ runner.os }}-node-

      - name: Install Dependencies
        run: npm install

      - name: Lint Code
        run: npm run lint

      - name: Run Unit Tests
        run: npm test

  # 2️⃣ Build Docker Image
  docker_build:
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Build Docker Image
        run: |
          docker build -t myapp:latest .

      - name: Run Docker Container (Smoke Test)
        run: |
          docker run -d --name myapp_test -p 3000:3000 myapp:latest
          sleep 10
          curl -f http://localhost:3000 || exit 1
          docker stop myapp_test
          docker rm myapp_test

  # 3️⃣ Deploy Simulado
  deploy:
    runs-on: ubuntu-latest
    needs: docker_build
    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Deploy Application
        env:
          API_KEY: ${{ secrets.DEPLOY_API_KEY }}
        run: |
          echo "Simulating deploy..."
          echo "Deploy API_KEY is $API_KEY"
          # Aqui podes adicionar comandos reais, ex: scp, rsync ou AWS CLI
```
## 🔹 Explicação das Fases
### Build e Instalação
* Faz checkout do código
* Instala Node.js
* Faz cache dos node_modules para acelerar builds futuros
* Instala dependências (npm install)
* Lint e testes unitários
### Docker Build
* Constrói a imagem Docker do projeto
* Executa um container temporário para teste rápido (smoke test)
### Deploy
* Simula deploy usando uma API key armazenada nos Secrets
* Aqui é onde podes integrar AWS, Azure, GCP ou outro servidor

  
## ⚠️ Nota
* Workflows correm em ambientes temporários
* Tudo precisa ser instalado em cada execução
* Secrets nunca devem ser expostos em logs
## 🧠 Boas Práticas
* Fazer workflows pequenos e claros
* Separar jobs (build, test, deploy)
* Usar cache para acelerar builds
* Nunca fazer hardcode de secrets
* Testar workflows em branches antes da main

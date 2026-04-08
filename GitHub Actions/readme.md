# ⚙️ GitHub Actions Notes (DevOps Path)
## 📌 Introdução

GitHub Actions é uma ferramenta de CI/CD integrada no GitHub que permite automatizar workflows como build, testes e deploy diretamente no repositório.

## 🧠 Conceitos Principais

Workflow: Processo automatizado (ex: build + deploy)
Job: Conjunto de passos executados no mesmo ambiente
Step: Tarefa individual dentro de um job
Action: Bloco reutilizável (plugin)
Runner: Máquina onde o workflow corre

## 📦 Estrutura Básica

Os workflows ficam na pasta:

.github/workflows/

Exemplo de ficheiro:
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
* Evento	Função	Exemplo
* push	Quando há push	on: push
* pull_request	Quando há PR	on: pull_request
* schedule	Execução agendada	cron job
* workflow_dispatch	Execução manual	botão no GitHub

## 🧩 Jobs e Steps
jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Step 1
        run: echo "Hello"

      - name: Step 2
        run: echo "World"
## 🔄 Actions (Reutilização)

Usar actions públicas:

- name: Checkout repository
  uses: actions/checkout@v3

Exemplo com Node.js:

- name: Setup Node
  uses: actions/setup-node@v3
  with:
    node-version: '18'
## 🌐 Variáveis e Secrets
Variáveis:
env:
  APP_NAME: myapp
Secrets (seguras):

Configuradas no GitHub → Settings → Secrets

env:
  API_KEY: ${{ secrets.API_KEY }}
🧪 Exemplo Prático
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
## 🔄 Múltiplos Jobs
jobs:
  build:
    runs-on: ubuntu-latest

  deploy:
    runs-on: ubuntu-latest
    needs: build

👉 needs garante ordem de execução

## ⏱️ Agendamentos (Cron)
on:
  schedule:
    - cron: "0 0 * * *"

👉 Corre todos os dias à meia-noite

## ⏪ Debug e Logs

Ver logs no GitHub:

Repo → Actions → Workflow → Job → Logs

Adicionar debug:

- name: Debug
  run: echo "Debugging..."
## ⚠️ Nota
* Workflows correm em ambientes temporários
* Tudo precisa ser instalado em cada execução
* Secrets nunca devem ser expostos em logs
## 🧠 Boas Práticas
* Usar workflows pequenos e claros
* Separar jobs (build, test, deploy)
* Usar cache para acelerar builds
Nunca hardcode secrets
Testar workflows em branches antes de usar na main

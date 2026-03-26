# 🔧 Git Notes (DevOps Path)

## 📌 Introdução

Git é um sistema de controlo de versões distribuído, usado para gerir código, colaborar em equipa e manter histórico de alterações.

---

## 🧠 Conceitos Principais

* **Repository (Repo)**: Projeto controlado pelo Git
* **Commit**: Snapshot das alterações
* **Branch**: Linha de desenvolvimento
* **Merge**: Junção de branches
* **Remote**: Repositório remoto (ex: GitHub)

---

## 📦 Comandos Básicos

| Comando       | Função                    | Exemplo                                       |
| ------------- | ------------------------- | --------------------------------------------- |
| git init      | Criar repositório local   | git init meu-projeto                          |
| git clone     | Clonar repositório remoto | git clone https://github.com/user/projeto.git |
| git status    | Ver estado do repo        | git status                                    |
| git add       | Adicionar ficheiros       | git add script.sh                             |
| git add .     | Adicionar tudo            | git add .                                     |
| git commit -m | Criar commit              | git commit -m "mensagem"                      |

---

## 🌿 Branching

| Comando              | Função          | Exemplo                  |
| -------------------- | --------------- | ------------------------ |
| git branch           | Listar branches | git branch               |
| git branch nome      | Criar branch    | git branch feature1      |
| git checkout nome    | Mudar branch    | git checkout feature1    |
| git checkout -b nome | Criar + mudar   | git checkout -b feature2 |
| git merge            | Juntar branches | git merge feature1       |

---

## 🌐 Repositório Remoto

| Comando               | Função            | Exemplo                                                   |
| --------------------- | ----------------- | --------------------------------------------------------- |
| git remote add origin | Ligar repo remoto | git remote add origin https://github.com/user/projeto.git |
| git push              | Enviar alterações | git push -u origin main                                   |
| git pull              | Atualizar local   | git pull origin main                                      |

---

## 🧪 Exemplo Prático

```bash id="q2k9zm"
# Criar projeto
mkdir devops
cd devops

# Criar ficheiros
touch index.html style.css

# Iniciar git
git init

# Adicionar e guardar
git add .
git commit -m "add html and css files"
```

---

## 🔄 Alterações e Histórico

```bash id="y7xv2n"
# Remover ficheiro
rm index.html

# Criar novo ficheiro
touch app.js

# Ver ficheiros
ls

# Adicionar alterações
git add .

# Novo commit
git commit -m "delete html and add js"

# Ver histórico
git log
```

---

## ⏪ Voltar a um Commit

```bash id="l1w8xp"
# Mudar para commit antigo
git checkout <commit_id>
```

👉 Exemplo:

```bash id="s3v8dp"
git checkout a1b2c3d
```

---

## ⚠️ Nota

* Ao usar `git checkout` num commit antigo, entras em estado **detached HEAD**
* Para voltar ao normal:

```bash id="k0m3z9"
git checkout main
```

---

## 🧠 Boas Práticas

* Fazer commits pequenos e frequentes
* Usar mensagens claras
* Trabalhar com branches
* Fazer pull antes de push

---

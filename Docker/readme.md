# 🔧 Docker Notes (DevOps Path)

## 📌 Introdução

Docker é uma plataforma de virtualização leve usada para criar, executar e gerir aplicações em containers, garantindo consistência entre ambientes.

---

## 🧠 Conceitos Principais

* **Image**: Template com tudo necessário para correr a aplicação
* **Container**: Instância em execução de uma image
* **Dockerfile**: Ficheiro com instruções para criar uma image
* **Volume**: Persistência de dados
* **Network**: Comunicação entre containers
* **Docker Hub**: Repositorio com imagens

---

## 📦 Comandos Básicos

| Comando       | Função                   | Exemplo           |
| ------------- | ------------------------ | ----------------- |
| docker pull   | Descarregar image        | docker pull nginx |
| docker images | Listar images            | docker images     |
| docker run    | Criar e correr container | docker run nginx  |
| docker ps     | Ver containers ativos    | docker ps         |
| docker ps -a  | Ver todos os containers  | docker ps -a      |
| docker stop   | Parar container          | docker stop <id>  |
| docker rm     | Remover container        | docker rm <id>    |

---

## 🌿 Gestão de Containers

| Comando         | Função              | Exemplo                  |
| --------------- | ------------------- | ------------------------ |
| docker start    | Iniciar container   | docker start web         |
| docker restart  | Reiniciar container | docker restart web       |
| docker logs     | Ver logs            | docker logs web          |
| docker exec -it | Aceder ao container | docker exec -it web bash |
| docker inspect  | Ver detalhes        | docker inspect web       |

---

## 🌐 Imagens

| Comando      | Função        | Exemplo               |
| ------------ | ------------- | --------------------- |
| docker build | Criar image   | docker build -t app . |
| docker rmi   | Remover image | docker rmi app        |
| docker tag   | Tag de image  | docker tag app v1     |

---

## 🧪 Exemplo Prático

```bash
mkdir docker-app
cd docker-app

touch Dockerfile app.js

docker build -t myapp .
docker run -p 3000:3000 myapp
```

---

## 🔄 Alterações e Gestão

```bash
docker logs <id>
docker stop <id>
docker rm <id>
docker ps -a
```

---

## ⏪ Volumes (Persistência)

```bash
docker volume create dados
docker run -v dados:/app nginx
```

---

## ⚠️ Nota

* Containers são efémeros (dados perdem-se sem volumes)
* Images são imutáveis
* Usar `.dockerignore`

---

## 🧠 Boas Práticas

* Usar images oficiais
* Manter Dockerfiles simples
* Usar volumes para persistência
* Limpar sistema com `docker system prune`

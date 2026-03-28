🔧 Docker Notes (DevOps Path)
📌 Introdução

Docker é uma plataforma que permite criar, executar e gerir aplicações em containers. Garante consistência entre ambientes e facilita o deployment.

🧠 Conceitos Principais
Image: Template com tudo necessário para correr a aplicação
Container: Instância em execução de uma image
Dockerfile: Ficheiro com instruções para criar uma image
Volume: Persistência de dados
Network: Comunicação entre containers
📦 Comandos Básicos
Comando	Função	Exemplo
docker pull	Descarregar image	docker pull nginx
docker images	Listar images	docker images
docker run	Criar e correr container	docker run nginx
docker ps	Containers ativos	docker ps
docker ps -a	Todos os containers	docker ps -a
docker stop	Parar container	docker stop <id>
docker rm	Remover container	docker rm <id>
docker rmi	Remover image	docker rmi nginx
🏗️ Criar Containers
Comando	Função	Exemplo
docker run -d	Modo detached	docker run -d nginx
docker run -p	Mapear portas	docker run -p 8080:80 nginx
docker run --name	Nomear container	docker run --name web nginx
docker exec -it	Aceder ao container	docker exec -it web bash
📄 Dockerfile
FROM node:18

WORKDIR /app

COPY . .

RUN npm install

EXPOSE 3000

CMD ["npm", "start"]
🧪 Exemplo Prático
# Criar projeto
mkdir docker-app
cd docker-app

# Criar ficheiros
touch Dockerfile app.js

# Build da image
docker build -t myapp .

# Correr container
docker run -p 3000:3000 myapp
🔄 Gestão de Containers
# Ver logs
docker logs <id>

# Reiniciar container
docker restart <id>

# Ver detalhes
docker inspect <id>
💾 Volumes
# Criar volume
docker volume create dados

# Usar volume
docker run -v dados:/app nginx
🌐 Docker Compose
version: "3"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
docker-compose up -d
docker-compose down
⚠️ Nota
Containers são efémeros
Usar volumes para persistência
Utilizar .dockerignore
🧠 Boas Práticas
Usar images oficiais
Manter Dockerfiles simples
Fazer limpeza com docker system prune
Versionar o docker-compose

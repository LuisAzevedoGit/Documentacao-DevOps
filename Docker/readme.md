🔧 Docker Notes (DevOps Path)
📌 Introdução

Docker é uma plataforma que permite criar, executar e gerir aplicações em containers.
Garante consistência entre ambientes e facilita o deployment.

🧠 Conceitos Principais
Image: Template com tudo necessário para correr a aplicação
Container: Instância em execução de uma image
Dockerfile: Ficheiro com instruções para criar uma image
Volume: Persistência de dados
Network: Comunicação entre containers
📦 Comandos Básicos
docker pull nginx          # Descarregar image
docker images              # Listar images
docker run nginx           # Criar e correr container
docker ps                  # Containers ativos
docker ps -a               # Todos os containers
docker stop <id>           # Parar container
docker rm <id>             # Remover container
docker rmi nginx           # Remover image
🏗️ Criar Containers
docker run -d nginx                    # Modo detached
docker run -p 8080:80 nginx           # Mapear portas
docker run --name web nginx           # Nomear container
docker exec -it web bash              # Aceder ao container
📄 Dockerfile
FROM node:18

WORKDIR /app

COPY . .

RUN npm install

EXPOSE 3000

CMD ["npm", "start"]
🧪 Exemplo Prático
mkdir docker-app
cd docker-app

touch Dockerfile app.js

docker build -t myapp .
docker run -p 3000:3000 myapp
🔄 Gestão de Containers
docker logs <id>       # Ver logs
docker restart <id>    # Reiniciar container
docker inspect <id>    # Ver detalhes
💾 Volumes
docker volume create dados

docker run -v dados:/app nginx
🌐 Docker Compose
docker-compose.yml
version: "3"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
Comandos
docker-compose up -d
docker-compose down
⚠️ Nota
Containers são efémeros
Usar volumes para persistência
Utilizar .dockerignore
🧠 Boas Práticas
Usar images oficiais
Manter Dockerfiles simples
Limpar com docker system prune
Versionar o docker-compose

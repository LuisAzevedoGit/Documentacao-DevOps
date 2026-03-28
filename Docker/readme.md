🔧 Docker Notes (DevOps Path)
📌 Introdução

Docker é uma plataforma de virtualização leve que permite criar, executar e gerir aplicações em containers.
Facilita a portabilidade, consistência entre ambientes e deploy de aplicações.

🧠 Conceitos Principais
Image: Template imutável com tudo necessário para correr a app
Container: Instância em execução de uma image
Dockerfile: Ficheiro com instruções para criar uma image
Volume: Persistência de dados fora do container
Network: Comunicação entre containers
📦 Comandos Básicos
Comando	Função	Exemplo
docker --version	Ver versão	docker --version
docker pull	Descarregar image	docker pull nginx
docker images	Listar images	docker images
docker run	Criar e correr container	docker run nginx
docker ps	Listar containers ativos	docker ps
docker ps -a	Listar todos os containers	docker ps -a
docker stop	Parar container	docker stop <id>
docker rm	Remover container	docker rm <id>
docker rmi	Remover image	docker rmi nginx
🏗️ Criar Containers
Comando	Função	Exemplo
docker run -d	Modo detached	docker run -d nginx
docker run -p	Mapear portas	docker run -p 8080:80 nginx
docker run --name	Nomear container	docker run --name web nginx
docker run -v	Adicionar volume	docker run -v dados:/app nginx
docker exec -it	Aceder ao container	docker exec -it web bash
📄 Dockerfile

Exemplo de Dockerfile simples:

# Base image
FROM node:18

# Diretório de trabalho
WORKDIR /app

# Copiar ficheiros
COPY . .

# Instalar dependências
RUN npm install

# Expor porta
EXPOSE 3000

# Comando de arranque
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

Ferramenta para gerir múltiplos containers.

Exemplo docker-compose.yml:

version: "3"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
# Iniciar serviços
docker-compose up -d

# Parar serviços
docker-compose down
⚠️ Nota
Containers são efémeros (dados perdem-se sem volumes)
Evitar correr containers como root
Usar .dockerignore para otimizar builds
🧠 Boas Práticas
Usar images oficiais quando possível
Manter Dockerfiles simples e otimizados
Utilizar volumes para dados persistentes
Versionar o docker-compose.yml
Limpar containers/images não usados regularmente (docker system prune)

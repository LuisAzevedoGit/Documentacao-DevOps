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


## 🧪 Exemplo Prático
### Estrutura do projeto

docker-app/
│
├── app.js
├── package.json
└── Dockerfile

### Codigo app.js
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  res.end('Hello Docker!');
});

server.listen(3000, () => {
  console.log('Server running on port 3000');
});
```
### Dockerfile
```dockerfile
# imagem base
FROM node:18-alpine

# diretório de trabalho
WORKDIR /app

# copiar ficheiros
COPY package*.json ./

# instalar dependências
RUN npm install

# copiar restante código
COPY . .

# expor porta
EXPOSE 3000

# comando inicial
CMD ["node", "app.js"]
```
Resumo do que é feito:
Selecionamos no docker hub a imagem base: node e a versao: 18-alpine.
Mudamos o diretorio de trabalho /app
Copiamos os ficheiros package.json para instalar as dependências.
Após isso copiamos o restante codigo para o diretorio atual.
Abrimos a porta 3000
Definimos o comando de arranque do container usando CMD, que executa node app.js quando o container inicia.

## 🚀 Build e Run
```bash
docker build -t myapp . 
docker run -p 3000:3000 myapp
docker ps
```
Explicação:
* -t myapp → define o nome da imagem
* -p 3000:3000 → mapeia porta host → container

Por fim basta verificar no browser se está a correr:
* http://localhost:3000
---






---

## 🧠 Boas Práticas

* Usar images oficiais
* Manter Dockerfiles simples
* Usar volumes para persistência
* Limpar sistema com `docker system prune`

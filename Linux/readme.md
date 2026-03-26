# 🐧 Linux Notes (DevOps Path)

## 📌 Introdução

Linux é um sistema operativo baseado em Unix, amplamente utilizado em servidores, cloud computing e ambientes DevOps.

A sua arquitetura é composta por várias camadas:

**User → Shell → Kernel → Hardware**

* **User**: Interage com o sistema
* **Shell**: Interface de linha de comandos (CLI)
* **Kernel**: Gere recursos (CPU, memória, dispositivos)
* **Hardware**: Componentes físicos

---

## 🧪 Exemplo Prático

```bash
# Criar diretório
mkdir projeto

# Entrar no diretório
cd projeto

# Criar ficheiro
touch app.txt

# Listar ficheiros
ls -la
```

---

## 📁 Arquivos e Diretórios

| Comando | Função                   | Exemplo        |
| ------- | ------------------------ | -------------- |
| cd      | Mudar diretório          | cd /home       |
| ls      | Listar ficheiros         | ls -la         |
| mkdir   | Criar diretório          | mkdir pasta    |
| rmdir   | Remover diretório vazio  | rmdir pasta    |
| rm      | Remover ficheiros/pastas | rm -r pasta    |
| cp      | Copiar ficheiros         | cp a.txt b.txt |
| mv      | Mover/renomear           | mv a.txt b.txt |
| touch   | Criar ficheiro           | touch file.txt |

---

## 📄 Visualização e Manipulação

| Comando | Função            |
| ------- | ----------------- |
| cat     | Mostrar conteúdo  |
| less    | Navegar ficheiros |
| head    | Primeiras linhas  |
| tail    | Últimas linhas    |
| grep    | Procurar texto    |
| sort    | Ordenar           |
| cut     | Extrair colunas   |

---

## 🔍 Pesquisa de Ficheiros

| Comando | Função             | Exemplo               |
| ------- | ------------------ | --------------------- |
| find    | Procurar ficheiros | find . -name file.txt |
| locate  | Pesquisa rápida    | locate file.txt       |

---

## ⚙️ Processos

| Comando | Função                  |
| ------- | ----------------------- |
| ps      | Listar processos        |
| top     | Monitorizar sistema     |
| htop    | Versão melhorada do top |
| kill    | Terminar processo       |
| kill -9 | Forçar término          |

---

## 💾 Disco e Espaço

| Comando | Função               |
| ------- | -------------------- |
| df -h   | Espaço em disco      |
| du -sh  | Tamanho de diretório |

---

## 👤 Permissões e Utilizadores

| Comando | Função              |
| ------- | ------------------- |
| chmod   | Alterar permissões  |
| chown   | Alterar dono        |
| sudo    | Executar como admin |
| su      | Trocar utilizador   |
| useradd | Criar utilizador    |
| userdel | Remover utilizador  |
| passwd  | Definir password    |

---

## 🌐 Networking

| Comando    | Função                         |
| ---------- | ------------------------------ |
| ping       | Testar conectividade           |
| ip a       | Ver IP                         |
| netstat    | Ver conexões                   |
| ss         | Alternativa moderna ao netstat |
| traceroute | Ver rota                       |
| nslookup   | DNS lookup                     |
| curl       | Fazer requests HTTP            |

---

## 🛠️ Serviços e Sistema

| Comando          | Função            |
| ---------------- | ----------------- |
| systemctl start  | Iniciar serviço   |
| systemctl stop   | Parar serviço     |
| systemctl status | Ver estado        |
| reboot           | Reiniciar sistema |
| shutdown         | Desligar sistema  |

---

## 📦 Gestão de Pacotes (Debian/Ubuntu)

```bash
sudo apt update
sudo apt upgrade
sudo apt install nginx
sudo apt remove nginx
```

---

## 🧠 Conceitos Importantes

* Linux domina ambientes cloud (AWS, Azure, etc.)
* A maioria dos servidores usa Linux
* CLI é essencial para automação
* Base fundamental para DevOps

---

## 🚀 Próximos Passos (DevOps)

* Docker 🐳
* AWS ☁️
* CI/CD ⚙️
* Automação (Bash/Python)

---

## 💡 Nota Final

Estas notas fazem parte do meu percurso para DevOps, focando nos conceitos e comandos mais utilizados no dia-a-dia.

# 🐧 Linux Notes (DevOps Path)

## 📌 Introdução

Linux é um sistema operativo baseado em Unix, amplamente utilizado em servidores, cloud computing e ambientes DevOps.

Arquitetura:

**User → Shell → Kernel → Hardware**

---

## 🧪 Exemplo Prático

```bash
mkdir projeto
cd projeto
touch app.txt
ls -la
```

---

## 📁 Arquivos e Diretórios

| Comando | Função                   | Exemplo           |
| ------- | ------------------------ | ----------------- |
| cd      | Mudar diretório          | cd /home          |
| ls      | Listar ficheiros         | ls -la            |
| mkdir   | Criar diretório          | mkdir pasta       |
| rmdir   | Remover diretório vazio  | rmdir pasta       |
| rm      | Remover ficheiros/pastas | rm -r pasta       |
| cp      | Copiar ficheiros         | cp a.txt path/pasta|
| mv      | Mover/renomear           | mv a.txt path/pasta |
| touch   | Criar ficheiro           | touch file.txt    |

---

## 📄 Visualização e Manipulação

| Comando | Função           | Exemplo                    |
| ------- | ---------------- | -------------------------- |
| cat     | Mostrar conteúdo | cat file.txt               |
| less    | Navegar ficheiro | less file.txt              |
| head    | Primeiras linhas | head -n 10 file.txt        |
| tail    | Últimas linhas   | tail -n 10 file.txt        |
| grep    | Procurar texto   | grep "erro" file.txt       |
| cut     | Extrair colunas  | cut -d ":" -f1 /etc/passwd |

---

## 🔍 Pesquisa de Ficheiros

| Comando | Função             | Exemplo               |
| ------- | ------------------ | --------------------- |
| find    | Procurar ficheiros | find . -name file.txt |
| locate  | Pesquisa rápida    | locate file.txt       |

---

## ⚙️ Processos

| Comando | Função              | Exemplo      |
| ------- | ------------------- | ------------ |
| ps      | Listar processos    | ps aux       |
| top     | Monitorizar sistema | top          |
| htop    | Interface melhorada | htop         |
| kill    | Terminar processo   | kill 1234    |
| kill -9 | Forçar término      | kill -9 1234 |

---

## 💾 Disco e Espaço

| Comando | Função            | Exemplo      |
| ------- | ----------------- | ------------ |
| df -h   | Espaço em disco   | df -h        |
| du -sh  | Tamanho diretório | du -sh pasta |

---

## 👤 Permissões e Utilizadores

| Comando | Função              | Exemplo                   |
| ------- | ------------------- | ------------------------- |
| chmod   | Alterar permissões  | chmod 755 script.sh       |
| chown   | Alterar dono        | chown user:grupo file.txt |
| sudo    | Executar como admin | sudo apt update           |
| su      | Trocar utilizador   | su root                   |
| useradd | Criar utilizador    | useradd user1             |
| userdel | Remover utilizador  | userdel user1             |
| passwd  | Definir password    | passwd user1              |

---

## 🌐 Networking

| Comando    | Função                 | Exemplo                  |
| ---------- | ---------------------- | ------------------------ |
| ping       | Testar conectividade   | ping google.com          |
| ip a       | Ver IP                 | ip a                     |
| netstat    | Ver conexões           | netstat -tuln            |
| ss         | Alternativa ao netstat | ss -tuln                 |
| traceroute | Ver rota               | traceroute google.com    |
| nslookup   | DNS lookup             | nslookup google.com      |
| curl       | HTTP request           | curl https://example.com |

---

## 🛠️ Serviços e Sistema

| Comando          | Função            | Exemplo                |
| ---------------- | ----------------- | ---------------------- |
| systemctl start  | Iniciar serviço   | systemctl start nginx  |
| systemctl stop   | Parar serviço     | systemctl stop nginx   |
| systemctl status | Ver estado        | systemctl status nginx |
| reboot           | Reiniciar sistema | reboot                 |
| shutdown         | Desligar sistema  | shutdown now           |

---

## 📦 Gestão de Pacotes (Debian/Ubuntu)

```bash
sudo apt update
sudo apt upgrade
sudo apt install nginx
sudo apt remove nginx
```

---

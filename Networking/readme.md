# 🌐 Networking Notes (DevOps Path)

## 📌 Introdução

Networking é a base da comunicação entre sistemas, sendo essencial em ambientes cloud, DevOps e infraestrutura.

---

## 🧠 Conceitos Principais

| Conceito    | Descrição                             | Exemplo                 |
| ----------- | ------------------------------------- | ----------------------- |
| IP          | Identificador único de um dispositivo | 192.168.1.10            |
| Subnet Mask | Define o tamanho da rede              | /24 = 255.255.255.0     |
| Gateway     | Saída da rede para a internet         | 192.168.1.1             |
| DNS         | Traduz nomes para IPs                 | google.com → 8.8.8.8    |
| DHCP        | Atribui IPs automaticamente           | Router atribui IP ao PC |
| NAT         | Converte IP privado em público        | Rede interna → Internet |
| SSH         | Acesso remoto seguro                  | ssh user@192.168.1.10   |
| Portas      | Identificam serviços                  | HTTP:80                 |

---

## 🔌 Portas Comuns

| Serviço | Porta |
| ------- | ----- |
| HTTP    | 80    |
| HTTPS   | 443   |
| SSH     | 22    |
| DNS     | 53    |
| FTP     | 21    |
| SMTP    | 25    |

---

## 🌍 Tipos de Rede

| Tipo | Descrição              |
| ---- | ---------------------- |
| LAN  | Rede local             |
| WAN  | Rede global (internet) |
| VLAN | Segmentação lógica     |
| VPN  | Rede privada segura    |

---

## 🧱 Modelo OSI

O modelo OSI divide a comunicação em 7 camadas:

| Camada | Nome         | Função                     | Exemplo        |
| ------ | ------------ | -------------------------- | -------------- |
| 7      | Aplicação    | Interface com o utilizador | HTTP, FTP      |
| 6      | Apresentação | Formatação / encriptação   | SSL/TLS        |
| 5      | Sessão       | Gestão de sessões          | Login sessions |
| 4      | Transporte   | Comunicação fim-a-fim      | TCP, UDP       |
| 3      | Rede         | Endereçamento              | IP             |
| 2      | Data Link    | Comunicação local          | MAC            |
| 1      | Física       | Hardware                   | Cabos          |

---

## 🔁 TCP vs UDP

| Protocolo | Características     | Exemplo        |
| --------- | ------------------- | -------------- |
| TCP       | Fiável, conexão     | HTTP, HTTPS    |
| UDP       | Rápido, sem conexão | DNS, streaming |

---

## 🧪 Comandos Úteis (Linux)

| Comando    | Função               | Exemplo                  |
| ---------- | -------------------- | ------------------------ |
| ping       | Testar conectividade | ping google.com          |
| ip a       | Ver IP               | ip a                     |
| netstat    | Ver conexões         | netstat -tuln            |
| ss         | Alternativa moderna  | ss -tuln                 |
| traceroute | Ver rota             | traceroute google.com    |
| nslookup   | Resolver DNS         | nslookup google.com      |
| curl       | Fazer pedidos HTTP   | curl https://example.com |

---

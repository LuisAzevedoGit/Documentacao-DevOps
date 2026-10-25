# Prometheus

ferramenta de monitorização de código aberto, pensada para ambientes de contentores altamente dinâmicos, mas que também funciona em servidores tradicionais (bare metal). É a escolha mais comum em ambientes de contentores e microserviços.

## Porquê monitorizar?

Uma ferramenta de monitorização vigia constantemente todos os serviços e envia alertas quando algo falha, permitindo identificar problemas **antes** que afetem os utilizadores.

**Exemplos:**

- Verificar a utilização de memória e notificar o administrador quando ultrapassa, por exemplo, 70%.
- Evitar que os logs da aplicação enchem a memória do Elasticsearch: configura-se um alerta aos 50% de utilização, antes de se atingir o limite.
- Aplicação lenta porque um servidor deixou de funcionar: a monitorização deteta a falha e avisa de imediato.

**Em resumo:** o Prometheus oferece monitorização e alertas automatizados.


## Arquitetura

### Servidor Prometheus

Responsável por todo o trabalho de monitorização. É composto por:

| Componente | Função |
|---|---|
| **Armazenamento** | Base de dados de séries temporais que guarda todos os dados das métricas |
| **Recolha (Retrieval)** | Obtém (pull) as métricas das aplicações, serviços e servidores e envia-as para o armazenamento |
| **Servidor HTTP** | Aceita consultas via HTTP, feitas através da interface web do Prometheus ou do Grafana |

### Armazenamento de dados

- Disco local (HDD/SSD)
- Sistemas de armazenamento remoto
- Formato próprio de séries temporais

---

## O que é que o Prometheus monitoriza?

**Alvos (targets):** servidores Windows/Linux, servidores Apache, aplicações individuais, serviços como bases de dados.

**Que unidades são monitorizadas nesses alvos:**

- Estado do CPU
- Utilização de memória
- Espaço em disco
- Número de exceções
- Número de pedidos
- Duração dos pedidos

---

## Métricas

As métricas estão num formato de texto legível por humanos. Cada entrada contém os atributos `HELP` e `TYPE`:

- **HELP:** descrição do que a métrica representa.
- **TYPE:** o tipo da métrica. Existem 3 tipos:

| Tipo | Pergunta a que responde | Exemplos |
|---|---|---|
| **Counter** | Quantas vezes aconteceu? | Número de pedidos, número de exceções |
| **Gauge** | Qual é o valor atual? | Utilização de CPU, espaço em disco |
| **Histogram** | Quanto tempo demorou ou qual o tamanho? | Duração dos pedidos, tamanho das respostas |

---

## Exporters

O Prometheus recolhe dados (pull) a partir de endpoints HTTP, normalmente em `hostaddress/metrics`, e os dados têm de estar no formato correto.

Nem todos os alvos expõem métricas nesse formato, e é aí que entra o **exporter**: obtém as métricas do alvo, converte-as para o formato correto e expõe-nas no endpoint `/metrics`.

**Exemplo:** para monitorizar um servidor Linux, descarrega-se o **Node Exporter**.

---

## Modelo Pull

O Prometheus usa um sistema de **pull** (é ele que vai buscar os dados aos alvos). Vantagens:

- Várias instâncias do Prometheus podem recolher as mesmas métricas.
- Melhor deteção e perceção de se um serviço está ativo e a funcionar.

---

## Configuração

O ficheiro de configuração (`prometheus.yml`) tem três secções principais:

| Secção | Função |
|---|---|
| `global` | Define com que frequência o Prometheus recolhe (scrape) as métricas dos alvos |
| `rule_files` | Regras para agregar valores de métricas ou criar alertas quando uma condição é cumprida |
| `scrape_configs` | Define que recursos o Prometheus monitoriza, ou seja, os alvos |

---

## Alertmanager

Envia notificações por email, Slack, etc. Lê as regras de alerta definidas no ficheiro de configuração.

---

## PromQL

Linguagem de consulta do Prometheus (Prometheus Query Language). Usa-se na interface web do Prometheus ou no Grafana para consultar as métricas.

---

## Características do Prometheus

**Vantagens:**

- Fiável
- Autónomo (standalone e autossuficiente)
- Continua a funcionar mesmo que outras partes da infraestrutura estejam em baixo
- Não exige uma configuração complexa
- Menos complexo

**Desvantagens:**

- Difícil de escalar
- A monitorização acaba por ficar limitada. Para contornar:
  - Aumentar a capacidade do servidor Prometheus
  - Limitar o número de métricas

---

## Compatibilidade

Totalmente compatível com **Docker** e **Kubernetes**.
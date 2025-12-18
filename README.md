# 🚀 Desafio Microsserviços Node.js

Este projeto demonstra uma arquitetura de **microsserviços em Node.js com TypeScript**, projetada com foco em **escalabilidade, resiliência, observabilidade e boas práticas de engenharia de software**.

A solução é composta por **dois microsserviços independentes**, que se comunicam de forma **assíncrona via mensageria**, utilizando **infraestrutura como código (IaC)** e um stack completo de **monitoramento e tracing distribuído**.

---

## 📌 Objetivos do Projeto

- Aplicar conceitos de **arquitetura de microsserviços**
- Demonstrar comunicação **assíncrona orientada a eventos**
- Utilizar **boas práticas de observabilidade**
- Garantir **isolamento de dados** entre serviços
- Provisionar infraestrutura de forma declarativa com **Pulumi**
- Facilitar desenvolvimento e execução local com **Docker**

---

## 🧱 Arquitetura

### Visão Geral

A arquitetura é baseada em serviços independentes, cada um com seu próprio banco de dados, comunicando-se através de eventos publicados no RabbitMQ e expostos externamente por um API Gateway.

### Componentes Principais

#### Microsserviços

- **app-orders**

  - Gerencia todo o ciclo de vida de pedidos
  - Publica eventos de pedidos criados e atualizados

- **app-invoices**
  - Consome eventos de pedidos
  - Responsável pela geração e gerenciamento de faturas

#### Infraestrutura

- **Kong API Gateway**
  - Roteamento e controle de acesso
- **RabbitMQ**
  - Comunicação assíncrona entre serviços
- **PostgreSQL**
  - Banco de dados relacional (um por serviço)
- **Pulumi**
  - Infraestrutura como Código (IaC)
- **Docker & Docker Compose**
  - Padronização de ambientes

#### Observabilidade

- **OpenTelemetry**
  - Coleta de métricas, logs e traces
- **Jaeger**
  - Tracing distribuído (desenvolvimento)
- **Grafana**
  - Monitoramento e visualização de métricas

---

## 🛠️ Stack Tecnológica

- **Runtime**: Node.js 22.x
- **Linguagem**: TypeScript
- **Framework HTTP**: Fastify
- **Banco de Dados**: PostgreSQL
- **ORM**: Drizzle ORM
- **Validação**: Zod
- **Mensageria**: RabbitMQ (amqplib)
- **Observabilidade**: OpenTelemetry, Jaeger, Grafana
- **Infraestrutura**: Pulumi + AWS SDK
- **Containerização**: Docker
- **Qualidade de Código**: Biome
- **Gerenciador de Pacotes**: PNPM

---

## ▶️ Como Executar o Projeto

### Pré-requisitos

- Docker e Docker Compose
- Node.js 22.x
- PNPM

---

### Ambiente de Desenvolvimento

1. Clone o repositório:

```bash
git clone https://github.com/Luiz1nn/desafio-microsservicos-nodejs.git
cd desafio-microsservicos-nodejs
```

2. Suba a infraestrutura local:

```bash
docker-compose up -d
```

3. Configure as variáveis de ambiente:

```bash
cp app-orders/.env.example app-orders/.env
cp app-invoices/.env.example app-invoices/.env
```

4. Instale as dependências e execute os serviços:

```bash
# Microsserviço de pedidos
cd app-orders
pnpm install
pnpm dev
# Microsserviço de faturas
cd app-invoices
pnpm install
pnpm dev
```

### ☁️ Infraestrutura como Código (IaC)

A infraestrutura em nuvem é gerenciada com Pulumi, permitindo versionamento, rastreabilidade e reprodutibilidade do ambiente.

```bash
cd infra
pnpm install
pulumi up
```

### 📂 Estrutura do Projeto

```bash
.
├── app-orders/            # Microsserviço de pedidos
├── app-invoices/          # Microsserviço de faturas
├── contracts/             # Contratos compartilhados (eventos e DTOs)
├── docker/                # Configurações Docker comuns
├── infra/                 # Infraestrutura como Código (Pulumi)
├── docker-compose.yml     # Orquestração local
└── README.md
```

### 🔄 Fluxo de Comunicação

Requisições externas chegam via Kong API Gateway

O app-orders processa pedidos via API HTTP

Eventos de pedidos são publicados no RabbitMQ

O app-invoices consome esses eventos

Faturas são geradas e persistidas

Traces e métricas são coletados com OpenTelemetry

Visualização no Jaeger e Grafana

### 📊 Observabilidade

O projeto já nasce instrumentado para observabilidade, permitindo:

Tracing distribuído entre microsserviços

Monitoramento de performance

Análise de falhas e gargalos

Visibilidade ponta a ponta do fluxo de requisições

### 📄 Licença

Este projeto foi desenvolvido para fins de estudo e como desafio técnico.

![Logo](logo.png)
# Lince - Arquitetura em DevOps

O **Lince** é um sistema completo para **monitoramento, análise e gestão
de EPIs** (Equipamentos de Proteção Individual), integrando dados em
tempo real de sensores instalados em estações e ambientes operacionais.\
A plataforma permite acompanhar uso, conformidade, alertas de segurança
e comportamento operacional, garantindo maior proteção para
colaboradores e maior controle para equipes de supervisão e segurança.

Nosso objetivo é oferecer uma solução moderna e confiável para
**monitoramento inteligente de EPIs**, reduzindo riscos, prevenindo
acidentes e centralizando informações essenciais para os times de
segurança corporativa.

## Problemas que a aplicação resolve
-   Falta de visibilidade sobre **uso correto** de EPIs.
-   Dificuldade em monitorar automaticamente **violação de áreas
    restritas**.
-   Baixa eficiência em auditorias e checklists de segurança.
-   Falta de relatórios centralizados para tomada de decisão.
-   Integração limitada entre sensores físicos e aplicações
    administrativas.

## Sobre o time

- **Arthur Algate RM:560109**: Responsável pelo banco de dados e Compliance QA.  
- **Carlos Clementino RM:561187**: Responsável pelo desenvolvimento da API em Java Spring Boot e .NET, infraestrutura e práticas de DevOps, e pela integração com dispositivos IoT.  
- **Eder Silva RM:559647**: Responsável pela criação do APP mobile.

## Informações Importantes

Este repositório reúne toda a estrutura de **DevOps**, documentação de
deploy e organização dos dois projetos principais que compõem o sistema
**Lince**:

-   **Frontend** --- Aplicação Web em *React + TypeScript*\
-   **Backend** --- API em *Spring Boot Java*

Ambos foram configurados para rodar em máquinas virtuais na nuvem, com
inicialização automática e ambientes independentes.

------------------------------------------------------------------------

## 📁 Estrutura do Repositório

    /DevOps
     ├── Site/   → Site React + TypeScript
     ├── Backend/    → API Spring Boot em Java
     └── README.md

------------------------------------------------------------------------

## 🔧 Ferramentas Instaladas (Nome + Versão)

### 🖥️ Sistemas Operacionais das VMs

-   **Backend:** AlmaLinux 9 
-   **Frontend:** Windows Server 2019 Datacenter

------------------------------------------------------------------------

### 🔙 Ferramentas do Backend

-   Java **21 LTS**
-   Apache Maven **3.9.x**
-   Spring Boot **3.3.x**
-   Oracle Database **21c** (produção)
-   Git **2.43+**

### 🌐 Ferramentas do Frontend

-   Node.js **20.x LTS**
-   npm **10.x**
-   React **18.x**
-   TypeScript **5.x**
-   Vite **5.x** (ou CRA)
-   **NSSM 2.24** (rodar o frontend como serviço)

### 🧰 Ferramentas de DevOps / Infraestrutura

-   OpenSSH Server
-   NSG / Security Groups
-   RDP (Windows Server)

------------------------------------------------------------------------

## 🏷️ Informações do Projeto

### Frontend --- Lince Web

-   **Nome:** Lince Web Platform\
-   **Versão:** v1.0.0\
-   **Tecnologias:** React, TypeScript, Node.js\
-   **Deploy:** Windows Server via NSSM

### Backend --- Lince API

-   **Nome:** Lince API\
-   **Versão:** v1.0.0\
-   **Tecnologias:** Java 21, Spring Boot, Maven\
-   **Deploy:** VM Linux executando .jar

------------------------------------------------------------------------

# 🚀 Como Executar os Projetos

------------------------------------------------------------------------

## 🖥️ 1. Executando o Frontend (React + TypeScript)

### 📌 Pré-requisitos

-   Node 20+
-   npm 10+
-   NSSM instalado no Windows Server
-   Git

### 📂 Acessar o diretório

    cd Site

### 📦 Instalar dependências

    npm install

### 🏭 Build para produção

    npm run build

Isso gera a pasta **dist/**.

------------------------------------------------------------------------

## ⚙️ Rodar o Frontend como Serviço no Windows usando NSSM

### 1. Criar o serviço

    nssm install Lince-Frontend

### 2. Configurar o serviço

**Application Path:**

    C:\Program Files\nodejs\npx.cmd

**Arguments:**

    serve C:\Site\dist -p 3000 -s

**Startup directory:**

    C:\Site

### 3. Iniciar o serviço

    nssm start Lince-Frontend

### 4. Ver logs

    nssm edit Lince-Frontend

### 🌐 Site disponível em:

    http://<IP-DA-VM>:3000

------------------------------------------------------------------------

# 🖧 2. Executando o Backend (Spring Boot)

### 📌 Pré-requisitos

-   Java 21\
-   Maven 3.9+\
-   Oracle/H2\
-   VM Linux com SSH\
-   Git

### 📂 Acessar o diretório

    cd backend

### 🏗️ Gerar o .jar

    mvn clean package -DskipTests

Isso gera um arquivo como:

    target/lince-1.0.0.jar

### ▶️ Executar o Backend (profile prod com Oracle)

    java -jar target/lince-api-1.0.0.jar --spring.profiles.active=prod

### 🌐 API disponível

    http://<IP-DA-VM>:8080

------------------------------------------------------------------------

# 🔐 Regras de NSG Necessárias

## Backend (Linux)

| Porta | Função       | 
|--------|----------------|
| **8080**    | API Spring Boot       | 
| **22**    | SSH       | 


## Frontend (Windows)

| Porta | Função       | 
|--------|----------------|
| **3000**    | Site React       | 
| **3389**    | RDP       | 


------------------------------------------------------------------------

# ☁️ Fluxo de Deploy nas VMs

## Backend (Linux)

1.  Criar VM Linux\
2.  Instalar Java + Maven\
3.  Clonar repositório\
4.  Buildar o .jar\
5.  Executar com o profile desejado\
6.  Liberar porta 8080 no NSG

## Frontend (Windows)

1.  Criar VM Windows Server\
2.  Instalar Node.js\
3.  Instalar NSSM\
4.  Clonar repositório\
5.  Rodar `npm install` e `npm run build`\
6.  Configurar serviço no NSSM\
7.  Liberar porta 3000

------------------------------------------------------------------------

**Lince** — Visão total. Risco mínimo. 🦁

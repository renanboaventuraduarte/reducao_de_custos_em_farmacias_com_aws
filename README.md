# 🚀 Projeto de Redução de Custos e Modernização de Infraestrutura de Farmácia(AWS)

<p align="center">
  <img src="https://user-images.githubusercontent.com/25181517/183896132-54262f2e-6d98-41e3-8888-e40ab5a17326.png" height="120" alt="AWS">
</p>

## 📋 Informações Gerais
* **Empresa:** Abstergo Industries (Indústria Farmacêutica)
* **Responsável:** Renan Boaventura Duarte
* **Data:** 20/07/2026

---

## 📝 Introdução
Este repositório documenta o processo de implementação de ferramentas e arquitetura em nuvem na **Abstergo Industries**. O objetivo principal do projeto foi elencar serviços específicos da AWS com a finalidade de realizar uma diminuição imediata de custos de infraestrutura local, além de garantir a disponibilidade do sistema de verificação de estoque.

---

## 🏗️ Descrição do Projeto e Arquitetura

O projeto foi dividido em etapas estratégicas para garantir uma migração segura do modelo *on-premise* para uma arquitetura híbrida e *serverless* baseada em microsserviços.

### 🗺️ Visão Geral dos Serviços e Diagrama de Fluxo

| Etapa | Serviço AWS | Categoria | Função Principal |
| :--- | :--- | :--- | :--- |
| **Etapa 1** | `Amazon RDS` | Banco de Dados | Armazenamento relacional escalável dos produtos. |
| **Etapa 2** | `Amazon API Gateway` | Integração/Rede | Porta de entrada segura para requisições externas. |
| **Etapa 3** | `AWS Lambda` | Computação | Execução sob demanda de consultas ao estoque. |
| **Etapa 4.1** | `AWS IAM Auth` | Segurança/Infra | Autenticação segura do sistema de estoque externo. |
| **Etapa 4.2** | `Amazon Cognito` | Segurança/Usuário | Gerenciamento de login e acessos dos clientes. |

```text
  [ SISTEMA EXTERNO ]  (Atualização Diária)
           │
           ▼ (AWS Signature V4)
     [ AWS IAM ]
           │
           ▼
   [ API GATEWAY ] ◄─── (Token JWT) ─── [ AMAZON COGNITO ] ◄─── [ CLIENTES (Web/App) ]
           │                                                               │
           ▼                                                               │ (Acesso/Login)
     [ AWS LAMBDA ] ◄──────────────────────────────────────────────────────┘
           │
           ▼
    [ AMAZON RDS ] ─── (PostgreSQL)
```
---

## 🛠️ Detalhamento das Etapas de Implementação

### Etapa 1: Amazon Relational Database Service (RDS)
* **Descrição:** Banco de dados relacional gerenciado na nuvem.
* **Implementação:** Considerando a carga de dados que será utilizada e a necessidade de alta disponibilidade para todos os usuários, o RDS trará grande eficiência. Por ser um serviço gerenciado e com escalabilidade nativa, ele cumpre a função de maneira simples, eliminando os custos de manutenção de servidores *on-premise* locais.
* **Ação:** Criação de uma conta AWS para configurar um banco de dados **PostgreSQL**. A migração dos dados atuais será feita de forma escalável, isolada e segura.

### Etapa 2: Amazon API Gateway
* **Descrição:** Serviço de gerenciamento para criar, proteger e monitorar APIs em qualquer escala.
* **Implementação:** Atuará como a porta de entrada única da aplicação. Ele garantirá que tanto os clientes quanto os fornecedores externos acessem os dados de forma estritamente segura, evitando sobrecargas de conexões e mitigando potenciais ataques.

### Etapa 3: AWS Lambda
* **Descrição:** Serviço de computação serverless (sem servidor) baseado em execução de código por eventos.
* **Implementação:** Será implementado para executar a lógica de negócios das consultas de estoque e retornar as respostas aos clientes. Possui excelente disponibilidade e gera custos **apenas durante o tempo exato de processamento**, evitando o desperdício financeiro de manter servidores ligados 24/7.

### Etapa 4.1: AWS IAM Auth (Segurança da Infraestrutura)
* **Descrição:** Gerenciamento de identidade e controle de acesso a recursos internos da AWS.
* **Implementação:** Criação de um *IAM User* (com chaves de acesso programático restritas) para que o sistema de estoque externo tenha permissão exclusiva de escrever e atualizar dados ou disparar a Lambda de atualização. O sistema externo roda um gatilho (*trigger*) diário, autentica-se via IAM e sincroniza o estoque diretamente.

### Etapa 4.2: Amazon Cognito (Segurança do Usuário)
* **Descrição:** Gerenciamento de identidade, autenticação e login de usuários finais.
* **Implementação:** Controle de acesso dos clientes à plataforma. O fluxo ocorre quando o cliente abre o sistema e realiza o login: o Cognito valida a identidade, cria um token seguro e o envia para o API Gateway para autorizar o consumo dos dados por meio de credenciais temporárias de baixa permissão.

---

## 📈 Conclusão

A implementação destas ferramentas na **Abstergo Industries** resultará em maior organização, segurança robusta e alta disponibilidade dos dados para os clientes. A mudança do modelo tradicional de infraestrutura para serviços sob demanda garante uma redução drástica de custos imediatos e aumento da produtividade.

Como próximos passos, recomenda-se a continuidade da utilização das ferramentas implementadas, monitoramento de custos via *AWS Budgets* e a busca contínua por novas tecnologias que otimizem ainda mais os processos da empresa.

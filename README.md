# API SIGO - Backend Mobile

![Status](https://img.shields.io/badge/status-concluido-green)
![Linguagem](https://img.shields.io/badge/linguagem-TypeScript-blue)
![Backend](https://img.shields.io/badge/backend-Node.js-green)
![ORM](https://img.shields.io/badge/ORM-Prisma-blueviolet)
![Banco de Dados](https://img.shields.io/badge/database-SQLite-lightgrey)

**Sistema:** `SIGO (Sistema Integrado de Gestão de Ocorrência)`  

## Objetivo

Este projeto consiste no desenvolvimento de uma **API RESTful** para dar suporte ao aplicativo móvel do SIGO. O backend é responsável por gerenciar a autenticação dos bombeiros, o registro de ocorrências em tempo real e a sincronização de dados entre o dispositivo móvel e o banco de dados.

O projeto utiliza **Prisma ORM** para facilitar a manipulação do banco de dados **SQLite**, garantindo tipagem segura e agilidade no desenvolvimento.

## Estrutura de Dados

O sistema é baseado principalmente em duas entidades relacionais:

### 1. Usuário (User)
Representa os bombeiros/militares que utilizam o aplicativo. Contém dados como matrícula, patente (role) e credenciais de acesso.

### 2. Ocorrência (Occurrence)
Representa os chamados atendidos. Armazena dados geográficos (GPS), endereço, prioridade, descrição e status do atendimento (Aberta, Em Andamento, Finalizada).

## Tecnologias Utilizadas

- **Node.js & Express:** Framework para construção do servidor web e gerenciamento de rotas.
- **TypeScript:** Superset do JavaScript para tipagem estática e segurança no código.
- **Prisma ORM:** Ferramenta moderna para comunicação e migrações do banco de dados.
- **SQLite:** Banco de dados relacional embarcado (arquivo `dev.db`).
- **Cors:** Middleware para habilitar requisições de diferentes origens (necessário para o app mobile).

## Endpoints Implementados

Abaixo estão listadas as principais rotas disponíveis na API:

### Autenticação e Usuário

| Método | Rota               | Descrição                                 |
|--------|--------------------|---------------------------------------------|
| **POST** | `/login`           | Autentica o usuário via matrícula e senha.  |
| **GET** | `/user/profile`    | Retorna o perfil do usuário logado.         |
| **PUT** | `/user/{id}`       | Atualiza dados de contato (email, telefone).|
| **GET** | `/seed`            | Rota de desenvolvimento para criar usuário inicial (Carlos). |

### Ocorrências e Dashboard

| Método | Rota               | Descrição                                 |
|--------|--------------------|---------------------------------------------|
| **GET** | `/dashboard/stats` | Retorna estatísticas (ocorrências ativas, viaturas). |
| **POST** | `/occurrence/new`  | Registra uma nova ocorrência no sistema.    |
| **GET** | `/user/{id}/occurrences` | Lista o histórico de ocorrências de um usuário. |
| **PUT** | `/occurrence/{id}` | Edita detalhes de uma ocorrência existente. |
| **PATCH**| `/occurrence/{id}/status` | Atualiza apenas o status (ex: Finalizada). |
| **DELETE**| `/occurrence/{id}` | Remove uma ocorrência do banco de dados.    |

## Como Executar o Projeto

### Pré-requisitos

- **Node.js** (versão 18 ou superior recomendada)
- **Git**

### 1. Clonar o Repositório

```bash
git clone [https://github.com/jmtmds/sigo-backend-mobile.git](https://github.com/jmtmds/sigo-backend-mobile.git)
cd sigo-backend-mobile
```

### 2. Instalar Dependências

Instale os pacotes listados no package.json:
```bash
npm install
```
### 3. Configurar o Banco de Dados

Como o projeto utiliza Prisma com SQLite, é necessário gerar o cliente e criar o arquivo do banco

```bash

# Gera o cliente Prisma (node_modules)
npx prisma generate

# Cria as tabelas no banco de dados (dev.db)
npx prisma db push
```
### 4. Rodar o Servidor

Inicie a API em modo de desenvolvimento (utilizando ts-node):

```bash
npx ts-node src/server.ts
```

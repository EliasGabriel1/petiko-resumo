# Documentação — Projeto Petiko (Backend + Arquitetura Inicial)

## 📌 Visão Geral

O projeto foi estruturado utilizando arquitetura de microservices separando autenticação da regra de negócio principal.

Estrutura atual:

```text id="e4k8pw"
projeto-petiko/
├── auth-service/
├── todo-app/
└── docker-compose.yml
```

---

# 🧠 Arquitetura

## 🔐 auth-service

Responsável por:

* autenticação
* usuários
* geração de token
* controle de roles (admin/user)

Tecnologias:

* Laravel 11
* Sanctum
* MySQL
* Seeders

---

## 🟢 todo-app (BFF)

Responsável por:

* gerenciamento de listas
* gerenciamento de tarefas
* paginação
* busca
* regras de negócio

Tecnologias:

* Laravel 11
* MySQL

O BFF será responsável futuramente por:

* comunicação com auth-service
* validação de token
* centralização das regras
* integração com frontend Vue.js

---

# 🐳 Docker

Foi criado um ambiente com dois bancos separados para isolamento entre serviços.

## Serviços Docker

* mysql-auth
* mysql-bff
* phpmyadmin

---

## docker-compose.yml

```yaml id="r9m2tx"
services:
  mysql-auth:
    image: mysql:8.0
    container_name: mysql-auth
    restart: always

    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: auth_service

    ports:
      - "3307:3306"

  mysql-bff:
    image: mysql:8.0
    container_name: mysql-bff
    restart: always

    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: bff_service

    ports:
      - "3308:3306"

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: petiko-phpmyadmin
    restart: always

    environment:
      PMA_HOST: mysql-auth
      MYSQL_ROOT_PASSWORD: root

    ports:
      - "8080:80"
```

---

# 🚀 Subindo ambiente

```bash id="d5w7qp"
docker compose up -d
```

---

# ⚙️ Configuração do Laravel

## Auth Service `.env`

```env id="m1v4zn"
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3307
DB_DATABASE=auth_service
DB_USERNAME=root
DB_PASSWORD=root
```

---

## Todo App `.env`

```env id="a8k2rf"
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3308
DB_DATABASE=bff_service
DB_USERNAME=root
DB_PASSWORD=root
```

---

# 👤 Estrutura de usuários

Foi adicionada a coluna:

```text id="x3n7qc"
is_admin
```

na tabela `users`.

---

# 🌱 Seeders

Usuários iniciais criados automaticamente:

## Admin

```text id="v9p1tm"
admin@test.com
123456
```

## User

```text id="f6r4ky"
user@test.com
123456
```

---

# 🧩 Estrutura planejada do domínio

## 📌 todo_lists

Representa categorias/listas de tarefas.

Exemplos:

* academia
* estudos
* trabalho
* mercado

Campos:

```text id="q2m8wd"
id
user_id
title
description
created_at
```

---

## 📌 tasks

Tarefas pertencentes a uma lista.

Campos:

```text id="t7v5px"
id
todo_list_id
title
description
due_date
is_completed
created_at
```

---

# 🧠 Relacionamento

```text id="h1w9mr"
TodoList
  └── hasMany Tasks
```

Isso permite:

* múltiplas listas por usuário
* múltiplas tarefas por lista
* paginação isolada
* filtros futuros
* busca por categoria

---

# 📦 Estrutura de arquitetura planejada

```text id="p4x2zn"
app/
├── Adapters
├── Services
├── Repositories
├── Http
│   ├── Controllers
│   ├── Middleware
│   └── Requests
```

---

# 🔌 Comunicação entre serviços

Fluxo planejado:

```text id="u8r3kq"
Frontend
→ BFF (todo-app)
→ Auth Adapter
→ auth-service
```

O BFF será responsável por:

* validar tokens
* centralizar autenticação
* consumir auth-service
* proteger endpoints

---

# 📄 Funcionalidades implementadas/planejadas

## Backend atual

* microservice auth
* BFF separado
* Docker
* múltiplos bancos
* seeders
* migrations
* paginação
* estrutura em camadas

---

## Próximas implementações

### Auth Service

* login
* register
* me
* Sanctum token

---

### Todo App

* CRUD todo_lists
* CRUD tasks
* paginação
* busca
* middleware auth
* adapter auth-service

---

## Features futuras

* Events
* Jobs
* Observers
* Broadcast
* Laravel Echo
* Export CSV
* Swagger/OpenAPI
* Testes automatizados

---

# 🖥️ Executando os projetos

## Auth Service

```bash id="b6n4pt"
php artisan serve --port=8001
```

---

## Todo App

```bash id="w2m9rf"
php artisan serve --port=8000
```

---

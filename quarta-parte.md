# Documentação — Fase 4: Integração Frontend + Backend

## 📌 Objetivo da fase

Nesta etapa o foco será integrar:

```text id="u7m2qx"
Vue Frontend
↔
BFF (todo-app)
↔
Auth Service
```

A arquitetura foi planejada para seguir um padrão moderno de aplicações desacopladas utilizando microservices e BFF.

---

# 🧠 Arquitetura Atual

## 🔐 Auth Service

Responsável por:

* autenticação
* login
* usuários
* tokens
* permissões

---

## 🟢 BFF (todo-app)

Responsável por:

* centralizar regras de negócio
* consumir auth-service
* validar autenticação
* fornecer endpoints ao frontend

---

## 🎨 Frontend Vue

Responsável por:

* interface
* gerenciamento de estado
* autenticação visual
* consumo do BFF

---

# 🧱 Estrutura Frontend

Estrutura organizada visando:

* escalabilidade
* componentização
* design system
* reutilização
* separação de responsabilidades

---

## Estrutura Base

```text id="r5k8pn"
src/
├── api/
├── assets/
├── components/
├── composables/
├── layouts/
├── pages/
├── router/
├── services/
├── stores/
├── styles/
├── types/
└── utils/
```

---

# 🎨 Organização de UI

## Componentes reutilizáveis

```text id="m9v1qx"
components/
├── ui/
│   ├── Button
│   ├── Input
│   ├── Card
│   ├── Modal
│   └── Typography
```

---

## Componentes de domínio

```text id="w4r7tk"
components/
├── auth/
├── todo/
├── task/
```

---

# 🎨 Sass Architecture

Foi adicionada arquitetura Sass para padronização visual.

---

## Estrutura Sass

```text id="x8n2mp"
styles/
├── abstracts/
│   ├── _variables.scss
│   ├── _mixins.scss
│   └── _functions.scss
│
├── base/
│   ├── _reset.scss
│   ├── _global.scss
│   └── _typography.scss
│
├── components/
├── layouts/
└── main.scss
```

---

# 📌 Objetivos da arquitetura Sass

* padronização
* reutilização
* escalabilidade
* manutenção simplificada
* design system consistente

---

# 🔌 Camada de API

## Estrutura

```text id="g2p9wx"
api/
├── axios.ts
├── auth.api.ts
└── todo.api.ts
```

---

## Axios Instance

Centraliza:

* baseURL
* headers
* interceptors
* autenticação

---

## Interceptors

Será implementado interceptor para:

* adicionar Bearer Token
* tratar erros globais
* interceptar expiração de sessão

---

# 🔐 Fluxo de autenticação

Fluxo planejado:

```text id="q6m4rp"
Frontend
→ BFF
→ Auth Adapter
→ Auth Service
```

---

# 📌 Objetivos

* desacoplamento
* segurança
* centralização de regras
* facilidade futura de expansão

---

# 🧠 Gerenciamento de Estado

Será utilizado:

```text id="n1x7tv"
Pinia
```

---

## Stores planejadas

```text id="f8k2mq"
stores/
├── auth.store.ts
├── todo.store.ts
└── task.store.ts
```

---

# 🔐 Auth Store

Responsável por:

* token
* usuário autenticado
* persistência local
* logout
* sessão

---

# 🧩 Fluxo das páginas

## Login

```text id="v5p8zr"
LoginView
→ auth.store
→ auth.api
→ BFF
→ auth-service
```

---

## Dashboard

```text id="a3r1wn"
Dashboard
→ todo.api
→ BFF
→ database
```

---

# 📌 Funcionalidades desta fase

## Frontend

* login
* proteção de rotas
* persistência de sessão
* integração com API
* CRUD de listas
* CRUD de tarefas

---

## Backend

* endpoints integrados
* adapter auth-service
* autenticação
* paginação
* filtros

---

# 📄 Estrutura do domínio

## Todo Lists

Representam agrupamentos de tarefas.

Exemplos:

* estudos
* academia
* trabalho

---

## Tasks

Representam tarefas pertencentes a uma lista.

---

# 🔄 Relacionamento

```text id="t7v2kp"
TodoList
  └── hasMany Tasks
```

---

# 📌 Estratégia de UX/UI

Após integração completa:

* responsividade
* loading states
* feedback visual
* validações
* estados vazios
* animações leves

---

# 🧪 Próxima e última fase

## Testes automatizados

---

# Backend

Laravel:

* testes unitários
* testes de feature
* autenticação
* CRUD
* paginação

---

# Frontend

Vue/Vitest:

* componentes
* stores
* services
* integração

---

# 📌 Objetivo final do projeto

Demonstrar:

* arquitetura moderna
* separação de responsabilidades
* domínio técnico
* integração frontend/backend
* boas práticas
* organização escalável
* conhecimento avançado de Laravel + Vue.js

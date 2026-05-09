# Documentação Geral do Projeto — Todo App com Arquitetura BFF e Microserviços

# Visão Geral

O projeto consiste em uma aplicação de gerenciamento de tarefas (Todo App) desenvolvida utilizando arquitetura moderna baseada em microserviços e padrão BFF (Backend For Frontend).

A aplicação foi construída utilizando Laravel no backend e Vue 3 no frontend, com foco em:

* organização de código
* separação de responsabilidades
* escalabilidade
* desacoplamento entre serviços
* manutenção facilitada
* experiência moderna de desenvolvimento

Além do desenvolvimento da aplicação, foram utilizadas ferramentas de Inteligência Artificial como apoio técnico durante o projeto, auxiliando em:

* documentação técnica
* refatoração de trechos específicos do código
* revisão de estrutura
* otimização de organização de componentes e serviços
* apoio na criação e validação de Pull Requests (PRs)

O uso de IA teve como objetivo aumentar a produtividade, melhorar a padronização do código e auxiliar na qualidade geral da aplicação, mantendo todas as decisões arquiteturais e implementações sob validação e revisão manual.

---

# Arquitetura Geral

O sistema foi dividido em três partes principais:

## Frontend (Vue.js)

Responsável pela interface do usuário, renderização das telas e comunicação com o backend.

Tecnologias:

* Vue 3
* TypeScript
* Pinia
* Vue Router
* Sass

---

## BFF — Backend For Frontend (Laravel)

Camada intermediária responsável por:

* regras de negócio
* gerenciamento de tarefas
* paginação
* busca
* validações
* integração com microserviços
* abstração da comunicação externa

O frontend nunca se comunica diretamente com o microserviço de autenticação.

Fluxo:

Frontend → BFF → Auth Service

---

## Auth Service (Microserviço)

Serviço isolado responsável exclusivamente pela autenticação e gerenciamento de usuários.

Responsabilidades:

* login
* registro
* validação de token
* identificação de permissões
* gerenciamento de usuários

Tecnologias:

* Laravel
* Sanctum
* MySQL

---

# Decisão Arquitetural

Foi adotada uma arquitetura desacoplada para simular um ambiente corporativo real.

Benefícios:

* facilidade de manutenção
* escalabilidade horizontal
* independência entre serviços
* reutilização futura do serviço de autenticação
* maior organização de responsabilidades

---

# Estrutura do Backend

O backend foi organizado utilizando separação em camadas:

Controller → Service → Repository → Model

## Controllers

Responsáveis apenas por:

* receber requisições
* validar entrada
* retornar respostas

## Services

Responsáveis pelas regras de negócio da aplicação.

## Repositories

Responsáveis pelo acesso aos dados.

## Models

Responsáveis pelo mapeamento das entidades do banco.

---

# Banco de Dados

O sistema foi dividido em dois bancos independentes:

## Banco do Auth Service

Responsável pelos usuários e autenticação.

Tabelas:

* users
* personal_access_tokens

---

## Banco do BFF

Responsável pelas tarefas.

Tabelas:

* todos
* todo_types

---

# Frontend

O frontend foi estruturado visando reutilização e escalabilidade.

Estrutura:

* components
* pages
* stores
* services
* composables
* types
* styles

---

# Design System

Foi implementado um Design System simples utilizando Sass.

Foram criados:

* variáveis globais
* reset CSS
* padronização de cores
* componentes reutilizáveis
* estrutura escalável de estilos

Todos os estilos inline foram removidos dos componentes principais.

---

# Funcionalidades Implementadas

## Autenticação

* Login
* Registro
* Persistência de token
* Rotas protegidas

---

## CRUD Completo

* Criar tarefas
* Editar tarefas
* Remover tarefas
* Listar tarefas

---

## Busca

Busca dinâmica por:

* título
* descrição

---

## Paginação

Paginação backend utilizando Laravel paginate().

---

# Controle de Permissões

Foi implementado controle de acesso baseado em perfil:

## Administrador

Pode:

* criar tarefas
* editar
* remover
* listar

## Usuário comum

Pode:

* visualizar tarefas
* interagir apenas com permissões limitadas

---

# Segurança

Foram aplicadas práticas básicas de segurança:

* uso de variáveis de ambiente
* token de autenticação
* separação de serviços
* proteção de rotas
* validações backend
* validações frontend

---

# Testes

Foi iniciada a estrutura de testes automatizados utilizando PHPUnit.

Estrutura preparada para:

* testes de feature
* testes unitários
* mock de serviços externos
* validação de regras de negócio

Também foram realizadas validações de qualidade em Pull Requests, incluindo revisão de padrões de código, consistência arquitetural e apoio automatizado utilizando IA para análise de melhorias e possíveis ajustes.

---

# Docker

Foi utilizada conteinerização com Docker para facilitar:

* setup do ambiente
* padronização
* execução local
* isolamento dos bancos

---

# Documentação Visual

O projeto também possui:

* desenho arquitetural no Figma: [https://www.figma.com/design/2UnGEXdmG02lkSFWNcznbC/petiko?m=auto&t=Gsp59VRq2QqQU0s4-1](https://www.figma.com/design/2UnGEXdmG02lkSFWNcznbC/petiko?m=auto&t=Gsp59VRq2QqQU0s4-1)
* vídeo demonstrando funcionamento completo: [https://drive.google.com/file/d/1EBbZcX-nac47GPiuLS9Nx_iILyDxzcBJ/view?usp=sharing](https://drive.google.com/file/d/1EBbZcX-nac47GPiuLS9Nx_iILyDxzcBJ/view?usp=sharing)
* documentação técnica
* explicação das decisões arquiteturais

---

# Resultado Final

Ao final do desenvolvimento, o sistema apresentou:

* arquitetura desacoplada
* frontend moderno
* backend organizado
* autenticação separada
* CRUD completo
* paginação
* busca
* controle de permissões
* estrutura escalável
* preparação para futuras integrações e crescimento do sistema

O projeto foi desenvolvido buscando aproximar a implementação de um cenário corporativo real, utilizando boas práticas modernas de desenvolvimento web, além do apoio de ferramentas de Inteligência Artificial para auxiliar processos de documentação, refatoração, validação de PRs e melhoria contínua da qualidade do código.

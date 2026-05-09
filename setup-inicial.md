# Documentação — Setup do Ambiente Docker + WSL2

## Objetivo

Configurar ambiente de desenvolvimento para o projeto Laravel utilizando:

* Docker Desktop
* WSL2
* Laravel Sail
* MySQL em container

---

# Tempo gasto

## Tempo aproximado total

Entre **2h e 4h** de troubleshooting/configuração.

Grande parte do tempo foi consumida por incompatibilidades e bloqueios do ambiente Windows relacionados ao WSL2.

---

# Problemas encontrados

## 1. Docker instalado, porém daemon não iniciava

Erro inicial:

```txt id="t5dn1v"
failed to connect to the docker API
```

### Causa

O Docker Desktop dependia do WSL2, que ainda não estava configurado corretamente.

---

## 2. Virtualização não detectada

Erro:

```txt id="fc17o5"
virtualisation support wasn’t detected
```

### Verificações realizadas

* VT-x habilitado na BIOS ✔️
* Virtualização ativa no Windows ✔️

---

## 3. WSL2 sem suporte

Erro persistente:

```txt id="h0tvfd"
Não há suporte para WSL2 com a configuração atual do computador
```

---

# Diagnóstico realizado

Foram verificadas:

* Configuração da BIOS
* Hypervisor
* VirtualMachinePlatform
* WSL
* Segurança baseada em virtualização (VBS)
* Kernel do WSL2

---

# Problema principal identificado

O Windows 11 estava com:

```txt id="twvnjh"
Segurança baseada em virtualização: Executando
```

Isso fazia com que:

* o hypervisor fosse utilizado pela segurança do Windows
* bloqueando funcionamento correto do WSL2

---

# Correções aplicadas

## 1. Desativação do VBS

Foi desativado:

* Core Isolation
* Memory Integrity
* Device Guard

---

## 2. Reconfiguração do Hypervisor

Comandos utilizados:

```bash id="vt2r8j"
bcdedit /set hypervisorlaunchtype auto
```

---

## 3. Atualização manual do kernel do WSL2

Foi necessário instalar manualmente o kernel do WSL2 através do instalador oficial da Microsoft.

---

# Resultado final

Docker funcionando corretamente:

```bash id="0ljd89"
docker run hello-world
```

Resultado:

```txt id="o2smn4"
Hello from Docker!
```

---

# Motivo da escolha do Docker

O Docker foi escolhido por proporcionar:

* ambiente isolado
* facilidade de replicação
* padronização do setup
* ambiente mais próximo de produção
* integração simples com Laravel Sail

---

# Alternativa caso Docker não funcionasse

Caso o ambiente Docker continuasse incompatível, a alternativa seria utilizar:

## Stack alternativa

* XAMPP ou Laragon
* MySQL local
* PHP local
* Laravel via:

```bash id="jlwm92"
php artisan serve
```

---

# Motivo da alternativa

Essa abordagem permitiria:

* continuidade do desenvolvimento
* menor dependência do ambiente
* entrega do teste dentro do prazo

Mesmo sem Docker, os requisitos técnicos principais do teste continuariam plenamente atendidos:

* Laravel
* Vue.js
* API REST
* autenticação
* arquitetura em camadas
* eventos/jobs/observers

---

# Conclusão

Apesar do tempo elevado de setup do ambiente, o problema foi identificado e resolvido com sucesso, permitindo utilizar uma arquitetura moderna baseada em Docker + WSL2 para desenvolvimento da aplicação Laravel.

# Estruturação do Frontend

O frontend da aplicação foi iniciado utilizando Vue 3 com TypeScript, priorizando organização, reutilização de componentes e escalabilidade da aplicação.

Inicialmente foram criadas quatro views principais da aplicação, separando responsabilidades entre páginas e componentes reutilizáveis.

Os componentes semelhantes foram desacoplados e estruturados para reutilização através de props, reduzindo duplicação de código e facilitando manutenção futura.

---

# Padronização Visual

Foi adicionado Sass ao projeto para melhorar a organização dos estilos e permitir maior escalabilidade visual.

Também foi criada uma estrutura central de configuração contendo:

* variáveis globais de cores
* tipografia
* padrões visuais
* estilos reutilizáveis
* reset CSS

Essa estrutura funciona como base inicial do Design System da aplicação, acelerando futuras implementações e mantendo padronização visual entre as telas.

---

# Estrutura Técnica

Foi criada uma separação de pastas visando melhor organização do frontend:

* views
* components
* services
* stores
* composables
* styles
* types

A pasta `types` foi criada para centralizar tipagens TypeScript reutilizáveis em toda a aplicação.

---

# Integração com Backend

Antes da integração definitiva com a API, foram utilizados dados mockados para acelerar o desenvolvimento das interfaces e evitar bloqueios durante possíveis instabilidades de requisição.

Após a integração, as requisições foram implementadas utilizando services dedicadas, mantendo separação entre lógica de interface e comunicação HTTP.

Toda a comunicação com a API foi desenvolvida utilizando TypeScript tipado, reduzindo retrabalho e facilitando manutenção futura.

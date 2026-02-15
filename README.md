# Sistema de Gestão de Usuários e Acessos (Admin Dashboard)

Gestão simples de usuários, onde os usuários podem ver os dados com permissão limitada e o gestor tem total controle dos dados tendo acesso ao CRUD completo!

Essa aplicação é fullstack, com autenticação, validação de dados, tratamento de erros, tipada para garantir uma segurança para futuras versões, conteinerizada para rodar em qualquer ambiente. No Backend temos um CRUD completo para servir o Frontend, tendo a validação correta das permissões de cada usuário. No Frontend utilizamos de componentes reutilizáveis para melhor flexibilidade e escalabilidade.

Esse projeto tem as seguintes stacks separadas por aplicação:

- Backend
  - Node.js
  - Express
  - TypeScript
  - Sequelize
  - SQL(MYSQL)
  - JWT
  - Docker (FRONTEND + API + DB)

- Frontend:
  - React
  - TypeScript
  - HTML / CSS
  - Fetch

O objetivo principal do projeto é o pleno funcionamento de seus requisitos, em sua primeira versão não contemplará assuntos como:

- Testes automatizados (opcional depois)
- Microserviços
- Clean Architecture hardcore
- CQRS
- Mensageria
- UI perfeita

**Obs: Em versões futuras poderá ser discutido a melhoria da aplicação com os assuntos citados acima**

## Diagramas

Contamos com 3 diagramas essenciais, para facilitarmos o entendimento de algumas partes, optamos por poucos diagramas justamente para não ficarmos preso a isso

### Diagrama de Fluxo

![Diagrama de Fluxo](./Diagramas/Diagrama_Fluxo.png)

### Diagrama ER

![Diagrama ER](./Diagramas/DER.png)

### Diagrama arquitetural

![Diagrama Arquitetural](./Diagramas/Diagrama_Arquitetural.png)

## Docker

Vamos ter dois Dockerfiles gerando um a imagem do backend e outro a do frontend, a imagem para o DB é utilizada a mysql:8.4 para garantirmos que nada quebre futuramente com atualizações. Todos os containers são orquestrados via **Docker Compose**, escolhido por ser mais simples, ideal para projeto pequeno, porém, para projetos maiores e que necessitam de escala alta é interessante considerar soluções como Kubernetes.

### Diagrama de Containers

![Diagrama de Containers](./Diagramas/Diagrama-de-containers.png)

### Volumes:

Apenas um volume para o database chamado `mysql_data`, persiste dados de `/var/lib/mysql`, onde o mysql guarda todos os dados do DB

`docker compose up`

1. Cria o volume mysql_data (se não existir)

2. Cria o container

3. Conecta o volume ao caminho /var/lib/mysql

4. Tudo que o MySQL salvar ali vai para o volume

5. Se o container morrer → volume continua existindo

### Redes virtuais

Foram criadas duas redes a `virtual-front` e `virtual-db`

## Backend

### Configurações iniciais

- Utilizando importação e exportação com ES Module
- Para rodar o node em desenvolvimento use `npm run dev`, está rodando com tsx para hot-reload

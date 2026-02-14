#-------------------------- Primeira Etapa --------------------------
FROM node:24-alpine AS builder
# Nesta usamos o node para instalação e contrução da aplicação
WORKDIR /frontend
# Definimos o diretorio de frontend, ou seja, já estamos dentro dele, daqui o caminho deve ser relativo a ele
COPY package*.json ./
# Copiamos todo o package para que possamos instalar as dependências contidas nele
RUN npm ci
# Precisamos instalar as dependências sem alterar nada e nem instalar algo a mais por isso usamos Continuos Integrations(CI) ao invés de install
COPY . .
# Com as dependências instaladas, copiamos o restante da aplicação para dentro do container
RUN npm run build
# Com tudo certo, rodamos o build, onde o vite faz o resto, construindo o estático para podermos servi-lo por meio do NGINX

#-------------------------- Segunda Etapa --------------------------
FROM nginx:mainline-alpine
# Usamos o NGINX para servir nossas páginas
COPY --from=builder /frontend/dist /usr/share/nginx/html
# Aqui usamos multi-stage para seguir com o build e copiamos o estático no arquivo html do nginx para que as requisições http encontre nossas páginas
COPY nginx.config /etc/nginx/conf.d/default.conf
# Copiamos as configs para que possamos renderizar outras páginas que não estão em html, pois se usamos react router as outras rotas são via script, ou seja
# não estão em html
EXPOSE 80

CMD [ "nginx", "-g", "daemon off;" ]
# Por fim, já estamos usando a imagem de nginx e podemos utilizar o comando nginx -g daemon off
# Esse -g é para podermos definir globalmente
# daemon off; é para que possamos utilizar no nginx na linha de frente, por padrão o nginx vai para background por estar com daemon true
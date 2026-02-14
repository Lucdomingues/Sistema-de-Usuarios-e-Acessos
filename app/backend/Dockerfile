# ------------------ Etapa 1 - Construção ------------------
FROM node:24.13.1-alpine AS building-stage

WORKDIR /backend

COPY package*.json ./

RUN npm ci

COPY . .

RUN npm run build

# ------------------ Etapa 2 - Produção ------------------

FROM node:24.13.1-alpine

WORKDIR /backend

COPY package*.json ./

RUN npm ci --omit=dev

COPY --from=building-stage /backend/dist ./dist

EXPOSE 3000

CMD [ "node", "dist/server.js" ]

# npm ci, usa exatamente o package-lock.json, Não altera nada, Instala mais rápido, É determinístico, Se lock estiver inconsistente → falha

# --omit=dev omite das devDependencies, que não são necessáris em produção
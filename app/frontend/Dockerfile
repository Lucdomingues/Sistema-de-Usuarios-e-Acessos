#-------------------------- Primeira Etapa --------------------------
FROM node:24-alpine AS builder

WORKDIR /frontend

COPY package*.json .

RUN npm ci


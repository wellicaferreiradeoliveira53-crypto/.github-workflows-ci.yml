# --- ESTÁGIO 1: Build & Dependências ---

FROM node:20-alpine AS builder

WORKDIR /APP

COPY package*.json ./

RUN npm install

COPY . .

# --- ESTÁGIO 2: Imagem de Produção Leve ---

FROM node:20-alpine

WORKDIR /APP

COPY package*.json ./

RUN npm ci --only=production

COPY --from=builder /APP/server.js ./server.js

USER node

EXPOSE 3000

CMD ["node", "server.js"]
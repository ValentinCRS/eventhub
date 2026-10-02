# =========================
# Development
# =========================
FROM node:22-alpine AS development

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 5000

CMD ["npm", "run", "dev"]


# =========================
# Production dependencies
# =========================
FROM node:22-alpine AS production

WORKDIR /app

COPY package*.json ./

RUN npm install --omit=dev

COPY src ./src

EXPOSE 5000

CMD ["npm", "start"]
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

FROM node:20-alpine
WORKDIR /app
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
COPY package*.json ./
RUN npm install --only=production && npm cache clean --force
COPY --from=builder /app/src ./src
USER appuser
ENV NODE_ENV=production
EXPOSE 3003
CMD ["node", "src/index.js"]
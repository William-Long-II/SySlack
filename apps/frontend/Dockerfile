# ---- Builder Stage ----
FROM node:22-alpine3.22 AS builder
WORKDIR /app

COPY apps/frontend/package*.json ./
RUN npm install

COPY apps/frontend .
RUN npm run build

# ---- Production Stage ----
FROM node:22-alpine3.22
WORKDIR /app

COPY --from=builder /app/public ./public
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/package.json ./package.json

ENV NODE_ENV=production
EXPOSE 3000
CMD ["npm", "start"]

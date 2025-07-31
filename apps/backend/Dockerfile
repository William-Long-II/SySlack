# ---- Builder Stage ----
FROM node:22-alpine3.22 AS builder
WORKDIR /app

COPY apps/backend/package*.json ./
RUN npm install

COPY apps/backend .
RUN npm run build

# ---- Production Stage ----
FROM node:22-alpine3.22
WORKDIR /app

COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
COPY apps/backend/package.json ./

ENV NODE_ENV=production
CMD ["node", "dist/main"]

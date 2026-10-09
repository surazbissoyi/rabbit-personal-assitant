# Railway service: API (Fastify backend)
# Build context is the repo root. Start command runs DB migrations first
# (idempotent), then boots the server.
FROM node:20-slim

RUN corepack enable && corepack prepare pnpm@9.12.0 --activate

WORKDIR /app
COPY . .
RUN pnpm install --frozen-lockfile
RUN pnpm -r --filter=./packages/* build
RUN pnpm --filter @agent/api build

ENV NODE_ENV=production

CMD ["sh", "-c", "pnpm --filter @agent/db migrate:prod && node apps/api/dist/index.js"]

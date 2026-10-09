# Railway service: Web (Next.js control center)
# Build context is the repo root. NEXT_PUBLIC_API_URL must be set as a build
# variable since Next.js bakes it in at build time.
FROM node:20-slim

RUN corepack enable && corepack prepare pnpm@9.12.0 --activate

WORKDIR /app
COPY . .

ARG NEXT_PUBLIC_API_URL
ENV NEXT_PUBLIC_API_URL=${NEXT_PUBLIC_API_URL}

RUN pnpm install --frozen-lockfile
RUN pnpm -r --filter=./packages/* build
RUN pnpm --filter @agent/web build

ENV NODE_ENV=production

CMD ["sh", "-c", "cd apps/web && node node_modules/next/dist/bin/next start -p ${PORT:-3000} -H 0.0.0.0"]

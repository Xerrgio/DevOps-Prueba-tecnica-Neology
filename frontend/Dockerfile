FROM node:20-alpine AS build

WORKDIR /app

COPY package*.json ./

RUN npm ci --no-audit --no-fund

COPY . ./

RUN npm run build

FROM nginxinc/nginx-unprivileged:1.27-alpine

LABEL org.opencontainers.image.title="parking-frontend"
LABEL org.opencontainers.image.description="Neology Parking Frontend"
LABEL org.opencontainers.image.version="1.0.0"

COPY nginx.conf /etc/nginx/conf.d/default.conf

COPY --from=build --chown=101:101 \
    /app/dist/parking-frontend/browser \
    /usr/share/nginx/html

EXPOSE 8080

HEALTHCHECK --interval=30s --timeout=5s --start-period=15s --retries=3 \
  CMD wget -q -O /dev/null http://localhost:8080/ || exit 1
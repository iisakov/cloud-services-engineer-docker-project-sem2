FROM node:20-alpine AS builder

WORKDIR /app

ENV NODE_OPTIONS=--openssl-legacy-provider

COPY package*.json ./
RUN npm ci --no-audit --no-fund

COPY . .

RUN which npm || apk add --no-cache nodejs npm

RUN npm run build

RUN npm ci --only=production --no-audit --no-fund

FROM nginxinc/nginx-unprivileged:1.25-alpine

COPY --from=builder --chown=101:101 /app/dist /usr/share/nginx/html

COPY nginx.conf /etc/nginx/conf.d/default.conf

RUN rm -rf /etc/nginx/conf.d/default.conf.bak \
    && find /usr/share/nginx/html -name "*.map" -delete

USER 101

EXPOSE 80
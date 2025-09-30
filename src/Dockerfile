FROM node:20-alpine
WORKDIR /app

# Build-time: define quais deps instalar
ARG BUILD_ENV=production
ENV NODE_ENV=$BUILD_ENV

COPY package*.json ./
RUN if [ "$BUILD_ENV" = "production" ]; then \
      if [ -f package-lock.json ]; then npm ci --omit=dev; else npm install --omit=dev; fi; \
    else \
      if [ -f package-lock.json ]; then npm ci; else npm install; fi; \
    fi

COPY . .
USER node
EXPOSE 8080
CMD ["node","server.js"]
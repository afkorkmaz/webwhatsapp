FROM node:20-alpine AS build
WORKDIR /app

# Build aşamasında devDependencies gerekli (vite plugin, vue-tsc, vb.)
ENV NODE_ENV=development
ENV npm_config_production=false
ENV NPM_CONFIG_PRODUCTION=false

COPY package.json package-lock.json* ./
RUN npm ci --include=dev

COPY . .

ARG VITE_API_BASE
ARG VITE_WS_URL
ENV VITE_API_BASE=$VITE_API_BASE
ENV VITE_WS_URL=$VITE_WS_URL

RUN npm run build

FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
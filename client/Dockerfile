# client/Dockerfile
# 1) build stage
FROM node:18-alpine AS build
WORKDIR /app
COPY client/package*.json ./
RUN npm ci
COPY client/ ./
RUN NODE_OPTIONS=--openssl-legacy-provider npm run build

# 2) production stage: nginx serves static and proxies sockets
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html

# copy custom nginx config that will proxy /socket.io to the server container
COPY client/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

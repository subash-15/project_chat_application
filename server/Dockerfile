
FROM node:18-alpine
WORKDIR /app

# install deps (uses package.json from server/)
COPY server/package*.json ./
RUN npm ci --only=production

# copy server code
COPY server/ ./

ENV NODE_ENV=production
EXPOSE 5000

# use npm start (repo uses npm start per README)
CMD ["node","index.js"]

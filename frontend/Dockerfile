# stage build
FROM node:16-alpine
WORKDIR /app

COPY . .
RUN npm i
RUN npm audit fix
RUN npm run build


# stage run
FROM node:16-alpine
WORKDIR /app

COPY --from=0 /app/package*.json ./
RUN npm ci --production --ignore-scripts
RUN npm audit fix
COPY --from=0 /app/build ./

EXPOSE 3000
CMD ["node", "./index.js"]
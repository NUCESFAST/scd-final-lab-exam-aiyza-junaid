
FROM node:14

WORKDIR /i211145_backend

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3145

CMD ["node", "index.js"]

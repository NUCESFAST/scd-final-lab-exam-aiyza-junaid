FROM node:14 AS build

WORKDIR /i211145_frontend

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

FROM node:14

RUN npm install -g serve

WORKDIR /i211145_frontend

COPY --from=build /i211145_frontend/build /i211145_frontend/build

EXPOSE 1145

CMD ["serve", "-s", "build", "-l", "1145"]

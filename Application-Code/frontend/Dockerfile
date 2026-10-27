FROM dhi.io/alpine-base:3.24-alpine3.24-dev AS build

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

FROM dhi.io/node:24

WORKDIR /app

COPY --from=build /usr/src/app/build ./build
COPY --from=build /usr/src/app/package*.json ./

RUN npm install --production

EXPOSE 3000

CMD ["npm","start"]

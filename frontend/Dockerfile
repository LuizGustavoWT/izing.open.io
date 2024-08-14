FROM node:18-alpine

WORKDIR /front

COPY package*.json ./

RUN npm i -g @quasar/cli

RUN npm install

COPY . . 

RUN quasar build -P -m pwa

CMD ["quasar", "run", "serve"]
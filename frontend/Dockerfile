FROM node:18-alpine

WORKDIR /front

COPY package*.json ./

RUN npm install --force

RUN npm i -g @quasar/cli

RUN npx update-browserslist-db@latest

COPY . . 

RUN npm run build

COPY docker-entrypoint.sh .
RUN chmod +x docker-entrypoint.sh
ENTRYPOINT ["./docker-entrypoint.sh"]
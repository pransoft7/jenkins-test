FROM node:14

WORKDIR /home/bezkoder-app

COPY package*.json .

RUN npm install

COPY . .

CMD npm start

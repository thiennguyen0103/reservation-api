FROM node:alpine AS developement

WORKDIR /usr/src/app

COPY package.json ./

RUN npm install -g npm
RUN npm install

COPY . .

RUN npm run build

FROM node:alpine AS production

ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

WORKDIR /usr/src/app

COPY package.json ./

RUN npm install -g npm
RUN npm install --prod

COPY --from=developement /usr/src/app/dist ./dist

CMD [ "node", "dist/apps/auth/main" ]

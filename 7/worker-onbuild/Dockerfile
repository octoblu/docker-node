FROM octoblu/node:7-alpine-gyp

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

ONBUILD COPY package.json yarn.lock /usr/src/app/
ONBUILD RUN yarn --no-progress --no-emoji --production && yarn cache clean
ONBUILD COPY . /usr/src/app

CMD [ "node", "command.js" ]

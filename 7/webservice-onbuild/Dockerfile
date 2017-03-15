FROM octoblu/node:7-alpine-gyp

EXPOSE 80
HEALTHCHECK CMD curl --fail http://localhost:80/healthcheck || exit 1


RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

ONBUILD ARG NPM_TOKEN
ONBUILD RUN if [ ! -z ${NPM_TOKEN} ]; then echo '//registry.npmjs.org/:_authToken=${NPM_TOKEN}' > .npmrc; fi
ONBUILD COPY package.json yarn.lock /usr/src/app/
ONBUILD RUN yarn --no-progress --no-emoji --production && yarn cache clean
ONBUILD COPY . /usr/src/app

CMD [ "node", "command.js" ]

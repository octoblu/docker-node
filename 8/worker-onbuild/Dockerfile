FROM octoblu/node:8-alpine-gyp

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

ONBUILD ARG NPM_TOKEN
ONBUILD RUN if [ -n "${NPM_TOKEN}" ]; then echo '//registry.npmjs.org/:_authToken=${NPM_TOKEN}' > .npmrc; fi
ONBUILD COPY package.json yarn.lock /usr/src/app/
ONBUILD RUN yarn --no-progress --no-emoji --production && yarn cache clean
ONBUILD COPY . /usr/src/app

CMD [ "node", "--max-executable-size=256", "--max-old-space-size=256", "--max-semi-space-size=2", "command.js" ]

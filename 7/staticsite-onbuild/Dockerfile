FROM octoblu/node:7-alpine-gyp

RUN apk add --no-cache curl nginx jq bash

EXPOSE 80
HEALTHCHECK CMD curl --fail http://localhost:80/healthcheck || exit 1

RUN mkdir -p /usr/share/nginx/html

COPY nginx.conf /etc/nginx/nginx.conf
COPY conf.d/* /etc/nginx/conf.d/
COPY write-version /usr/local/bin/write-version

ONBUILD WORKDIR /usr/src/app
ONBUILD COPY package.json yarn.lock bower.json /usr/src/app/
ONBUILD RUN write-version
ONBUILD RUN yarn --no-progress --no-emoji --production && yarn cache clean
ONBUILD COPY . /usr/src/app
ONBUILD RUN yarn run build
ONBUILD RUN cp -rfp /usr/src/app/dist/* /usr/share/nginx/html/
ONBUILD RUN rm -rf /usr/src/app/*
ONBUILD COPY package.json yarn.lock bower.json /usr/src/app/

CMD ["nginx", "-g", "daemon off;"]

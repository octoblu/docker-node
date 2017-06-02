FROM node:8-alpine
MAINTAINER Octoblu <docker@octoblu.com>

ENV NPM_CONFIG_LOGLEVEL error

RUN apk add --no-cache alpine-sdk python-dev

RUN npm --silent install node-gyp -g \
  && node-gyp install \
  && npm cache --force clean 

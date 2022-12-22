FROM node:14.17
WORKDIR /home/genfanad

USER root

RUN mkdir /home/node/.npm-global
ENV PATH=/home/node/.npm-global/bin:$PATH
ENV NPM_CONFIG_PREFIX=/home/node/.npm-global

COPY . /home/genfanad

RUN npm i
USER node

CMD ["node", "server.js"]

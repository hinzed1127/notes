FROM node:12-stretch

USER node

WORKDIR /home/node/src

COPY --chown=node:node . .

RUN npm ci

# https://btholt.github.io/complete-intro-to-containers/expose
EXPOSE 3000

CMD ["node", "index.js"]

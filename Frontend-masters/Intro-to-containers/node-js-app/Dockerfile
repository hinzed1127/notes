FROM node:12-stretch

# lets us switch from the root user (default). node:12-stretch provides node for us, otherwise we'd have to do this with bash commands
USER node

# Ex of adding our own user
# RUN useradd -ms /bin/bash dan

# example uses code instead of src, but this is more conventional
WORKDIR /home/node/src

# COPY index.js index.js
COPY --chown=node:node index.js .

CMD ["node", "index.js"]

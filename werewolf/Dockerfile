FROM alpine/git:v2.32.0 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/AlecM33/Werewolf.git /app
WORKDIR /app
RUN git checkout 0754ffffb2c2e69e00c38ebee7165603821e9b2e
RUN rm -rf .git


FROM node:17.9.0-alpine
COPY --from=clone /app /app
WORKDIR /app
RUN npm install
RUN npm audit fix
RUN sed -i "/const secure = require('express-force-https');/d; /app.use(secure);/d" server.js
EXPOSE 5000
CMD ["node", "server.js"]

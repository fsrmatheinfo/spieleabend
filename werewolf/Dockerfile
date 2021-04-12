FROM alpine/git:v2.26.2 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/AlecM33/Werewolf.git /app
WORKDIR /app
RUN git checkout 0754ffffb2c2e69e00c38ebee7165603821e9b2e
RUN rm -rf .git


FROM node:14.15.1-stretch
COPY --from=clone /app /app
WORKDIR /app
RUN npm install
RUN npm audit fix
EXPOSE 5000
CMD ["node", "server.js"]

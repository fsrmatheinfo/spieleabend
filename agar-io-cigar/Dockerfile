FROM alpine/git:v2.32.0 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/opcon/Cigar2.git /app
WORKDIR /app
RUN git checkout ced18851717d2b18eef9e8e367e35cf399c50d6c
RUN rm -rf .git


FROM node:16.13.0-alpine3.11
EXPOSE 3000
ENV NPM_CONFIG_LOGLEVEL info
WORKDIR /app
COPY --from=clone /app/app/package*.json /app/
RUN yarn install --ignore-engines
COPY --from=clone /app/app /app
ARG OGAR_SERVER="localhost:443"
RUN sed -i "s/localhost:443/$OGAR_SERVER/g; s/Local 443/Spieleabend/g" web/index.html
CMD ["node", "webserver.js"]

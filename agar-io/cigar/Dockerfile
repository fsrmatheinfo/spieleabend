FROM alpine/git:v2.26.2 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/opcon/Cigar2.git /app
WORKDIR /app
RUN git checkout ced18851717d2b18eef9e8e367e35cf399c50d6c
RUN rm -rf .git


FROM node:8.17.0-alpine3.11
EXPOSE 3000
ENV NPM_CONFIG_LOGLEVEL info
WORKDIR /app
COPY --from=clone /app/app/package*.json /app/
RUN yarn install
COPY --from=clone /app/app /app
ARG OGAR_SERVER="localhost:443"
RUN sed -i s/localhost:443/$OGAR_SERVER/g web/index.html && \
    sed -i s/'Local 443'/Spieleabend/g web/index.html
CMD ["yarn", "start"]

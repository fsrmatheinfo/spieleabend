FROM alpine/git:v2.26.2 AS clone
RUN git config --global advice.detachedHead false
RUN git clone --branch "v1.0" --depth 1 https://github.com/fsrmatheinfo/spieleabend-battleship.git /app
WORKDIR /app


FROM alpine:3.12.1 AS replace
COPY --from=clone /app /app
WORKDIR /app
RUN sed -i "s|'https://war-vessels.herokuapp.com/play/'|window.location.href + 'play/'|g" views/pages/index.ejs


FROM node:12-stretch
COPY --from=replace /app /app
WORKDIR /app
RUN npm install
EXPOSE 5000
CMD ["node", "index.js"]

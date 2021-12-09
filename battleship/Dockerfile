FROM alpine/git:v2.32.0 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/manassarpatwar/WarVessels.git /app
WORKDIR /app
RUN git checkout 7a9e71315d21df3d91aaf6d818865dda52ca12f2
RUN rm -rf .git


FROM alpine:3.15.0 AS replace
COPY --from=clone /app /app
WORKDIR /app
RUN sed -i "s/'https:\/\/war-vessels.herokuapp.com\/play\/'/window.location.href + 'play\/'/g" views/pages/index.ejs


FROM node:16.13.0-alpine
COPY --from=replace /app /app
WORKDIR /app
RUN npm install
EXPOSE 5000
CMD ["node", "index.js"]

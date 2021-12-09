FROM alpine/git:v2.26.2 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/cepalle/red-tetris.git /app
WORKDIR /app
RUN git checkout cd0709baaf3c53f3e70d4232d223a0cac25cae56
RUN rm -rf .git


FROM node:16.13.0-alpine AS build
COPY --from=clone /app /app
WORKDIR /app
RUN npm install
RUN sed -i "s/(SOCKET_URL)/(window.location.origin)/g; /SOCKET_URL/d" src/client/redux/reducer.ts
RUN cat src/client/redux/reducer.ts
EXPOSE 4433
CMD ["npm", "run", "srv-dist"]

FROM alpine/git:v2.26.2 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/cepalle/red-tetris.git /app
WORKDIR /app
RUN git checkout cd0709baaf3c53f3e70d4232d223a0cac25cae56
RUN rm -rf .git


FROM node:14.15.1-stretch AS build
COPY --from=clone /app /app
WORKDIR /app
RUN npm install
ARG RED_TETRIS_SERVER="localhost:4433"
RUN sed -i s/localhost:4433/$RED_TETRIS_SERVER/g src/client/redux/reducer.ts
EXPOSE 4433
CMD ["npm", "run", "srv-dist"]

FROM alpine/git:v2.26.2 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/tarhses/teturisu.git /app
WORKDIR /app
RUN git checkout 2df7aeafec8e0ac1af5ef2ebef7c26bd661cf671
RUN rm -rf .git

FROM node:14.15.1-stretch
COPY --from=clone /app /app
WORKDIR /app
RUN yarn install
ARG TETURISU_SERVER="localhost:4433"
RUN sed -i "/const host = location.origin/,+2c const host = 'ws:\/\/$TETURISU_SERVER'" client/socket.ts
RUN yarn build
EXPOSE 8000
CMD ["yarn", "dev"]
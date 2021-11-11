FROM alpine/git:v2.32.0 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/opcon/OgarII.git /app
WORKDIR /app/app
RUN git checkout 33f489322a0dc02f2a283393a4266d3f89633552
RUN rm -rf .git


FROM node:16.13.0-alpine
EXPOSE 443
ENV NPM_CONFIG_LOGLEVEL info
WORKDIR /app
COPY --from=clone /app/app/package*.json /app/
COPY --from=clone /app/app /app
# Hack to replace unmaintained `uws` lib and be compatible with current node
RUN yarn add ws
RUN sed -i "s/require(\"uws\")/require(\"ws\")/g" src/sockets/Connection.js && \
    sed -i "s/require(\"uws\")/require(\"ws\")/g" src/sockets/Listener.js
RUN mkdir -p /app/settings
CMD ["node", "cli/index.js"]

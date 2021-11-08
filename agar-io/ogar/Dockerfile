FROM alpine/git:v2.32.0 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/opcon/OgarII.git /app
WORKDIR /app/app
RUN git checkout 33f489322a0dc02f2a283393a4266d3f89633552
RUN rm -rf .git


FROM node:8.17.0-slim
EXPOSE 443
ENV NPM_CONFIG_LOGLEVEL info
WORKDIR /app
COPY --from=clone /app/app/package*.json /app/
RUN yarn install
COPY --from=clone /app/app /app
RUN mkdir -p /app/settings
CMD ["node", "cli/index.js"]

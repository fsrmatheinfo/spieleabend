FROM alpine/git:v2.26.2 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/Tschuck/battletris.git /app
WORKDIR /app
RUN git checkout 35b273d5bae895084ca0aea9708fcd90a1a510a0
RUN rm -rf .git

FROM node:16.13.0-alpine AS build
COPY --from=clone /app /app
WORKDIR /app
RUN yarn install
# Fix deprecated types.
RUN sed -i "s/Record<string, string>/Record<string, string | string[]>/g" backend/src/server/RoomHandler.ts
# Unconfigure server URLs.
RUN sed -i "s/config.serverUrl/window.location.origin/g" frontend/src/lib/request.ts
RUN sed -i "s/config.wsUrl/window.location.origin.replace(\/^https\/, 'wss').replace(\/^http\/, 'ws')/g" frontend/src/lib/WsConnection.ts
RUN sed -i "s/config.frontendUrl/true/g" backend/src/server/plugins.ts
RUN yarn deploy


FROM node:16.13.0-alpine
COPY --from=build /app/.deploy /app
WORKDIR /app
RUN yarn install
EXPOSE 5000
CMD ["yarn", "start"]
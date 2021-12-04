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
# Refresh browser data.
RUN cd frontend && npx browserslist@latest --update-db
# Update frontend build target.
RUN sed -i "s/\"target\": \"esnext\"/\"target\": \"es2019\"/g" frontend/tsconfig.json
# Update server.
ARG BATTLETRIS_SERVER="localhost:4433"
RUN sed -i "s/https:\/\/battletris.de/http:\/\/$BATTLETRIS_SERVER/g; s/wss:\/\/battletris.de/ws:\/\/$BATTLETRIS_SERVER/g" frontend/.env.production
RUN sed -i "s/localhost/$BATTLETRIS_SERVER/g" backend/src/lib/config.ts
RUN yarn deploy


FROM node:16.13.0-alpine
COPY --from=build /app/.deploy /app
WORKDIR /app
RUN yarn install
EXPOSE 5000
CMD ["yarn", "start"]
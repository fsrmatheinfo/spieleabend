FROM alpine/git:v2.32.0 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/jbowens/codenames.git /app
WORKDIR /app
RUN git checkout 3e8db4bb4682fea113dd6421f7f1e83c7f0bf2c8
RUN rm -rf .git


FROM golang:1.18.2-alpine AS backend
COPY --from=clone /app /app
WORKDIR /app
RUN apk add gcc musl-dev \
    && go build ./cmd/codenames/main.go


FROM node:12-alpine AS frontend
COPY --from=clone /app /app
WORKDIR /app/frontend
RUN apk add python3 build-base
RUN npm install -g parcel-bundler \
    && npm install \
    && sh build.sh


FROM alpine:3.14
WORKDIR /app
COPY --from=backend /app/main .
COPY --from=frontend /app/frontend/dist ./frontend/dist
COPY --from=clone /app/assets assets
EXPOSE 9091/tcp
CMD /app/main

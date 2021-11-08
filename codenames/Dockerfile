FROM alpine/git:v2.26.2 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/jbowens/codenames.git /app
WORKDIR /app
RUN git checkout 3e8db4bb4682fea113dd6421f7f1e83c7f0bf2c8
RUN rm -rf .git


FROM golang:1.14-alpine AS backend
COPY --from=clone /app /app
WORKDIR /app
RUN apk add gcc musl-dev \
    && go build ./cmd/codenames/main.go


FROM node:12-alpine AS frontend
COPY --from=clone /app /app
WORKDIR /app/frontend
RUN npm install -g parcel-bundler \
    && npm install
RUN npm audit fix\
    && sh build.sh


FROM alpine:3.11
WORKDIR /app
COPY --from=backend /app/main .
COPY --from=frontend /app/frontend/dist ./frontend/dist
COPY --from=clone /app/assets assets
EXPOSE 9091/tcp
CMD /app/main
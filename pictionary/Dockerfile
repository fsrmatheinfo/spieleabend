FROM alpine/git:v2.24.3 AS clone
RUN git config --global advice.detachedHead false
RUN git clone --branch "v1.0" --depth 1 https://github.com/uni-halle-fsr-mathe-info/spieleabend-pictionary.git /app
WORKDIR /app


FROM golang:1.14.2 AS build
COPY --from=clone /app /app
WORKDIR /app
RUN make build


FROM scratch
COPY --from=build /app/scribblers /scribblers
ENTRYPOINT ["/scribblers"]
EXPOSE 8080

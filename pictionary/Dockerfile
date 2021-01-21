FROM alpine/git:v2.26.2 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/scribble-rs/scribble.rs.git /app
WORKDIR /app
RUN git checkout 5819ee114f4f24a7e072ea15b61e1befea0e216a
RUN rm -rf .git


FROM golang:1.15.5-buster AS build
COPY --from=clone /app /app
WORKDIR /app
RUN make build


FROM scratch
COPY --from=build /app/scribblers /scribblers
ENTRYPOINT ["/scribblers"]
EXPOSE 8080

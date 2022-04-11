FROM alpine/git:v2.32.0 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/seansegal/tincisnotcatan.git /app
WORKDIR /app
RUN git checkout dbee097162d1afd477089086a56b076dcdb89dca
RUN rm -rf .git


FROM alpine:3.15.4
RUN apk update && apk fetch openjdk8 && apk add openjdk8 bash maven
ENV JAVA_HOME=/usr/lib/jvm/java-1.8-openjdk
COPY --from=clone /app /app
WORKDIR /app
RUN ./build.sh
EXPOSE 4567
CMD ./run

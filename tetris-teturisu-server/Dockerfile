FROM alpine/git:v2.26.2 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/tarhses/teturisu.git /app
WORKDIR /app
RUN git checkout 2df7aeafec8e0ac1af5ef2ebef7c26bd661cf671
RUN rm -rf .git


FROM hayd/alpine-deno:1.5.2
WORKDIR /app
RUN mkdir server game

# Cache dependencies
COPY --from=clone /app/server/deps.ts /app/server
RUN deno cache server/deps.ts

# Cache source code
COPY --from=clone /app/server /app/server
COPY --from=clone /app/game /app/game
RUN deno cache server/main.ts

EXPOSE 8001
CMD ["run", "--allow-env", "--allow-net", "server/main.ts"]

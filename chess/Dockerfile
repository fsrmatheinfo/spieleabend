FROM alpine/git:v2.26.2 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/Aveek-Saha/Online-Chess.git /app
WORKDIR /app
RUN git checkout 12f39e091aeb54432937eae46c8c03f80e8fcfb2
RUN rm -rf .git


FROM node:14.15.1-alpine3.12
COPY --from=clone /app /app
WORKDIR /app
RUN npm install
EXPOSE 8080
CMD ["node", "index.js"]

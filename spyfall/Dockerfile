FROM alpine/git:v2.32.0 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/tannerkrewson/spyfall.git /app
WORKDIR /app
RUN git checkout bda1fdea2f96670096b5ce40cb1fe1ac2025dd46
RUN rm -rf .git


FROM node:17.5.0-alpine
COPY --from=clone /app /app
WORKDIR /app
RUN npm install
RUN npm run build
EXPOSE 3000
CMD ["npm", "start"]

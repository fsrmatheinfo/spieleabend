FROM alpine/git:v2.32.0 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/huytd/agar.io-clone.git /app
WORKDIR /app
RUN git checkout 8c8d26cff0d6c3c37d432a11443281139c74de3a
RUN rm -rf .git


# The game depends on Node 'primordials', which don't seem to be supported by modern node versions.
FROM node:17.1.0-alpine
COPY --from=clone /app /app
WORKDIR /app
RUN npm install
EXPOSE 3000
CMD ["npm", "start"]

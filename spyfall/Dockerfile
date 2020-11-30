FROM alpine/git:v2.26.2 AS clone
RUN git config --global advice.detachedHead false
RUN git clone https://github.com/tannerkrewson/spyfall.git /app
WORKDIR /app
RUN git checkout 75ce779d98043532fd37241a6ddb4c138813e9eb
RUN rm -rf .git


FROM node:14.15.1-stretch
COPY --from=clone /app /app
WORKDIR /app
RUN npm install
RUN npm audit fix
RUN npm run build
EXPOSE 3000
CMD ["npm", "start"]

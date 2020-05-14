FROM alpine/git:v2.24.3 AS clone
RUN git config --global advice.detachedHead false
RUN git clone --branch "v1.0.3" --depth 1 https://github.com/uni-halle-fsr-mathe-info/spieleabend-cards-against-humanity.git /app
WORKDIR /app


FROM maven:3.5.4-jdk-8 as build
COPY --from=clone /app /app
WORKDIR /app
RUN cp build.properties.example build.properties
RUN mvn clean dependency:go-offline
RUN mvn package -Dmaven.buildNumber.doCheck=false -Dmaven.buildNumber.doUpdate=false
RUN mvn war:war


FROM tomcat:7.0-jdk8
ADD sample.war $CATALINA_HOME/webapps/sample.war
COPY --from=build /app/target/ZY.war $CATALINA_HOME/webapps/ROOT.war
EXPOSE 8080
ENTRYPOINT ["catalina.sh", "run"]

# maven build
FROM maven:3.6.1-jdk-11-slim AS MAVEN_TOOL_CHAIN
COPY pom-docker.xml /tmp/pom.xml
COPY src /tmp/src/
COPY settings-docker.xml /usr/share/maven/ref/
WORKDIR /tmp/
RUN mvn -s /usr/share/maven/ref/settings-docker.xml package


# final custom slim java image (for apk command see jdk-11.0.3_7-alpine-slim)
FROM redhat-openjdk18-openshift:1.1

# add spring boot application
VOLUME /tmp
COPY --from=MAVEN_TOOL_CHAIN /tmp/target/camunda-bpm-identity-keycloak-examples-sso-kubernetes*.jar ./app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]

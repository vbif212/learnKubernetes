FROM openjdk:8-jdk-alpine
ENV OAUTH_TOKEN_URL =http://localhost:8081
ADD target/resourceserver-0.0.1-SNAPSHOT.jar /
EXPOSE 8085
CMD ["java", "-jar", "resourceserver-0.0.1-SNAPSHOT.jar", "--oauth.token.url=${OAUTH_TOKEN_URL}"]

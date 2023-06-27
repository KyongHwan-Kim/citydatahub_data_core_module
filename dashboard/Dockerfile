FROM eclipse-temurin:11
WORKDIR /
ADD target/datacore-usertool-2.0.2.jar app.jar
ENTRYPOINT [ "java", \
    "-Djava.security.egd=file:/dev/./urandom", \
    "-Djava.net.preferIPv4Stack=true", \
    "-Dspring.profiles.active=docker", \
    "-jar", \
    "app.jar"]


FROM maven:3.8.3-openjdk-17 AS build

WORKDIR /Back
ADD target/*.jar app.jar
EXPOSE 8082
ENTRYPOINT ["java", "-jar", "app.jar"]
# Use a base image with Java and Alpine Linux
FROM openjdk:11-jre-slim

# Set the working directory within the container
WORKDIR /app

# Copy the JAR file from your build context to the container
COPY target/your-spring-boot-app.jar /app/app.jar

# Expose the port your Spring Boot application will run on
EXPOSE 8081

# Command to run the Spring Boot application
CMD ["java", "-jar", "app.jar"]

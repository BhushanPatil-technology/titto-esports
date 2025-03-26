# Use OpenJDK as the base image
FROM openjdk:21-jdk-slim

# Set the working directory
WORKDIR /app

# Copy the Maven wrapper and pom.xml
COPY mvnw ./
COPY .mvn .mvn
COPY pom.xml ./

# Give execute permission to Maven wrapper
RUN chmod +x mvnw

# Download dependencies (this will cache them)
RUN ./mvnw dependency:go-offline

# Copy the source code
COPY src src/

# Build the application
RUN ./mvnw package

# Copy the built JAR file into the container
COPY target/*.jar app.jar

# Expose the port your Spring Boot app runs on
EXPOSE 8080

# Command to run the application
CMD ["java", "-jar", "app.jar"]

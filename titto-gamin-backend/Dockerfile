# Stage 1: Build the application
FROM maven:3.9.6-eclipse-temurin-21 AS build

# Set the working directory
WORKDIR /app

# Copy the source code
COPY . .

# Build the application (this will download dependencies and create the JAR)
RUN mvn clean package -DskipTests

# Stage 2: Create the final runtime image
FROM openjdk:21-jdk-slim

# Set the working directory
WORKDIR /app

# Copy the built JAR file from the build stage
COPY --from=build /app/target/*.jar app.jar

# Expose the port your Spring Boot app runs on
EXPOSE 8080

# Command to run the application
CMD ["java", "-jar", "app.jar"]

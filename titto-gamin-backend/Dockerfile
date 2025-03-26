# Stage 1: Build the application
FROM maven:3.8.4-openjdk-21 AS build

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
COPY src ./src

# Build the application (skipping tests for faster builds)
RUN ./mvnw clean package -DskipTests

# Stage 2: Create a lightweight image to run the application
FROM openjdk:21-jdk-slim

# Set the working directory
WORKDIR /app

# Copy only the built JAR from the first stage
COPY --from=build /app/target/*.jar app.jar

# Expose the port your Spring Boot app runs on
EXPOSE 8080

# Command to run the application
CMD ["java", "-jar", "app.jar"]

# Stage 1: Build the project
FROM maven:3.8.6-openjdk-21 AS build

# Set the working directory
WORKDIR /app

# Copy the pom.xml and download dependencies
COPY pom.xml ./
RUN mvn dependency:go-offline

# Copy the source code
COPY src ./src

# Build the project
RUN mvn clean package

# Stage 2: Prepare the runtime environment
FROM openjdk:21-jdk-slim

# Set the working directory
WORKDIR /app

# Copy the built JAR file(s) from the build stage
# Assuming the JAR is built into the target directory
COPY --from=build /app/target/*.jar /app/

# Optionally, set an entry point if this project is intended to run as an application
# CMD ["java", "-jar", "/app/your-library.jar"]

# If this is purely a library, you may not need CMD
# EXPOSE can be used if the library provides a service on a port

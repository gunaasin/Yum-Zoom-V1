# Use an official Maven image to build the Spring Boot app
FROM maven:3.9.6-eclipse-temurin-21 AS build
# Set the working directory
WORKDIR /app
# Copy the pom.xml and install dependencies
COPY pom.xml .
RUN mvn dependency:go-offline
# Copy the source code and build the application
COPY src ./src

# Compile and package the application
RUN mvn clean package -DskipTests

FROM eclipse-temurin:21-jdk
# Set the working directory
WORKDIR /app
# Copy the built JAR file from the build stage
COPY --from=build /app/target/yumzoom-0.0.1-SNAPSHOT.jar app.jar
# Expose port 8080
EXPOSE 8080
# Specify the command to run the application
CMD ["java", "-jar", "app.jar"]

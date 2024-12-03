# Base image with OpenJDK 17
FROM openjdk:17-jdk-slim AS build

# Install Maven
RUN apt-get update && apt-get install -y maven && apt-get clean

# Set the working directory
WORKDIR /app

# Copy the pom.xml and the source code
COPY pom.xml .
COPY src ./src

# Package the application
RUN mvn clean package -DskipTests

# Package stage
FROM openjdk:17-jdk-slim

# Set the working directory for the final image
WORKDIR /app

# Copy the JAR file from the build stage
COPY --from=build /app/target/DeploymentwithRender-0.0.1-SNAPSHOT.jar ./Demo.jar

# Use the Render-provided $PORT environment variable
ENV PORT=8080

# Run the application and bind to $PORT
CMD ["sh", "-c", "java -jar Demo.jar --server.port=${PORT}"]

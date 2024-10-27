# Use an official JDK runtime as a parent image
FROM adoptopenjdk:11-jre-hotspot

# Set the working directory in the container
WORKDIR /app

# Copy the jar file from the target directory into the container
COPY target/*.jar app.jar

# Expose the port the app runs on
EXPOSE 8090

# Run the application
CMD ["java", "-jar", "app.jar", "--server.port=8090"]

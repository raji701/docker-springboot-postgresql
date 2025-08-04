FROM openjdk:17-slim

# Install netcat (needed by wait-for-it.sh)
RUN apt-get update && apt-get install -y netcat && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Copy the jar file
ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} app.jar

# Copy the wait-for-it.sh script
COPY wait-for-it.sh .

# Make the script executable
RUN chmod +x wait-for-it.sh

# Wait for DB and start app
ENTRYPOINT ["./wait-for-it.sh", "postgres-db", "5432", "--", "java", "-jar", "app.jar"]

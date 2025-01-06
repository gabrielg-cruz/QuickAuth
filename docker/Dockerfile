#Maven image to build project in Docker
FROM maven:3.9.0-openjdk-17 AS build

#Working directory in container
WORKDIR /app

#Copy pom.xml to container to install dependencies
COPY pom.xml .

#Install dependencies
RUN mvn dependency:go-offline

#Copy source code to container
COPY src ../src

#Build project
RUN mvn clean package -DskipTests

#JRE image to run project in Docker
FROM openjdk:17-jre-slim

#Copy jar file from build image to run image
COPY --from=build /app/target/*.jar /app/app.jar

#Expose port 8080
EXPOSE 8080

#Run project
ENTRYPOINT ["java", "-jar", "/app/app.jar"]
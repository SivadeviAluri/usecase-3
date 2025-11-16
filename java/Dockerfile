FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app
RUN git clone https://github.com/spring-projects/spring-petclinic.git .
RUN mvn clean package -DskipTests
FROM eclipse-temurin:17-jdk
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]

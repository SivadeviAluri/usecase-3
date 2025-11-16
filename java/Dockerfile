FROM maven:3.9.8-eclipse-temurin-25 AS build
WORKDIR /app
RUN git clone https://github.com/spring-projects/spring-petclinic.git .
RUN mvn clean package -DskipTests
FROM eclipse-temurin:25-jdk
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
CMD ["java", "-jar", "app.jar"]


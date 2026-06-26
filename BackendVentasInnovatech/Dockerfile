# Etapa de compilación
FROM maven:3.9.9-eclipse-temurin-17 AS build
WORKDIR /app

COPY Springboot-API-REST/pom.xml ./
COPY Springboot-API-REST/mvnw ./
COPY Springboot-API-REST/.mvn ./.mvn
RUN chmod +x mvnw
RUN ./mvnw dependency:go-offline

COPY Springboot-API-REST/src ./src
RUN ./mvnw clean package -DskipTests

# Etapa de ejecución
FROM eclipse-temurin:17-jre-jammy
WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app/app.jar"]

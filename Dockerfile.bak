FROM gradle:8.10.2-jdk17 AS build
WORKDIR /app
COPY --chown=gradle:gradle . .
RUN gradle clean bootJar -x test || gradle clean build -x test

FROM eclipse-temurin:17-jre-jammy
WORKDIR /app
ARG JAR_FILE=build/libs/*.jar
COPY --from=build /app/${JAR_FILE} /app/app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","/app/app.jar"]

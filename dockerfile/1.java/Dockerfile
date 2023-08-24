FROM maven:3.6.3-jdk-11-slim AS build
WORKDIR /project
COPY . /project
RUN mvn clean package -DskipTests

FROM adoptopenjdk/openjdk11:jre-11.0.9.1_1-alpine
WORKDIR /app
RUN addgroup --system javauser && adduser -S -s /bin/false -G javauser javauser
COPY --from=build /project/target/*.jar /app/java-application.jar
RUN chown -R javauser:javauser /app
USER javauser
CMD "java" "-jar" "java-application.jar"

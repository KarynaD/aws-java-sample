FROM maven:3-amazoncorretto-21 AS builder
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn package -DskipTests


FROM amazoncorretto:21-alpine

RUN addgroup --system javauser && adduser -S -s /bin/false -G javauser javauser
ARG JAR_FILE=task-1.0.0-SNAPSHOT.jar
COPY --from=builder /app/target/${JAR_FILE} app.jar
RUN chown -R javauser:javauser app.jar
USER javauser

EXPOSE 8081
ENTRYPOINT ["java", "-jar", "app.jar", "--server.port=8081"]
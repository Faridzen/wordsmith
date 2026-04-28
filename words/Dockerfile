FROM maven:3-eclipse-temurin-17-alpine AS builder
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src/ ./src/
RUN mvn verify

RUN mvn verify dependency:copy-dependencies

FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=builder /app/target/words.jar .
COPY --from=builder /app/target/dependency/ ./lib/
CMD ["java", "-Xmx8m", "-Xms8m", "-cp", "words.jar:./lib/*", "Main"]
EXPOSE 8080
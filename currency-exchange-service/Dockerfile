# ---------- Stage 1 : Build ----------
FROM maven:3.9.9-eclipse-temurin-21 AS builder

WORKDIR /app

COPY pom.xml .
COPY src ./src

RUN mvn clean package -DskipTests

# ---------- Stage 2 : Runtime ----------
FROM eclipse-temurin:21-jre

RUN addgroup --system spring && adduser --system spring --ingroup spring

WORKDIR /app

COPY --from=builder /app/target/*.jar app.jar

USER spring

EXPOSE 8000

ENTRYPOINT ["java","-jar","app.jar"]
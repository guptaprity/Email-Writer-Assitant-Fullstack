# ===============================
# 1. BUILD STAGE
# ===============================
FROM eclipse-temurin:17-jdk AS builder

WORKDIR /app

COPY mvnw .
COPY .mvn .mvn
COPY pom.xml .
COPY src src

RUN chmod +x mvnw
RUN ./mvnw clean package -DskipTests


# ===============================
# 2. RUNTIME STAGE
# ===============================
FROM eclipse-temurin:17-jre

WORKDIR /app

# IMPORTANT: Use correct jar name pattern
COPY --from=builder /app/target/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]

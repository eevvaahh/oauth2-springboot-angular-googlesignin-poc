# 1. ETAPA DE CONSTRUCCIÓN (BUILD STAGE)
FROM maven:3.9.5-eclipse-temurin-17 AS builder

WORKDIR /app

# Copiar el archivo de configuración de Maven para aprovechar el cache
COPY pom.xml .
RUN mvn dependency:go-offline

# Copiar el código fuente y construir el JAR
COPY src/ ./src/
RUN mvn clean install -DskipTests

# 2. ETAPA DE EJECUCIÓN (RUNTIME STAGE)
FROM eclipse-temurin:17-jre-focal

# Instalamos curl para que funcione el HEALTHCHECK de docker-compose
RUN apt-get update && apt-get install -y curl && apt-get clean

WORKDIR /app

# Copiar el JAR construido
COPY --from=builder /app/target/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]

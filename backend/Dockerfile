FROM maven:3.9.9-eclipse-temurin-17 AS build

WORKDIR /workspace

COPY pom.xml ./

RUN mvn --batch-mode dependency:go-offline

COPY src ./src

RUN mvn --batch-mode clean package -DskipTests

FROM eclipse-temurin:17-jre-jammy

RUN apt-get update \
    && apt-get install -y --no-install-recommends curl \
    && rm -rf /var/lib/apt/lists/* \
    && groupadd --system appgroup \
    && useradd --system --gid appgroup --home-dir /app appuser

LABEL org.opencontainers.image.title="parking-api"
LABEL org.opencontainers.image.description="Neology Parking Backend"
LABEL org.opencontainers.image.version="1.0.0"

WORKDIR /app

COPY --from=build --chown=appuser:appgroup \
    /workspace/target/parking-api-1.0.0.jar \
    /app/app.jar

USER appuser

EXPOSE 8080

HEALTHCHECK --interval=30s --timeout=5s --start-period=30s --retries=3 \
  CMD curl --fail --silent http://localhost:8080/actuator/health || exit 1

STOPSIGNAL SIGTERM

ENTRYPOINT ["java", "-XX:MaxRAMPercentage=75.0", "-jar", "/app/app.jar"]


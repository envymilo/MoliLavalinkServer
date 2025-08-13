# Stage 1 - Build Lavalink
FROM eclipse-temurin:21-jdk-jammy AS builder

WORKDIR /app
COPY . .

RUN chmod +x gradlew

RUN ./gradlew :LavalinkServer:build --no-daemon

# Stage 2 - Run Lavalink
FROM eclipse-temurin:21-jdk-jammy

RUN groupadd -g 322 lavalink && \
    useradd -r -u 322 -g lavalink lavalink

WORKDIR /opt/Lavalink
COPY --from=builder /app/LavalinkServer/build/libs/Lavalink.jar Lavalink.jar

USER lavalink

ENTRYPOINT ["java", "-jar", "Lavalink.jar"]

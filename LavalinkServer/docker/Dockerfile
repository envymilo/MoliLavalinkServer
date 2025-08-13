# Stage 1 - Build
FROM eclipse-temurin:21-jre AS builder

WORKDIR /app
COPY . .
WORKDIR /app/LavalinkServer

RUN ./gradlew --no-daemon build

# Stage 2 - Run
FROM eclipse-temurin:18-jre-jammy

# Run as non-root user
RUN groupadd -g 322 lavalink && \
    useradd -r -u 322 -g lavalink lavalink

WORKDIR /opt/Lavalink
RUN chown -R lavalink:lavalink /opt/Lavalink
USER lavalink

COPY --from=builder /app/LavalinkServer/build/libs/Lavalink.jar Lavalink.jar

ENTRYPOINT ["java", "-jar", "Lavalink.jar"]

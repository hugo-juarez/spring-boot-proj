FROM gradle
LABEL authors="hugo-juarez"

WORKDIR /app


# Copy gradle wrapper and config first (layer caching)
COPY gradlew .
COPY gradle/ gradle/
COPY build.gradle.kts .
COPY settings.gradle.kts .

# Download dependencies first (cached as a separate layer)
RUN ./gradlew dependencies --no-daemon

# Copy source and build
COPY src/ src/
RUN ./gradlew bootJar --no-daemon

RUN mv ./build/libs/*jar ./app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
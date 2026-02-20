# Java 21 + Maven Setup in Docker

## Devcontainer Beispiel (für Entwicklung)

`.devcontainer/devcontainer.json`:

```json
{
  "name": "Java 21 + Maven",
  "image": "mcr.microsoft.com/devcontainers/java:1-21-bookworm",

  "features": {
    "ghcr.io/devcontainers/features/git:1": {},
    "ghcr.io/devcontainers/features/github-cli:1": {}
  },

  "customizations": {
    "vscode": {
      "extensions": [
        "vscjava.vscode-java-pack",
        "vscjava.vscode-maven",
        "GitLens.gitlens"
      ],
      "settings": {
        "java.configuration.updateBuildConfiguration": "automatic",
        "maven.executable.path": "/usr/local/maven/bin/mvn"
      }
    }
  },

  "postCreateCommand": "mvn -q -DskipTests compile",
  "remoteUser": "vscode"
}
```

**Starten**:
- VSCode Command Palette
- "Dev Containers: Reopen in Container"
- Fertig!

## Dockerfile Beispiel (für Produktion)

Einfache Version:

```dockerfile
FROM eclipse-temurin:21-jdk-jammy

# Maven installieren
RUN apt-get update && apt-get install -y maven git

WORKDIR /app

COPY . .

RUN mvn clean package -DskipTests

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "target/app.jar"]
```

Multi-stage Build (empfohlen):

```dockerfile
# Stage 1: Build
FROM maven:3.9-eclipse-temurin-21 as builder

WORKDIR /build

# Nur pom.xml zuerst (Layer Caching)
COPY pom.xml .
RUN mvn dependency:resolve

# Dann Source Code
COPY src ./src

# Build
RUN mvn clean package -DskipTests

# Stage 2: Runtime (kleiner)
FROM eclipse-temurin:21-jre-jammy

WORKDIR /app

# JAR von Builder kopieren
COPY --from=builder /build/target/*.jar app.jar

EXPOSE 8080

# Heap Size limitieren
ENV JAVA_OPTS="-Xmx512m -Xms256m"

ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS -jar app.jar"]
```

**Vorteil**: Runtime Image ist ~300MB statt ~800MB

## Docker Compose (Entwicklung)

```yaml
version: '3.8'

services:
  app:
    build: .
    container_name: java-app
    ports:
      - "8080:8080"
    environment:
      - JAVA_OPTS=-Xmx512m
      - MAVEN_OPTS=-Xmx512m
    volumes:
      # Source Code live mounten
      - ./src:/app/src
      # Target für Rebuild
      - ./target:/app/target
      # Maven Cache (beschleunigt Builds)
      - ~/.m2:/root/.m2
    working_dir: /app
    # Für Live-Reload oder Watch-Mode
    command: mvn clean compile exec:java
```

Starten:
```bash
docker-compose up --build
```

## Docker Compose + Database

```yaml
version: '3.8'

services:
  app:
    build: .
    ports:
      - "8080:8080"
    environment:
      DB_HOST: postgres
      DB_NAME: myapp
      DB_USER: appuser
      DB_PASSWORD: apppass
      JAVA_OPTS: -Xmx512m
    depends_on:
      - postgres
    volumes:
      - ./src:/app/src

  postgres:
    image: postgres:15-alpine
    container_name: java-postgres
    environment:
      POSTGRES_DB: myapp
      POSTGRES_USER: appuser
      POSTGRES_PASSWORD: apppass
    volumes:
      - postgres_data:/var/lib/postgresql/data
      # Initialisierung SQL
      - ./init-db.sql:/docker-entrypoint-initdb.d/init.sql
    ports:
      - "5432:5432"

volumes:
  postgres_data:
```

`init-db.sql`:
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255),
    email VARCHAR(255)
);
```

## pom.xml (Maven Basics)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project>
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>java-app</artifactId>
    <version>1.0.0</version>

    <properties>
        <maven.compiler.source>21</maven.compiler.source>
        <maven.compiler.target>21</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <!-- PostgreSQL Driver -->
        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <version>42.7.0</version>
        </dependency>

        <!-- JUnit für Tests -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <!-- JAR Plugin -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-jar-plugin</artifactId>
                <version>3.3.0</version>
                <configuration>
                    <archive>
                        <manifest>
                            <mainClass>com.example.Main</mainClass>
                        </manifest>
                    </archive>
                </configuration>
            </plugin>

            <!-- Shade Plugin (für Fat JAR mit Dependencies) -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>3.5.0</version>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

## Tipps

1. **Alpine Java Image für kleinere Größe**
   ```dockerfile
   FROM eclipse-temurin:21-jre-alpine
   ```

2. **Non-root User für Sicherheit**
   ```dockerfile
   RUN useradd -m appuser
   USER appuser
   ```

3. **Health Check**
   ```dockerfile
   HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
     CMD curl -f http://localhost:8080/health || exit 1
   ```

4. **Maven Cache für schnellere Builds**
   ```bash
   docker build --build-arg MAVEN_CACHE=true -t myapp .
   ```

## Workflow

```bash
# Devcontainer verwenden (Entwicklung)
# VSCode → Dev Containers: Reopen in Container

# Oder lokal mit Docker Compose
docker-compose up --build

# App läuft auf http://localhost:8080

# Testen
curl http://localhost:8080

# Produktions-Image bauen
docker build -t myapp:1.0 .

# Produktions-Container starten
docker run -p 8080:8080 myapp:1.0
```

Siehe auch: [Docker Grundlagen](Grundlagen.md), [Devcontainer](Devcontainer.md)

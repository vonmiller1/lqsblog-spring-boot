# LQSBlog Spring Boot

Modular Spring Boot backend for a personal blog with an administrative REST API, public read API, and a Thymeleaf web front end.

## Overview

LQSBlog splits persistence, business logic, and HTTP layers across seven Maven modules. The `lqsblog-api` application exposes JWT/Shiro-protected admin endpoints and public JSON APIs for articles, tags, search, and site configuration. The `lqsblog-webs` application renders server-side HTML from the same service layer. MyBatis-Plus maps entities to a MySQL schema with an `lqs_` table prefix.

## Features

- Administrative authentication with Apache Shiro and JWT
- Public APIs for articles, categories, tags, topics, works, links, search, and configuration
- Admin CRUD for content, accounts, roles, menus, uploads, and site settings
- MyBatis-Plus persistence on MySQL
- Thymeleaf templates with shared web components
- Configurable CORS, upload directory, and static asset mapping

## Tech stack

| Layer | Technology |
| --- | --- |
| Language | Java 11 |
| Framework | Spring Boot 2.2.6 |
| Build | Maven (multi-module reactor) |
| Persistence | MyBatis-Plus 3.3, MySQL |
| Security | Apache Shiro 1.4, JJWT |
| Web UI | Thymeleaf (`lqsblog-webs`) |
| JSON | Fastjson |

## Prerequisites

- JDK 11
- Maven 3.6+
- MySQL 5.7+ with the `lqsblog` schema and seed data expected by the mappers

## Getting started

```sh
git clone https://github.com/vonmiller1/lqsblog-spring-boot.git
cd lqsblog-spring-boot
```

Configure database credentials and JWT settings (see [Configuration](#configuration)) in each runnable module before building.

## Configuration

Runnable modules keep their own `application.yml`:

| Application | Config file |
| --- | --- |
| API | `lqsblog-api/src/main/resources/application.yml` |
| Web | `lqsblog-webs/src/main/resources/application.yml` |

Local development activates the `local` Spring profile, which enables verbose SQL logging via `application-local.yml` in each module.

Environment variables (defaults match local samples in YAML):

| Variable | Purpose |
| --- | --- |
| `LQSBLOG_DB_URL` | JDBC URL |
| `LQSBLOG_DB_USERNAME` | Database user |
| `LQSBLOG_DB_PASSWORD` | Database password |
| `LQSBLOG_JWT_KEY` | JWT signing key (API module) |
| `LQSBLOG_UPLOAD_DIR` | Filesystem upload root (API module) |
| `LQSBLOG_WEBURL` | Public site URL used in upload responses (API) |

Do not deploy with sample credentials or weak signing keys. Override these values in production.

Default HTTP ports: API **8088**, web **8089** (`server.port` in each module).

## Build

From the repository root:

```sh
mvn clean package
```

## Running locally

After a successful build, start either executable JAR from the repository root:

```sh
java -jar lqsblog-api/target/lqsblog-api-1.0-SNAPSHOT.jar
```

```sh
java -jar lqsblog-webs/target/lqsblog-webs-1.0-SNAPSHOT.jar
```

The API and web apps can run independently; configure MySQL for each before starting.

## Testing

From the repository root (requires configured MySQL for integration-style tests):

```sh
mvn test
```

Module-level tests live under each module’s `src/test/java` tree (for example `lqsblog-api/src/test/java`).

## Project structure

```
.
├── pom.xml                 # Parent reactor
├── lqsblog-common/         # Shared utilities (upload, JWT helpers)
├── lqsblog-database/       # Entities, mappers, DTOs
├── lqsblog-service/        # Business services (admin + public)
├── lqsblog-api-common/     # Shared API config and handlers
├── lqsblog-api/            # REST API Spring Boot app (port 8088)
├── lqsblog-webs-common/    # Shared web error handling
└── lqsblog-webs/           # Thymeleaf Spring Boot app (port 8089)
```

## Deployment

- Build fat JARs with `mvn clean package` and run with a JRE 11+ runtime.
- Point `LQSBLOG_DB_*` and `LQSBLOG_JWT_KEY` at production values; disable the `local` profile or omit `application-local.yml` logging in production.
- Ensure the upload directory exists and is writable when using admin upload endpoints.
- Configure `lqsblog.access.origins` for allowed admin front-end origins.

No Dockerfile or CI workflow is included in this repository.

## Contributing

1. Fork the repository and create a feature branch from `main`.
2. Keep commits focused; use imperative messages (for example `fix(upload): reject path traversal`).
3. Open a pull request describing behavior impact and configuration changes.

## License

[MIT License](LICENSE) — Copyright (c) 2020 LiQingSong.

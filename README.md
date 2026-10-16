# LQSBlog Spring Boot

A modular Java/Spring Boot backend for a personal blog. The project provides administrative and public-facing APIs, shared business and data-access modules, and a Thymeleaf-based web application.

## Features

- JWT/Shiro-based administrative authentication
- Public blog endpoints for articles, categories, tags, topics, works, links, search, and site configuration
- Administrative endpoints for content, accounts, roles, menus, uploads, and site settings
- MyBatis-Plus persistence backed by MySQL
- Thymeleaf web application with shared web components

## Technology

- Java 11
- Spring Boot 2.2.6
- Maven multi-module build
- MyBatis-Plus and MySQL
- Apache Shiro and JWT
- Thymeleaf

## Modules

| Module | Responsibility |
| --- | --- |
| `lqsblog-api` | Administrative and public REST API application |
| `lqsblog-api-common` | Shared API configuration and components |
| `lqsblog-webs` | Thymeleaf web application |
| `lqsblog-webs-common` | Shared web components |
| `lqsblog-service` | Blog business services |
| `lqsblog-database` | Persistence models and MyBatis mappers |
| `lqsblog-common` | Shared utilities and common code |

## Prerequisites

- JDK 11
- Maven 3.6 or later
- MySQL 5.7 or later, with the database schema and data required by the application

## Configure

Before starting either application, review its configuration:

- API: `lqsblog-api/src/main/resources/application.yml`
- Web: `lqsblog-webs/src/main/resources/application.yml`

Set the MySQL connection details for your environment. For the API, also set an appropriately protected JWT signing key, the upload directory, the site URL, and the allowed CORS origins. Do not deploy with development credentials or signing keys, and do not commit production secrets.

The API is configured for port `8088` and the web application for port `8089` by default. Adjust the corresponding `server.port` setting if those ports are unavailable.

## Build

From the repository root:

```sh
mvn clean package
```

## Run

Build the project first, then launch either executable application from the repository root:

```sh
java -jar lqsblog-api/target/lqsblog-api-1.0-SNAPSHOT.jar
```

```sh
java -jar lqsblog-webs/target/lqsblog-webs-1.0-SNAPSHOT.jar
```

The API and web application can be run independently; start the one you need after configuring its database connection.

## Development notes

- Application configuration is maintained separately in each runnable module.
- Uploaded files are written to the configured local upload directory; ensure it exists and is writable by the application.
- The root Maven project aggregates all seven modules.

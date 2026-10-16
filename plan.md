# Engineering Improvement Plan

## Objective

Improve the reliability, security, and maintainability of the existing modular Spring Boot blog without changing its public behavior unnecessarily. Work should be delivered in small, reviewable stages, with behavior and deployment compatibility checked before each release.

## Priorities

### P0 — Make runtime configuration safe

- [ ] Move database credentials, JWT signing material, upload paths, and environment-specific URLs out of checked-in defaults into documented external configuration.
- [ ] Ensure deployed environments cannot start with development credentials or a weak/default signing key.
- [ ] Disable verbose SQL logging outside local development and document the supported profile/configuration mechanism.
- [ ] Verify that upload directories are created or clearly reported as unavailable, and that only permitted upload types are accepted.

**Complete when:** a fresh deployment can be configured without editing tracked source files, required secrets have no unsafe fallback, and local and production logging behavior is explicit.

### P1 — Make setup and persistence reproducible

- [ ] Document the MySQL schema and seed-data provisioning procedure, including versioning and upgrade expectations.
- [ ] Add a repeatable local development setup that identifies all required services and configuration values.
- [ ] Define consistent API error, validation, and pagination behavior for administrative and public endpoints.

**Complete when:** a new contributor can prepare a compatible database and start the selected application by following repository documentation alone.

### P1 — Strengthen automated coverage

- [ ] Add focused service-layer tests for core blog and administrative workflows.
- [ ] Add persistence tests for representative MyBatis mappings and database-dependent behavior.
- [ ] Add API tests for authentication/authorization, validation, and public read endpoints.
- [ ] Document the test commands and the database or other services required by each test group.

**Complete when:** the main business paths and access-control boundaries have repeatable automated checks that can run in CI.

### P2 — Improve dependency and build maintenance

- [ ] Review the Spring Boot, Java, MyBatis-Plus, Shiro, JWT, and JSON-library versions for support status and known compatibility concerns.
- [ ] Plan framework and dependency upgrades in isolated increments, preserving Java and runtime compatibility intentionally.
- [ ] Standardize Maven plugin and dependency version management across modules.

**Complete when:** the supported runtime matrix is documented, dependency changes are reviewed for compatibility, and the full reactor builds consistently in the supported environment.

### P2 — Clarify module boundaries

- [ ] Document the intended dependency direction among common, database, service, API, and web modules.
- [ ] Keep transport-specific concerns in their respective API/web modules and shared business logic in the service layer.
- [ ] Remove placeholder module documentation and describe extension points that are actively supported.

**Complete when:** module responsibilities and allowed dependencies are clear enough to guide new features without duplicating business logic.

## Delivery approach

1. Address configuration and deployment risks before changing framework versions.
2. Establish repeatable database setup and focused tests before refactoring behavior.
3. Upgrade dependencies and reshape module boundaries only in small changes with explicit compatibility review.
4. Update the root README and this plan as the actual supported setup and priorities evolve.

## Scope and guardrails

- Preserve existing API behavior unless a change is explicitly documented and reviewed.
- Avoid mixing security, framework-upgrade, and feature work in one change.
- Keep deployment-specific values and generated or uploaded files out of source control.
- Treat each completion criterion as requiring evidence from the implementation and the appropriate automated checks.

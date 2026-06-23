# AGENTS.md — AI coding agent instructions

Purpose: provide concise, discoverable guidance so AI coding agents can be immediately productive in this repository. Link to existing docs; avoid duplicating long explanations.

Quick links
- README: [README.md](README.md)
- Contribution guide: [CONTRIBUTING.md](CONTRIBUTING.md)
- Parent Maven POM: [pom.xml](pom.xml)
- Docker compose: [docker-compose.yml](docker-compose.yml)
- Useful scripts: [scripts/run_all.sh](scripts/run_all.sh), [scripts/chaos/README.md](scripts/chaos/README.md)

Quick-start (developer)
- Build all modules: `./mvnw clean install`
- Run tests: `./mvnw test`
- Build Docker images: `./mvnw clean install -P buildDocker`
- Run full stack (Docker): `docker compose up --build`
- Hybrid dev run (script): `./scripts/run_all.sh`

Essential facts for agents
- This is a multi-module Maven project (parent POM at repository root). Use `./mvnw` from repo root for consistent Java/Maven versions.
- Key modules: spring-petclinic-admin-server, spring-petclinic-api-gateway, spring-petclinic-config-server, spring-petclinic-discovery-server, spring-petclinic-customers-service, spring-petclinic-vets-service, spring-petclinic-visits-service, spring-petclinic-genai-service.
- Service discovery: Eureka (Discovery Server). Start Config → Discovery → services for local Java runs.
- Profiles: use `-P buildDocker` to build container images. Some builds require Java 17+.
- Docker compose is provided at the repo root; `docker compose up` will stand up Prometheus/Grafana and the microservices (check healthchecks in `docker-compose.yml`).

What to link vs what to include
- Link to in-repo docs (README.md, CONTRIBUTING.md, docs/) rather than copying content.
- Include short, actionable commands and environment tips here (as above).

Conventions and pitfalls
- Expect ports and service registration via Eureka; do not hardcode ports across agents — consult Eureka or `docker-compose.yml`.
- Builds enforce Java 17+ (maven-enforcer-plugin). CI assumes the same.
- Docker builds may require extra CPU/memory on contributor machines; mention this if tests or builds fail due to OOM.

Where to look first
- Top-level README for overall architecture and run instructions: [README.md](README.md)
- Parent `pom.xml` for module list and Maven profiles: [pom.xml](pom.xml)
- `docker-compose.yml` for full-stack dependencies and ports: [docker-compose.yml](docker-compose.yml)
- `scripts/run_all.sh` for hybrid dev runs and common helper steps: [scripts/run_all.sh](scripts/run_all.sh)

Suggested next customizations (optional)
- Create a small skill that knows how to run targeted module builds and map service names → ports.
- Add a testing hook to run only changed-module unit tests (useful for large PRs).

If you want changes to this guidance (more details, stricter conventions, or separate instructions per module), tell me which area to expand.

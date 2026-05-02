# Python Standards & Practices

---

## 📖 1. Purpose

This handbook defines the engineering standards, architecture guidelines, and development practices for all python projects.

It ensures:
- Consistency across teams
- High performance and scalability
- Maintainable and production-ready code

---

## 🎯 2. Guiding Principles

- Clarity over cleverness
- Explicit over implicit (Zen of Python)
- Performance is a feature
- Async-first mindset
- Strong typing everywhere
- Separation of concerns
- Config-driven systems
- Provides standards and guidelines, you don't have to incorporate everything you see in this document however if you see any exception or deviation ask me.

---

## 🐍 3. Technology Standards

### Python Version
- Python 3.12 (mandatory)

### Core Libraries & Tools
- Data modeling: dataclasses, pydantic, Enums
- Typing: typing, Protocol, ABC, Annotated
- CLI: typer
- Configuration: hydra
- Async DB: motor, sync DB: pymongo
- Data processing: polars & numpy
- Use functools, itertools & collections where-ever deemed necessary
- API development: FASTAPI
- Scheduler: APScheduler
- HTTP client: httpx (async and sync)
- Notification: Email (simple and HTML based)

---

## 🏗️ 4. Project Architecture

```
├──project_name
	├── bin/                   # entry point executors (mainly bash scripts calling python entry points, essentially initializing/ priming the entry points - making sure the required py version, dirs, etc are in place. Also these scripts needs to have self tracker making sure multiple instances are not running causing corruption. This feature can be turned on and off by the user)
	├── docs/                  # will have various wiki markdown files explaining and going in depth about src files, this is why README.md should be a high level overview and point to here for more detailed descriptions
	├── logs/                  # Logging
	├── output/                # Any module that requires to capture output (can contain telemetry data too)
	├── reports/               # Any module that requires to generate reports (can contain telemetry data too)
	├── src/
		├── api/               # API code goes here and sub-dir depending on the project
		├── common/            # Shared/ common utilities, DB client, DB connection and other settings, Async and sync http client, logging, encryption, decryting code, email sender
			├── constants.py   # All common or shared constants go here
		├── config/            # Configuration management
		├── controllers
		├── models/            # Pydantic / dataclasses
		├── repositories/      # Data access layer
		├── telemetry/         # OTEL code goes here
		├── services/          # Business logic
		├── constants.py       # All project level/ application constants go here
		└── main.py            # Entry point, can have multiple entry points depends on the project
	├── tests/                 # It should follow same structure as src (Project is not complete if at least 95% score is not achieved) and I have common folder which should contain code which I can lift and shift to other projects and the corresponding tests and not worry to start over.
	├── README.md              # High level readme
	├── requirements.txt
	├── pyproject.toml         # my future choise is uv
	├── .gitignore
```
---

## ⚙️ 5. Configuration Management

### Rules
- Centralize all configuration
- No hardcoded values or secrets
- Hydra (maybe??)

### Priority Order

CLI > ENV > Pydantic Settings > Mongo-based Settings - Always take CLI config/ settings over the ENV based over pydantic-settings and if none found fallback to mongo based settings (Not sure how to approach this)

### Requirements
- Use Pydantic Settings
- Store env variables in /config
- Use clear naming conventions (e.g., PROJECT_NAME__DB_HOST, PROJECT_NAME__API_TIMEOUT)

---

## 🧱 6. Data Modeling

### When to Use What

| Use Case | Tool |
|----------|------|
| Lightweight structures | dataclasses |
| Validation & serialization | pydantic |

### Requirements
- Use type hints
- Provide field descriptions
- Avoid untyped/dynamic fields

---

## 🧠 7. Design & Code Practices

- Use design patterns where appropriate:
  - Repository
  - Factory
  - Strategy
  - Builder
  - Domain, Port & Adapters
  - Cohesion
  - Specification
  - Dependency Injection

- Follow SOLID principles
- Use value objects instead of primitivies
- Follow the Zen of Python:
  ```python   import this   ```

---

## 📝 8. Code Quality Standards

### Mandatory
- Type hints for all functions
- Docstrings for public APIs
- Clear naming conventions
- If a design pattern or conventions is being implemented define that in the comments above that section

### Example

python def get_user(user_id: str) -> User:     """Fetch a user by ID."""

---

## ⚡ 9. Performance Guidelines

### Core Rules
- Prefer async/await
- Consider Big-O complexity
- Use batch processing
- Use multiprocessing and multi threading where-ever deemed necessary

### Optimization Techniques
- Minimize database calls
- Replace:
  - List scans → dict/set lookups

---

## 📊 10. Data Processing

- Use Polars instead of Pandas
- Prefer columnar operations
- Avoid row-by-row loops

---

## 🗄️ 11. Database Layer

### Driver Selection
- Use Motor (async)
- Use PyMongo only when async is not feasible

### Repository Pattern

Service → Repository → Database

### Requirements
- Implement Base Repository
- Support both Motor and PyMongo

---

## 🖥️ 12. CLI Standards

- Use Typer
- Provide:
  - --help support
  - Typed arguments
  - Scriptable commands

---

## 🔄 13. Async Standards

- Avoid blocking I/O
- Use async-compatible libraries
- Avoid excessive parallelism

---

## 🔐 14. Environment & Secrets

- Never commit secrets
- Use environment variables
- Use secret managers in production
- Create a utility for encrypting and decryting data which will be used inside this project

---

## 🧪 15. Testing

- Use pytest
- Unit test business logic
- Mock external dependencies

---

## 🚀 16. Deployment Principles

- Config-driven deployments
- No environment-specific code
- Include logging and monitoring

---

## 📌 17. Anti-Patterns to Avoid

- Business logic in controllers
- Direct DB access in APIs
- Hardcoded configs
- Blocking I/O in async code
- Using Pandas for large datasets

---

## ✅ 18. Definition of Done

A feature is complete when:
- Fully typed
- Documented
- Tested
- Performance considered
- Follows all standards

---

## 🧭 19. Final Note

> Consistency beats cleverness.
> Simplicity scales.
> Performance matter.

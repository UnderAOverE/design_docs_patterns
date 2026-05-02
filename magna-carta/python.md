# 🏢 Engineering Handbook  
## Python Backend Standards & Practices

---

## 📖 1. Purpose

This handbook defines the engineering standards, architecture guidelines, and development practices for all backend services.

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

---

## 🐍 3. Technology Standards

### Python Version
- Python 3.12 (mandatory)

### Core Libraries & Tools
- Data modeling: dataclasses, pydantic, Enums
- Typing: typing, Protocol, Annotated
- CLI: typer
- Async DB: motor
- Data processing: polars
- Use functools, itertools, collections whereever deemed necessary

---

## 🏗️ 4. Project Architecture

src/   
	├── api/              # API routes 
	├── bin   
	├── controllers   
	├── services/         # Business logic   
	├── repositories/     # Data access layer   
	├── models/           # Pydantic / dataclasses   
	├── config/           # Configuration management   
	├── utils/            # Shared utilities   
	└── main.py           # Entry point
tests/ # it should follow same structure as src
README.md
requirements.txt
pyproject.toml # my future choise is uv
.gitignore
---

## ⚙️ 5. Configuration Management

### Rules
- Centralize all configuration
- No hardcoded values or secrets
- Hydra (maybe??)

### Priority Order

CLI > ENV > Pydantic Settings > Mongo-based Settings 

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
  - Port & Adapter
  - Specification
  - Dependency Injection

- Follow SOLID principles
- Follow the Zen of Python:
  ```python   import this   ```

---

## 📝 8. Code Quality Standards

### Mandatory
- Type hints for all functions
- Docstrings for public APIs
- Clear naming conventions

### Example

python def get_user(user_id: str) -> User:     """Fetch a user by ID.""" 

---

## ⚡ 9. Performance Guidelines

### Core Rules
- Prefer async/await
- Consider Big-O complexity
- Use batch processing

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

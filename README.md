# Grupo ing-sist

Welcome to the organization! This organization hosts a complete ecosystem composed of two main pillars: **Printscript**, a custom programming language, and **Snippet Searcher**, a scalable microservices application built around it.

---

## Ecosystem Architecture

Our architecture is heavily decoupled, separating the core language logic from the web platform services. The ecosystem is distributed across the following core repositories:

*   **`printscript`**: The core language implementation (Lexer, Parser, AST, Interpreter, Formatter, Linter, and CLI).
*   **`snippet-service` (Manager)**: The central orchestrator handling incoming requests and coordinating the asynchronous event flow.
*   **`engine-service`**: The execution environment that validates and runs Printscript code snippets.
*   **`auth-service`**: The access control microservice managing user permissions via Auth0.
*   **`printscript-ui`**: The frontend web application built with React and TypeScript.
*   **`infra`**: Centralized infrastructure definitions, including Nginx configurations, Let's Encrypt certificates, and Docker Compose environments.
*   **`asset-service`**: Service of the Snippet Searcher platform in charge of storing assets to a bucket.

---

## Printscript

Printscript is a custom programming language developed entirely from scratch. The language pipeline is strictly modular, utilizing design patterns such as **Factory** to keep components extensible and decoupled. It is structured around the following phases:

- **Lexer** – Tokenizes the source code into a stream of tokens.
- **Parser** – Builds an Abstract Syntax Tree (AST) from the token stream.
- **Interpreter** – Executes the AST to produce the final program output.
- **Formatter** – Applies configurable style rules to standardise source code.
- **Linter** – Enforces coding conventions and detects potential semantic issues.
- **CLI** – A command-line interface to run, format, and lint Printscript programs locally.

**Supported Versions:**
- **Version 1.0** – The initial language release.
- **Version 1.1** – Extended specification with advanced language features.

---

## Snippet Searcher

Snippet Searcher is a cloud-ready web application that allows users to store, share, and execute code snippets written in Printscript. The backend is designed as a distributed system composed of three primary microservices:

### 1. Service (Manager)
The main entry point for the backend. It receives requests from the frontend, orchestrates communication between the internal services, and manages the asynchronous event-driven workflow with the Engine to prevent blocking operations.

### 2. Engine
A dedicated worker service responsible for processing code snippets. Given a snippet, it:
- **Validates** syntax and semantics using the Printscript core libraries (Lexer, Parser, Linter).
- **Executes** the snippet safely using the Printscript interpreter and returns the output.

### 3. Authorization
Manages access control and resource ownership. It verifies identities using **Auth0** and determines if a user has permissions to:
- **Edit** a snippet (Owner).
- **View** a snippet (Shared access).
- **Have no access** to a snippet.

---

## Infrastructure & Tech Stack

We utilize a modern stack focused on scalability, containerization, and observability.

| Concern | Technology |
|:---|:---|
| **Backend Language** | Kotlin |
| **Frontend** | TypeScript, React, Vite |
| **Containerization** | Docker, Docker Compose |
| **CI/CD** | GitHub Actions |
| **Observability & APM** | New Relic |
| **End-to-End Testing** | Cypress |
| **Async Event Bus** | Redis |
| **Snippet Storage** | Azurite (Azure Blob Storage emulator) |
| **Reverse Proxy / TLS** | Nginx + Let's Encrypt (HTTPS) |
| **Authentication** | Auth0 |

---

## DevOps & CI/CD

All repositories in this organization employ automated **GitHub Actions** workflows to maintain code quality and streamline deployments. 
- **Continuous Integration**: On every pull request, the code is built, tested, and validated.
- **Continuous Deployment**: Packages and Docker images are automatically published, ensuring the latest stable versions are always ready for deployment.

# 🏗️ Architecture

This document explains the **system architecture and internal design** of the AI Code Review Agent.

It is written to help developers, reviewers, and contributors understand **how data flows through the system** and how each component interacts.

---

## 🎯 Architectural Goals

The architecture is designed with the following goals:

- ✅ Modularity & separation of concerns
- ✅ Scalability for new languages and tools
- ✅ Easy maintainability
- ✅ Offline-first & privacy-safe execution
- ✅ Industry-inspired backend design

---

## 🧱 High-Level Architecture

```text
Client (UI / API Consumer)
        ↓
Flask API Layer (Routes)
        ↓
Core Analysis Services
  ├─ Static Analysis Engine
  ├─ LLM Analysis Engine (Ollama)
        ↓
Result Aggregation & Formatter
        ↓
Structured JSON Response
```

Each layer is independent and communicates through **well-defined interfaces**.

---

## 📦 Layered Architecture Breakdown

### 1️⃣ Client Layer

**Examples:**
- Web UI
- Postman / curl
- CI/CD pipeline
- CLI tools

**Responsibilities:**
- Submitting source code
- Displaying review results

---

### 2️⃣ API Layer (Flask)

**Location:**
```
backend/routes/
```

**Responsibilities:**
- Handle HTTP requests
- Validate input payload
- Invoke analysis services
- Return formatted responses

This layer acts as the **entry point** to the system.

---

### 3️⃣ Core Services Layer

This is the **heart of the application**.

#### 🔹 Static Analysis Service

**Purpose:**
- Perform fast, rule-based analysis

**Tools Used:**
- pylint
- bandit
- radon

**Output:**
- Objective findings (errors, warnings, metrics)

---

#### 🔹 LLM Analysis Service (Ollama)

**Purpose:**
- Perform semantic and contextual code review

**Model:**
- `deepseek-coder:6.7b`

**Responsibilities:**
- Generate intelligent feedback
- Suggest refactored code
- Explain reasoning in human-readable form

---

### 4️⃣ Utilities Layer

**Location:**
```
backend/utils/
```

**Key Components:**

- `language_detect.py` → Detects programming language
- `chunker.py` → Splits large files into safe chunks
- `formatter.py` → Normalizes and structures output

This layer ensures the system is **robust and LLM-safe**.

---

### 5️⃣ Prompt Management

**Location:**
```
backend/prompts/
```

**Why it exists:**
- Keeps prompts version-controlled
- Easy experimentation and tuning
- Improves LLM output consistency

Prompts are written to enforce:
- Structured responses
- Professional tone
- Best-practice recommendations

---

## 🔄 Data Flow (Step-by-Step)

```text
1. Code is submitted by the client
2. Language is auto-detected
3. Static analysis tools are executed
4. Code is chunked if necessary
5. Prompt is generated with context + static results
6. Ollama LLM processes the request
7. Results are aggregated
8. Structured JSON response is returned
```

---

## 🧠 Design Decisions

### Why Hybrid Analysis?

| Static Analysis | LLM Analysis |
|----------------|--------------|
| Deterministic | Context-aware |
| Fast | Intelligent reasoning |
| Rule-based | Best-practice driven |

Combining both provides **accuracy + depth**, similar to real-world developer tools.

---

### Why Ollama (Local LLM)?

- No API cost
- Full data privacy
- Offline execution
- Low latency

Ideal for internal tools and enterprise environments.

---

## 🔐 Security Architecture

- No external network calls for code analysis
- All execution happens locally
- Static analysis tools are sandboxed
- No code is persisted unless configured

---

## 📈 Scalability & Extensibility

The architecture supports:

- Adding new programming languages
- Plugging in additional static analyzers
- Switching LLM models
- CI/CD pipeline integration
- GitHub Pull Request bots

Minimal changes are required due to modular design.

---

## 🛣️ Future Architecture Enhancements

- Message queue for async analysis
- Distributed worker nodes
- Vector database for code memory
- Real-time dashboard

---

## ⭐ Summary

This architecture follows **real-world backend and AI system design principles**, making the project suitable for:

- Hackathons
- Internships
- Production-grade prototypes

Next:
- See **api-reference.md** for endpoint documentation.

---

Happy building! 🚀


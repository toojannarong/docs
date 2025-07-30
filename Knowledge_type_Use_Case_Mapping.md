# Defensive Programming and the Four Types of Knowledge

This document maps the well-known "Known/Unknown" knowledge framework to defensive programming practices in software development.

## Knowledge Types and Their Meaning

| Knowledge Type        | Meaning                                                                 |
|------------------------|-------------------------------------------------------------------------|
| **Known knowns**       | Things we **know that we know**.                                        |
| **Known unknowns**     | Things we **know that we don’t know**.                                  |
| **Unknown knowns**     | Things we **don’t know we know** (e.g., undocumented tribal knowledge). |
| **Unknown unknowns**   | Things we **don’t know we don’t know**—the true surprises.              |

---

## Mapping to Defensive Programming Strategies

| Knowledge Type        | Description | Defensive Programming Strategies |
|------------------------|-------------|----------------------------------|
| **Known knowns**       | You understand the logic and risks. | - Unit tests<br>- Input validation<br>- Preconditions/postconditions |
| **Known unknowns**     | Gaps you're aware of (e.g., risky integrations). | - Timeouts, retries<br>- Fallback mechanisms<br>- Circuit breakers |
| **Unknown knowns**     | Hidden assumptions, tribal knowledge. | - Assertions for invariants<br>- Logging<br>- Code reviews<br>- Documentation |
| **Unknown unknowns**   | Unexpected failures or edge cases. | - Fail-fast design<br>- Global exception handlers<br>- Observability (logs, metrics, alerts)<br>- Safe defaults |

---

# Defensive Programming: Anticipating the Unknowns

This document connects the four types of knowledge (known knowns, known unknowns, unknown knowns, unknown unknowns) to defensive programming practices across different software components.

---

## ✅ Included Topics:
1. Anticipating Known Unknowns vs Unknown Unknowns  
2. Kafka Consumer Application  
3. Kafka Producer Application  
4. Spring Web MVC REST API  
5. Angular Frontend (Live Search + Filter Inputs)  
6. Null Pointer Exception (NPE)

---

## 🧠 Knowledge Types Explained

| Type                | Meaning                                                                 |
|---------------------|-------------------------------------------------------------------------|
| **Known knowns**    | Things we **know we know** (requirements, tested logic).                |
| **Known unknowns**  | Things we **know we don’t know** (external API behavior, uncertain load).|
| **Unknown knowns**  | Things we **don’t realize we know** (tribal knowledge, assumptions).     |
| **Unknown unknowns**| Things we **don’t know we don’t know** (rare bugs, edge cases).          |

---

## 🔐 Mapping to Defensive Programming

| Knowledge Type      | Defensive Focus Areas                                                                 |
|---------------------|----------------------------------------------------------------------------------------|
| **Known knowns**    | ✅ Validate inputs, write unit tests, enforce contracts (preconditions, assertions).   |
| **Known unknowns**  | 🛡️ Add fallbacks, circuit breakers, timeouts, retries, defensive defaults.             |
| **Unknown knowns**  | 🔍 Document code, write comments, log assumptions, peer reviews, integration tests.    |
| **Unknown unknowns**| 🚨 Fail-fast, global error handling, observability (logging, tracing, metrics).         |

---

## 🧩 Use Case Mapping

### 1. Kafka Consumer Application
| Knowledge Type        | Defensive Actions |
|------------------------|------------------|
| Known unknowns         | Handle schema evolution, unknown event order.<br>Use dead-letter queues (DLQ). |
| Unknown unknowns       | Add global error handler, structured logging with message metadata. |

---

### 2. Kafka Producer Application
| Knowledge Type        | Defensive Actions |
|------------------------|------------------|
| Known knowns           | Ensure message schema validity and correct topic config. |
| Known unknowns         | Handle broker unavailability, serialization failures. |
| Unknown unknowns       | Use retry and backoff, alert on message loss or delivery failure. |

---

### 3. Spring Web MVC REST API
| Knowledge Type        | Defensive Actions |
|------------------------|------------------|
| Known knowns           | Validate DTOs with `@Valid`, catch expected exceptions. |
| Known unknowns         | Timeout on external services, fallback responses. |
| Unknown unknowns       | Add `@ControllerAdvice` for global error handling, trace correlation ID. |

---

### 4. Angular Frontend (Live Search + Filter Inputs)
| Knowledge Type        | Defensive Actions |
|------------------------|------------------|
| Known knowns           | Debounce user input (e.g., 300ms), handle missing filters gracefully. |
| Known unknowns         | Unexpected backend responses, race conditions. |
| Unknown unknowns       | Fail silently with UI fallback, log unexpected JSON parsing or HTTP errors. |

---

### 5. Null Pointer Exception (NPE)
| Knowledge Type        | Defensive Actions |
|------------------------|------------------|
| Known knowns           | Null checks, `Optional`, `Objects.requireNonNull`. |
| Unknown knowns         | Identify hidden assumptions—e.g., fields initialized via config. |
| Unknown unknowns       | Fail-fast with logs to reveal unanticipated null paths. |

---

## 🧭 Visual Model (Text Diagram)

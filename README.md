# 🛡️ ACME Multimodal Content Moderation System

This project is an **AI-powered multimodal content moderation system** designed for customer service interactions at a fictional company called **ACME Enterprise**.

The goal of the application is to simulate how AI can help monitor and enforce communication standards in customer support environments, especially when agents interact with customers through different types of content.

## ✨ What the system does

Before any content is sent to the customer, the system analyzes it and checks whether it complies with the company's communication policies.

It can moderate:

* 💬 **Text**
* 🖼️ **Images**
* 🎥 **Videos**
* 🎧 **Audio**

The moderation agents can detect issues such as:

* Personally Identifiable Information (**PII**)
* Unprofessional or inappropriate language
* Unfriendly or disrespectful communication
* Disturbing or unsafe visual content
* Low-quality images, videos, or audio
* Other content that may violate customer service standards

When problematic content is detected, the system can **block it** and return a structured explanation describing why the content was flagged.

---

## 🎭 Customer Service Simulation

The application includes a simulated customer interaction designed for training purposes.

A trainee customer service agent interacts with an **LLM-powered customer** who is intentionally frustrated because a product they purchased the **ACME Power Widget Pro** has stopped working.

The trainee must handle the conversation professionally while attempting to resolve the customer's problem.

During the interaction, every message or uploaded file from the trainee is automatically analyzed by the moderation system before being delivered to the simulated customer.

This makes it possible to evaluate whether the trainee is following the expected communication standards throughout the conversation.

---

## 🏗️ Architecture

The project is divided into several components.

### 1. 🤖 Specialized Moderation Agents

The system contains four specialized moderation agents:

* Text moderation agent
* Image moderation agent
* Video moderation agent
* Audio moderation agent

Each agent uses **Google Gemini** with prompts tailored to the specific type of content being analyzed.

The agents are located in:

```text
agents/
```

This separation makes the system modular and allows each type of media to have its own moderation logic.

---

### 2. 🧑‍💻 LLM as a Customer

The customer in the simulation is also powered by an LLM.

Its behavior is implemented in:

```text
agents/customer_agent.py
```

The agent simulates an unhappy customer who purchased the **ACME Power Widget Pro** and is contacting customer support because the product is no longer working.

This creates a realistic environment where trainees can practice handling difficult conversations.

---

### 3. 📦 Structured Moderation Results

Instead of returning only a simple `true` or `false`, moderation agents return **structured results using Pydantic models**.

These results contain specific moderation flags such as:

```text
contains_pii
is_unfriendly
```

along with a human-readable **rationale** explaining why the content was flagged.

The moderation result definitions can be found in:

```text
types/moderation_result.py
```

Structured outputs make the moderation decisions easier to validate, test, log, and integrate with other services.

---

### 4. 💬 Frontend — Gradio Chat Interface

The project includes an interactive frontend built with **Gradio**.

The interface allows users to:

* Chat with the simulated customer
* Send text messages
* Upload images
* Upload videos
* Upload audio files
* Receive moderation feedback in real time

The frontend is implemented in:

```text
gradio_app.py
```

Gradio is especially useful for quickly building and testing AI proof-of-concept applications.

---

### 5. ⚡ Backend — FastAPI REST API

The backend is implemented using **FastAPI**.

It exposes HTTP endpoints that provide programmatic access to the moderation agents, such as:

```text
/moderate/text
/moderate/image
/moderate/video
/moderate/audio
```

The backend is implemented in:

```text
fastapi_app.py
```

These endpoints essentially wrap the moderation agents behind a REST API.

Separating the frontend from the backend is a common pattern in modern web applications and provides an important architectural advantage: **multiple frontends can reuse the same backend services**.

For example, this project currently uses Gradio as the frontend because it is convenient for building a proof of concept.

In a production environment, the Gradio interface could later be replaced by a more sophisticated application built with technologies such as:

```text
React
Vue
Angular
```

The new frontend could continue using the same FastAPI backend without requiring changes to the AI agents.

Both interfaces could even coexist during a migration period while the new frontend is validated.

This separation keeps the AI logic independent from the user interface.

---

### 6. 🔍 Observability with Arize Phoenix

The project includes **Arize Phoenix** for tracing and observability.

Observability is particularly important in AI applications because it helps developers understand:

* Which agents were executed
* What prompts were sent
* How the model responded
* Where moderation decisions were made
* How long different operations took
* Why unexpected behavior occurred

Some of the tracing configuration is located in:

```text
tracing.py
```

This makes it easier to inspect and debug the behavior of the AI agents during development.

---

### 7. 🚀 Service Launcher

The project also provides a convenience executable that starts the main services required by the application.

It launches:

1. **FastAPI backend**
2. **Gradio frontend**
3. **Arize Phoenix observability service**

This allows the complete application stack to be started more easily during development.

---

## 🔄 High-Level Flow

A typical interaction follows this flow:

```text
Trainee Agent
      │
      ▼
Gradio Frontend
      │
      ▼
Moderation Agent
(Text / Image / Video / Audio)
      │
      ▼
Structured Moderation Result
      │
      ├── Content Approved ──► Simulated Customer
      │
      └── Content Blocked ──► Explanation / Feedback
```

Meanwhile, **Phoenix tracing** records the behavior of the AI components for debugging and observability.

---

# 🛠️ How to Work on the Project

The initial project scaffolding is already provided.

For the step-by-step instructions to create and configure the project environment, see [Environment Setup](project/setup_environment.md).

Your task is to complete specific parts of the implementation while applying the concepts covered throughout the project.

The exercises are organized as a **sequence of steps**, and each step builds on the previous one.

For this reason, you should complete them **in the specified order**.

After each step, you can verify your implementation by running the provided automated tests.

> ⚠️ **Important:** Do not skip steps and do not continue to the next task while the current tests are failing.

The later exercises depend on functionality implemented in the earlier ones.

A good workflow is:

```text
Implement the required functionality
            ↓
Run the provided tests
            ↓
Fix any failing tests
            ↓
Confirm all tests pass
            ↓
Proceed to the next step
```

Following this process will make it much easier to identify bugs and understand how each part of the system fits into the complete application.

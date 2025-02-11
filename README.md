# Single-Agent-System

---

## Why?

### Problem Statement
Urban AI research often faces challenges in creating autonomous agents that can maintain coherent, context-aware conversations over time. The Single-Agent-System focuses on advancing research in autonomous AI agents within programming contexts, with a specific emphasis on developing advanced memory systems. The goal is to enable highly effective conversations between users and the agent by improving memory retention and recall capabilities.

### Objectives and Goals
- **Enhanced Memory Retention:** Develop a sophisticated memory module that allows the agent to recall previous interactions, ensuring contextually relevant conversations.
- **Seamless User Experience:** Provide a visually appealing and intuitive chat interface that allows users to interact naturally with the LLM agent.
- **Robust Agentic Logic:** Advance research in agent logic and memory systems, specifically focusing on autonomous conversation flow and context management.
- **Secure Data Handling:** Implement strong security practices for handling sensitive information, such as API keys, from the frontend to the backend.
- **Research and Experimentation:** Serve as a research repository to explore and validate concepts from cutting-edge papers like "Generative Agents: Interactive Simulacra of Human Behavior."

---

## What?

### What is it and What it is not
**It is:**
- A single-agent system designed to facilitate autonomous, context-aware conversations using an LLM with advanced memory retention capabilities.
- A research and experimental platform focusing on agentic logic and memory modules.
- A chat interface where users can communicate with an LLM agent that retains context from previous interactions.

**It is not:**
- A multi-agent system; this project intentionally focuses on a single, sophisticated agent.
- A generic chatbot without memory; the system’s strength lies in its memory and recall mechanisms.
- A complete commercial solution; it is primarily aimed at research and development.

### Personas
- **Ulysses User:**  
  - A user who accesses a chat window via a localhost server to communicate with the LLM Agent.
  - The user does not see past chat history directly; the agent maintains its own memory of previous interactions.

### User Stories
1. **Interface Interaction:**  
   *As Ulysses User, I want to open the application and see a visually appealing interface with a chat window so that I can engage in conversation with the LLM Agent.*

2. **Conversational Flow:**  
   *As Ulysses User, I want to type messages in the chat window and have a smooth conversation with the LLM Agent.*

3. **Memory Recall:**  
   *As Ulysses User, I want to reference previous conversations with the LLM Agent and have it recall the context correctly during our interactions.*

---

## How?

### System Design and Rationale

#### Architecture Overview
- **Frontend:**  
  - Built using **React**, **TypeScript**, and **TailwindCSS** for a lightweight, responsive, and modern chat interface.
  
- **Backend:**  
  - Developed using **FastAPI** with **uvicorn** to handle API requests.
  - Managed by **honcho** for combined server startup and process management.
  
- **Memory Module (MM):**  
  - Implements advanced memory operations inspired by "Generative Agents: Interactive Simulacra of Human Behavior."
  - Handles memory creation, scoring, vector embedding, reflection generation, and organization.
  
- **Containerization & Deployment:**  
  - **Docker** is used to ensure cross-platform compatibility and consistent deployment environments.
  
- **Data Storage & Security:**  
  - **SQLite** is used for secure storage (e.g., API keys), with practices ensuring automatic deletion upon database removal.
  - Strong encryption and secure data handling are implemented throughout the system.

#### Component Breakdown
- **Page Components and Widgets:**
  - **Chat Window:** The primary interface for conversation, comprising:
    - **User Response Widget**
    - **Agent Response Widget**
    - **Text Input Box**
    - **Send Button**
  - **Response Widget:** A base component used by both the user and agent response widgets for consistent styling and data handling.

- **Models:**
  - **Agent:**
    - `llm-name`
    - `api-service`
    - `memory-stream`
  - **User:**
    - `user-name`
    - `background` (optional for future expansion)
  - **Memory (Base Class):**
    - `timestamp`
    - `importance-score`
    - `vector-embedding`
    - `memory-contents`
  - **Reflection (Extends Memory):**
    - Contains a tree object of child Reflections and Memories.
  - **Response (Base Class):**
    - `timestamp`
    - `response-content`
    - `sender` (User or Agent)

- **API Routes:**
  - `POST /response`:  
    Handles the transmission of user responses to the backend, forwards them to the agent’s API service, awaits the agent's reply, and then returns the result to the frontend.

- **Security Considerations:**
  - Emphasis on the secure handling of user API keys from the frontend UI to the backend database.
  - Implementation of proper encryption and secure storage practices throughout the system.

#### Memory Module (MM) Details
- **Memory Processing Flow:**
  1. User input triggers memory creation.
  2. A secondary LLM evaluates the input to assign an importance score.
  3. A memory object is created with the computed importance score.
  4. A vector embedding is generated for semantic operations.
  5. A timestamp is assigned for recency tracking.
  6. The memory is stored and organized for future retrieval.
  
- **Memory Operations:**
  - Semantic search using cosine similarity to find relevant memories.
  - Inclusion of relevant memories into the LLM context during conversation.
  - Creation of new memories from both user inputs and LLM responses.
  - Periodic generation of reflections based on time or memory thresholds.
  
- **Reflection Process:**
  - Initiated based on specific time periods or when memory accumulation exceeds a threshold.
  - Involves a multi-step process to generate and store reflections with timestamps, importance scores, and vector embeddings.
  - Integrates reflections with existing memory structures.
  
- **Agent Initialization:**
  - The agent is pre-seeded with initial, user-independent memories.
  - It continuously expands its memory collection through interactions.
  - It periodically generates reflections based on accumulated memories.
  
For further details on the memory system design, refer to the [original paper](https://arxiv.org/abs/2304.03442).

### Wireframes/Mockups
Below is an example wireframe for the chat interface:

![Wireframe/Mockup](https://github.com/user-attachments/assets/949f54a1-13b9-49aa-9e6a-ee9df9335b2e)

### Technology Stack

#### Frontend
- **Framework:** React + TypeScript
- **Styling:** TailwindCSS
- **Package Management:** npm

#### Backend
- **API Framework:** FastAPI
- **Server:** uvicorn
- **Process Manager:** honcho

#### Containerization and Deployment
- **Containerization:** Docker

#### Database
- **Database:** SQLite

#### External Dependencies
- **OpenAI API:** For LLM interactions and processing

#### Testing
- **Testing Strategy:**
  - Unit Testing
  - Integration Testing
  - Performance Testing
  - Application Testing
- **Coverage:** Maintains approximately 100% test coverage (±5% tolerance)

---

## Conclusion

The **Single-Agent-System** is designed to push the boundaries of autonomous AI agent research by integrating a sophisticated memory system into an interactive LLM-based chat interface. By focusing on advanced memory retention and recall capabilities, the system aims to provide context-aware and seamless conversations, positioning itself as a valuable research platform for agentic logic development. This document outlines the problem statement, key objectives, component design, and the technical stack necessary to bring the project to fruition.

# Single-Agent-System

---

## Why?

### Problem Statement
Autonomous AI agents often struggle with retaining context over extended conversations, which limits their ability to engage in meaningful, context-aware interactions. The Single-Agent-System addresses this challenge by developing an advanced memory system that enables the agent to recall past interactions seamlessly, ensuring that conversations remain coherent and relevant over time.

### Objectives and Goals
- **Advanced Memory Retention:** Develop a sophisticated memory module capable of capturing, scoring, and recalling past interactions.
- **Enhanced Conversational Experience:** Provide a visually appealing and intuitive chat interface that allows users to engage in rich, context-aware dialogues with the LLM Agent.
- **Robust Agent Logic:** Improve the agent’s ability to integrate historical context into current responses, ensuring a more natural and effective conversation flow.
- **Security and Data Integrity:** Implement secure handling and storage of sensitive information, such as user API keys.
- **Research Innovation:** Serve as a platform for experimenting with cutting-edge memory systems and agentic logic inspired by recent academic work.

---

## What?

### What It Is and What It Is Not

**It is:**
- An experimental research platform focused on advancing autonomous AI agents by incorporating a state-of-the-art memory system.
- A chat application where users interact with a single LLM agent that maintains its own internal memory of past conversations.
- A system that implements advanced memory operations, including semantic search, memory scoring, vector embedding generation, and reflection processing.

**It is not:**
- A multi-agent system; the focus is solely on a single agent.
- A simple, stateless chatbot; the primary feature is its memory retention and recall capability.
- A production-ready commercial solution; it is intended as a research and experimentation platform.

### Key Personas
- **Ulysses User:**  
  A user who accesses the chat application via a localhost server to communicate with the LLM Agent. The user does not see previous chat history directly—the agent retains and recalls past interactions independently.

### User Stories
1. **Interface Interaction:**  
   *As Ulysses User, I want to open the application and see a visually appealing chat window so that I can start a conversation with the LLM Agent.*

2. **Conversational Engagement:**  
   *As Ulysses User, I want to type messages into the chat window and have a smooth, engaging conversation with the LLM Agent.*

3. **Context Recall:**  
   *As Ulysses User, I want the LLM Agent to recall previous conversations accurately, ensuring that context is maintained throughout our interactions.*

### Wireframes/Mockups
Below is an example wireframe of the chat interface:

![Chat Interface Wireframe](https://github.com/user-attachments/assets/949f54a1-13b9-49aa-9e6a-ee9df9335b2e)

---

## How?

### System Design and Rationale

#### Architecture Overview
- **Frontend:**  
  - Built using **React**, **TypeScript**, and **TailwindCSS** to provide a modern, responsive, and intuitive chat interface.
  
- **Backend:**  
  - Developed with **FastAPI** and run via **uvicorn** to handle API requests.
  - **honcho** is used for process management to start both the backend and frontend servers concurrently.
  
- **Memory Module (MM):**  
  - Implements advanced memory operations inspired by the paper [Generative Agents: Interactive Simulacra of Human Behavior](https://arxiv.org/abs/2304.03442).
  - Processes user inputs to create memory objects, assigns importance scores, generates vector embeddings, and organizes memories.
  
- **Containerization:**  
  - **Docker** is used to ensure consistent deployment across different platforms.

- **Data Storage & Security:**  
  - **SQLite** is utilized for secure storage of sensitive data such as API keys, with proper encryption and secure storage practices in place.

#### Page Components and Widgets
- **Chat Window:** The main interface for user-agent interaction, comprising:
  - **User Response Widget**
  - **Agent Response Widget**
  - **Text Input Box**
  - **Send Button**
  
- **Response Widget:** A base component for both the User and Agent response elements, responsible for styling and text transmission.
- **Text Input Box:** Captures user input and relays it to the backend.
- **Send Button:** Initiates the transmission of the input text from the Chat Window to the backend.

#### Models
- **Agent**
  - `llm-name`
  - `api-service`
  - `memory-stream`
  
- **User**
  - `user-name`
  - `background` (optional, for future expansion)
  
- **Memory (Base Class)**
  - `timestamp`
  - `importance-score`
  - `vector-embedding`
  - `memory-contents`
  
- **Reflection (Extends Memory)**
  - Contains a tree object of child Reflections and Memories, abstracting the relationships between them.
  
- **Response (Base Class)**
  - `timestamp`
  - `response-content`
  - `sender` (User or Agent)

#### API Routes
- **`POST /response`:**  
  Handles the submission of user responses to the backend, forwards them to the Agent's API service, receives the Agent's response, and returns it to the frontend.

#### Security Considerations
- Secure transmission and storage of user API keys from the frontend to the backend database.
- Implementation of robust encryption and secure storage practices across the system.

### Memory Module (MM)

#### Memory Processing Flow
1. **Input Trigger:** User input initiates the creation of a new memory.
2. **Importance Evaluation:** A secondary LLM evaluates the input to assign an importance score.
3. **Memory Object Creation:** A memory object is created with the assigned importance score.
4. **Vector Embedding:** Generates a vector embedding for semantic operations.
5. **Timestamping:** Assigns a timestamp to track recency.
6. **Storage and Organization:** The memory is stored and organized for future retrieval.

#### Memory Operations
- **Semantic Search:** Uses cosine similarity to compare new inputs with existing memories.
- **Context Inclusion:** Integrates relevant memories into the LLM context during response generation.
- **Memory Creation:** Records new memories from both user inputs and Agent responses.
- **Periodic Reflection:** Triggers reflection generation based on time intervals or memory accumulation thresholds.

#### Reflection Process
- **Triggering:** Initiated by specific time intervals or when memory accumulation exceeds a threshold.
- **Generation:** A multi-step process generates reflections, which include timestamps, importance scores, and vector embeddings.
- **Integration:** Reflections are merged into the existing memory structure to enhance context retention.

#### Agent Initialization
- **Pre-Seeding:** The agent starts with initial, user-independent memories.
- **Memory Growth:** The agent continuously expands its memory through ongoing interactions.
- **Reflection Generation:** The agent periodically generates reflections based on the accumulation of memories.

For more detailed information about the memory system design, refer to the [original paper](https://arxiv.org/abs/2304.03442).

### Testing Strategy
- **Unit Testing**
- **Integration Testing**
- **Performance Testing**
- **Application Testing**
- **Coverage:** Approximately 100% test coverage (±5% tolerance)

---

## Conclusion

The **Single-Agent-System** is a research-focused platform designed to advance the capabilities of autonomous AI agents by incorporating an advanced memory system. By enabling the agent to retain and recall past interactions, the system facilitates more natural, context-aware conversations. This document outlines the problem statement, key objectives, component design, and technical stack necessary to build and experiment with this innovative platform.

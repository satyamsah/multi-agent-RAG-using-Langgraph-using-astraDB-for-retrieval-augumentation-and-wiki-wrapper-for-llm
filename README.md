
# ** Muti-agent AI chatbot with LangChain and LangGraph**

## **Overview**
Exploring multi-agent systems with LangGraph, LangChain, and a vector database. The goal is to create a retrieval-augmented generation (RAG) pipeline that leverages Llama as the large language model (LLM) agent to intelligently answer user queries. The system dynamically routes queries to either a local corpus (powered by AstraDB as the vector database) or a Wikipedia agent for external knowledge retrieval, all orchestrated through a simple LangGraph setup.

For this iteration, I used a straightforward AstraDB instance as the vector datastore. In the next phase, I plan to replace AstraDB with OpenSearch, while keeping the overall concept intact.

Excited to see where this journey leads—feel free to share your thoughts or comments! 🚀


<img width="995" alt="Screenshot 2025-01-13 at 7 15 22 PM" src="https://github.com/user-attachments/assets/1056e76e-aa9f-473d-9d41-61e3919b9f11" />


---

## **Key Components**

### **1. LangChain**
- **Role:** Facilitates interaction with large language models (LLMs) and tool integrations.
- **Applications:**
  - Decision-making for query routing.
  - Retrieval from external tools like Astra DB and Wikipedia.
  - Producing structured outputs for downstream processes.

### **2. LangGraph**
- **Role:** Models and executes workflows as a directed state graph.
- **Applications:**
  - Node and edge definitions for workflow orchestration.
  - Visualizes workflows and compiles them for execution.
  - Enables dynamic routing based on query type.

### **3. Astra DB**
- **Role:** Acts as the vector database for domain-specific document retrieval.
- **Applications:**
  - Stores pre-processed, vectorized documents for fast retrieval.
  - Serves as the knowledge base for specialized queries.

### **4. Wikipedia Search**
- **Role:** Provides real-time access to external general knowledge.
- **Applications:**
  - Answers general or non-domain-specific queries.

---

## **Use Cases**

### **1. Customer Support Systems**
Automatically route customer questions to the correct knowledge base, providing faster and more accurate responses.

### **2. Intelligent Search**
Offer users a hybrid search experience by combining structured domain knowledge with real-time external sources.

### **3. AI Assistants**
Enable AI systems to adaptively handle queries, ensuring domain expertise while maintaining flexibility for general questions.

### **4. Educational Tools**
Provide students and professionals with relevant knowledge by integrating diverse knowledge sources dynamically.

---

## **Workflow Structure**

### **1. Input and Routing (`route_question`)**
- **Input:** A natural language query from the user.
- **Logic:** 
  - Queries are analyzed by LangChain's LLM.
  - Decision function (`route_question`) determines whether to:
    - Fetch general knowledge from Wikipedia.
    - Retrieve domain-specific documents from Astra DB.

---

### **2. Graph Workflow**
- **Framework:** Designed and executed with LangGraph.
- **Nodes:**
  - `route_question`: Routes queries to appropriate nodes.
  - `wiki_search`: Handles real-time external lookups from Wikipedia.
  - `astra_db_retrieve`: Retrieves documents from Astra DB for specialized queries.
- **Edges:**
  - Conditional routing using `route_question` determines the path based on the query context.
  - Terminal edges mark the completion of the workflow.

---

## **Graph Execution**

1. **Start**:
   - User submits a question.
2. **Decision Point (`route_question`)**:
   - Evaluates the query and routes it to the appropriate node:
     - `wiki_search` for general knowledge.
     - `astra_db_retrieve` for domain-specific questions.
3. **Processing Nodes**:
   - **`wiki_search`**: Executes a Wikipedia search for external information.
   - **`astra_db_retrieve`**: Retrieves vectorized documents from Astra DB.
4. **Completion**:
   - Outputs the retrieved or generated response.

---

## **Core Functionalities**

### **1. Query Routing with LangChain**
- LangChain's LLM analyzes queries and outputs routing decisions.
- Decisions are implemented through LangGraph’s conditional edges.

### **2. Knowledge Retrieval**
- **Astra DB**:
  - Vectorized storage and retrieval for domain-specific content.
  - Ensures fast and accurate results for specialized queries.
- **Wikipedia**:
  - Real-time search integration for broad, general-purpose questions.

### **3. Modular Workflow with LangGraph**
- **Node Definitions**:
  - Encapsulate specific functions like `route_question`, `wiki_search`, and `astra_db_retrieve`.
- **Dynamic Transitions**:
  - Conditional edges enable dynamic routing based on query type.
- **Visualization**:
  - The graph structure can be visualized for better debugging and understanding.

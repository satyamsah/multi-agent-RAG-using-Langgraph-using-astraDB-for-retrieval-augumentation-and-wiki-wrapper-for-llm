# **AI Workflow with LangChain and LangGraph**

## **Overview**
This project integrates **LangChain** and **LangGraph** to construct an intelligent, modular question-answering workflow. It leverages the strengths of **retrieval-augmented generation (RAG)**, vector databases, and Wikipedia search to provide dynamic, context-aware responses. By combining **LLM-driven routing** and **workflow graphing**, the system efficiently routes user queries to the appropriate knowledge sources.

---

## **Key Components**

### **1. LangChain**
- **Role:** The backbone of LLM interaction and tool integration.
- **Applications:**
  - Routing queries via a **ChatLLM** model.
  - Retrieving data using tools like vectorstores (Astra DB) and Wikipedia search.
  - Enabling structured outputs through LLM pipelines.

### **2. LangGraph**
- **Role:** Models the overall workflow as a state graph.
- **Applications:**
  - Defines nodes (functional units) and edges (transitions) in the workflow.
  - Automates routing based on LangChain's LLM outputs.
  - Visualizes and compiles workflows for execution.

---

## **Workflow Structure**

### **1. Input and Routing (`route_question`)**
- **Input:** A user-provided natural language query.
- **Functionality:** 
  - LangChain's LLM analyzes the query.
  - **Routing Logic (`route_question`):**
    - Outputs `next_node` as either:
      - `"wiki_search"`: For general knowledge queries.
      - `"vectorstore"`: For domain-specific questions.

---

### **2. Graph Workflow**
- **Framework:** Designed and executed with **LangGraph**.
- **Nodes:**
  - `route_question`: Decision-making node that determines the next step.
  - `wiki_search`: Handles Wikipedia-based general search.
  - `astra_db_retrieve`: Fetches domain-specific documents from Astra DB (a vector database).
- **Edges:**
  - `add_conditional_edges`: Routes queries dynamically based on `route_question`'s output.
  - Terminal edges (`END`) indicate workflow completion.

---

## **Graph Execution**

1. **Start**:
   - The workflow begins with a user query.
2. **Decision Point (`route_question`)**:
   - LangChain’s LLM evaluates the query and decides whether to:
     - Perform a Wikipedia search (`wiki_search`).
     - Fetch documents from the vectorstore (`astra_db_retrieve`).
3. **Processing Nodes**:
   - **`wiki_search`**: Queries Wikipedia using LangChain’s tools.
   - **`astra_db_retrieve`**: Retrieves vectorized domain-specific documents.
4. **Completion**:
   - The workflow ends after retrieving and formatting the output.

---

## **Core Functionalities**

### **1. Decision Logic with LangChain**
- **Routing with `route_question`:**
  - LangChain-powered LLM examines the query.
  - Dynamically determines the most relevant data source.

### **2. Knowledge Retrieval**
- **Vectorstore (Astra DB)**:
  - Stores and retrieves documents for domain-specific queries.
  - Integrated via LangChain’s vector database tools.
- **Wikipedia Search**:
  - Conducts real-time external lookups for general information.

### **3. Modular Workflow with LangGraph**
- **Node Definitions:**
  - Each functional block (e.g., `wiki_search`, `astra_db_retrieve`) is a node.
- **Dynamic Transitions:**
  - Conditional edges (`add_conditional_edges`) enable routing based on query type.
- **Visualization and Execution:**
  - LangGraph visualizes the workflow and compiles it for seamless execution.

---

## **Purpose and Applications**

1. **Dynamic Routing:**
   - Routes queries to the most relevant knowledge source based on their content.
2. **Knowledge Integration:**
   - Combines internal domain-specific data (via vectorstores) with external general knowledge (via Wikipedia).
3. **AI-Driven Workflow:**
   - Demonstrates the power of combining **LangChain** and **LangGraph** for creating adaptable, intelligent systems.
4. **Real-World Use Cases:**
   - Customer support, intelligent search systems, and AI-driven assistants.

---

## **How to Run the Workflow**
1. Clone the repository.
2. Install dependencies for **LangChain**, **LangGraph**, and vector database integration.
3. Define and load vectorstore data into Astra DB.
4. Run the graph-based workflow:
   ```python
   inputs = {"question": "Your question here"}
   for output in app.stream(inputs):
       print(output)

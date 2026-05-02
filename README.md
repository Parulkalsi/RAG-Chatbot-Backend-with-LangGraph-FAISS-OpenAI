This project implements an intelligent Retrieval-Augmented Generation (RAG) pipeline using LangGraph, LangChain, and OpenAI models. It dynamically decides whether to answer from general knowledge or retrieve relevant information from multiple PDF documents before generating a response.

🚀 Features

🔍 Dynamic Retrieval Decision
Uses LLM to decide whether external document retrieval is required
📚 Multi-PDF Knowledge Base
Supports multiple documents (Company Policies, Profile, Pricing, etc.)
🧠 Context-Aware Answering
Generates answers strictly from retrieved context when needed
🎯 Relevance Filtering
Filters only useful documents before passing to the LLM

🔄 Graph-Based Workflow
Built using LangGraph for modular and scalable pipelines

⚡ FAISS Vector Store
Fast similarity search for document retrieval

🏗️ Architecture

The workflow is implemented as a LangGraph State Machine:

START
  ↓
Decide Retrieval (LLM)
  ↓
 ┌───────────────┬─────────────────┐
 ↓               ↓
Retrieve Docs    Direct Answer
 ↓
Check Relevance (LLM)
 ↓
 ┌───────────────┬─────────────────┐
 ↓               ↓
Generate Answer  No Relevant Docs
 ↓
END

🛠️ Tech Stack
LangChain
LangGraph
OpenAI GPT (gpt-4o-mini)
FAISS (Vector DB)
Python
Pydantic

📂 Project Structure
├── main.py                  # Core pipeline logic
├── data/
│   ├── Company_Policies.pdf
│   ├── Company_Profile.pdf
│   ├── Product_and_Pricing.pdf
├── .env                    # API keys
├── requirements.txt
└── README.md

Example query:

result = chatbot.invoke({
    "question": "What is the refund policy of NEXAAI?"
})

print(result["answer"])
🧩 Key Components
1. Retrieval Decision

Determines if external documents are needed:
should_retrieve: bool

2. Document Retrieval
Uses FAISS similarity search
Top-K documents fetched
3. Relevance Filtering
LLM filters only useful documents
4. Response Generation
Two modes:
Direct LLM response
Context-based RAG response
💡 Example Flow

Input:

What is the refund policy of NEXAAI?

System Behavior:

Decides retrieval is required ✅
Fetches relevant PDF chunks 📄
Filters useful docs 🔍
Generates contextual answer 🤖

📈 Future Improvements
Add streaming responses
Integrate frontend UI (Streamlit/React)
Add memory for conversation history
Support multiple vector DBs (Pinecone)

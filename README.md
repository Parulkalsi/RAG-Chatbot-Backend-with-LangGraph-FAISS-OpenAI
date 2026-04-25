# RAG-Chatbot-Backend-with-LangGraph-FAISS-OpenAI
This project implements a Retrieval-Augmented Generation (RAG) chatbot backend using modern LLM orchestration tools.

It enables users to ask questions over a PDF document, where the system:

Retrieves relevant content from the document
Enhances the LLM response with context
Produces accurate, grounded answers

The project focuses on backend orchestration using LangGraph, making it modular, extensible, and production-ready.

🧠 How It Works
User Query
    ↓
LangGraph Agent (LLM + Tool Decision)
    ↓
RAG Tool Triggered
    ↓
FAISS Vector Store (Semantic Search)
    ↓
Relevant Chunks Retrieved
    ↓
LLM Generates Context-Aware Response

⚙️ Tech Stack
LLM & Orchestration: LangGraph, LangChain, OpenAI
Embeddings: OpenAI Embeddings (text-embedding-3-small)
Vector Database: FAISS
Document Loader: PyPDFLoader
Text Splitting: RecursiveCharacterTextSplitter
Tooling: LangGraph ToolNode
Environment Management: python-dotenv

✨ Key Features
📄 Document Understanding (RAG)
Loads PDF documents using PyPDFLoader
Splits text into manageable chunks
Stores embeddings in FAISS vector database

🔍 Semantic Retrieval
Retrieves top-k relevant chunks using similarity search
Ensures context-aware and accurate responses

🧠 Agentic Workflow (LangGraph)
Uses StateGraph to manage flow
Dynamically decides when to call RAG tool
Maintains conversation state

🔧 Tool Integration
📚 RAG Tool

Retrieves relevant document context
Returns:
Query
Context
Metadata
📂 Project Structure
├── rag_chatbot.py        # Main LangGraph RAG pipeline
├── intro-to-ml.pdf       # Source document
├── requirements.txt
└── .env

🔌 Core Components
1. Document Loading
loader = PyPDFLoader("intro-to-ml.pdf")
docs = loader.load()

3. Text Splitting
splitter = RecursiveCharacterTextSplitter(
    chunk_size=1000,
    chunk_overlap=200
)

4. Embeddings + Vector Store
embeddings = OpenAIEmbeddings(model="text-embedding-3-small")
vectorstore = FAISS.from_documents(chunk, embeddings)

6. Retriever
retriever = vectorstore.as_retriever(
    search_type="similarity",
    search_kwargs={"k": 3}
)

7. RAG Tool
Fetches relevant chunks from vector store
Supplies context to LLM for grounded responses

9. LangGraph Workflow
chat_node → LLM response
tools → executes RAG tool if needed
Conditional routing using tools_condition

▶️ How to Run
1. Install dependencies
pip install -r requirements.txt
2. Set environment variables

Create .env file:

OPENAI_API_KEY=your_api_key_here

3. Run the script
python rag_chatbot.py
🧪 Example Use Cases
“What is machine learning?”
“Explain supervised learning from the document”
“Summarize key concepts from the PDF”

🚧 Future Improvements
Add FastAPI interface for API access
Build Streamlit UI for interaction
Support multiple documents
Deploy using Docker & AWS

🎯 What I Learned
Building RAG pipelines from scratch
Using FAISS for vector similarity search
Designing agentic workflows with LangGraph
Integrating LLMs with external knowledge sources
Structuring scalable AI backends

# ChatBot Using RAG

A demo application showcasing a Retrieval-Augmented Generation (RAG) system built with **LangGraph** and **Streamlit**. It features an AI agent equipped with both mathematical calculation tools and a local knowledge base search. 

## 🚀 Features

- **Agentic Workflow**: Uses LangGraph to orchestrate decisions between answering directly or using tools.
- **RAG Capabilities**: Local vector search using **FAISS** and **Google Gemini Embeddings**.
- **Interactive UI**: A sleek **Streamlit** chat interface with a live sidebar tracing the agent's tool calls and thought process.
- **High-Speed Inference**: Powered by **Groq** for rapid LLM responses.
- **Built-in Tools**: Includes standard mathematical tools (`add`, `multiply`, `divide`) alongside a `search_docs` tool for RAG.

## 🛠️ Tech Stack

- **Python**: `>=3.13`
- **Frontend**: [Streamlit](https://streamlit.io/)
- **Orchestration**: [LangGraph](https://python.langchain.com/v0.1/docs/langgraph/) & [LangChain](https://langchain.com/)
- **LLM Provider**: [Groq](https://groq.com/) (`openai/gpt-oss-20b`)
- **Embeddings**: Google Generative AI (`models/gemini-embedding-001`)
- **Vector Database**: [FAISS](https://github.com/facebookresearch/faiss) (Local)
- **Package Manager**: [uv](https://github.com/astral-sh/uv)

## 📁 Project Structure

```text
.
├── app.py                # Streamlit UI, chat interface, and tool trace rendering
├── agent.py              # LangGraph state graph definition, tools, and LLM setup
├── ingest.py             # Script to chunk documents and build the FAISS vector index
├── sample_docs/          # Source .txt documents for the knowledge base
├── faiss_index/          # Generated FAISS local vector database
├── experiments.ipynb     # Jupyter notebook for experimentation and prototyping
├── pyproject.toml        # Project dependencies and configuration (uv)
└── .env                  # Environment variables (API keys)
```

## ⚙️ Setup & Installation

### 1. Environment Variables
Create a `.env` file in the root directory and add your API keys:
```env
GROQ_API_KEY=your_groq_api_key
GOOGLE_API_KEY=your_google_api_key
```

### 2. Install Dependencies
This project uses `uv` for lightning-fast dependency management.
```bash
uv sync
```

### 3. Build the Vector Database
Before running the app, index the sample documents from the `sample_docs/` directory:
```bash
uv run python ingest.py
```
*This will read all `.txt` files, chunk them, embed them using Google Gemini, and save the index to the `faiss_index/` directory.*

### 4. Run the Application
Start the Streamlit development server:
```bash
uv run streamlit run app.py
```

## 💡 How it Works
pank
1. **User Input**: You ask a question in the Streamlit UI.
2. **LangGraph Agent**: The agent analyzes the prompt. If it involves math, it uses the calculator tools. If it's about AI/ML/LangGraph, it triggers the `search_docs` tool.
3. **Retrieval**: The `search_docs` tool queries the local FAISS index and retrieves relevant document chunks.
4. **Synthesis**: The LLM synthesizes the tool outputs and generates a final response.
5. **Trace Sidebar**: The Streamlit sidebar updates in real-time, displaying the exact inputs and outputs of the tools used during the turn.

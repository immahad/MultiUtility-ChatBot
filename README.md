# Multi-Utility Chatbot

A versatile, multi-functional chatbot powered by **LangGraph**, **LangChain**, and **Groq** (Llama 3). This application provides a unified conversational interface with access to various external tools, including real-time web search, a calculator, live stock prices, and PDF document retrieval (RAG).

## Features
- **Intelligent Routing**: The chatbot autonomously decides when to answer directly or when to utilize one of its tools.
- **RAG (Retrieval-Augmented Generation)**: Upload a PDF file, and the chatbot will automatically chunk, embed, and index it using FAISS. You can then ask questions about the document.
- **Web Search**: Integrated with DuckDuckGo to pull in real-time information from the web.
- **Stock Prices**: Fetches live stock quotes using the Alpha Vantage API.
- **Conversation Memory**: Chat histories are persisted locally using an SQLite database (`chatbot_state.db`).
- **Interactive UI**: A beautiful, streaming interface built with Streamlit that clearly displays when tools are being used.

## Prerequisites
You will need API keys for the following services:
- **[Groq](https://console.groq.com/keys)**: For lightning-fast LLM inference.
- *(Optional)* **LangChain Smith**: For tracing and debugging.

## Installation & Deployment

1. **Clone the repository:**
   ```bash
   git clone <your-repository-url>
   cd ChatBot
   ```

2. **Set up a virtual environment (recommended):**
   ```bash
   python -m venv myenv
   # On Windows
   myenv\Scripts\activate
   # On macOS/Linux
   source myenv/bin/activate
   ```

3. **Install the dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set your Environment Variables:**
   Create a `.env` file in the root of the project and add your API keys:
   ```env
   GROK_API_KEY="your-groq-api-key"
   LANGCHAIN_TRACING_V2=true
   LANGCHAIN_ENDPOINT="https://api.smith.langchain.com"
   LANGCHAIN_API_KEY="your-langsmith-api-key"
   LANGCHAIN_PROJECT="chatBot"
   ```

## Usage

Start the Streamlit application locally:

```bash
streamlit run ChatBot_frontend.py
```

- Open the provided local URL (usually `http://localhost:8501`) in your browser.
- **Chat**: Start typing to chat with the Llama 3 model.
- **Upload PDFs**: Use the sidebar to upload a PDF. Once indexed, ask questions about its content.
- **Tools**: Try asking "What is the stock price of AAPL?", "Search the web for...", or "Calculate 254 * 84".
- **Past Conversations**: Use the sidebar to jump back into previous chat threads.

## Project Structure
- `langgraph_backend.py`: The core backend logic. Handles the LangGraph state machine, tool definitions, PDF ingestion, and SQLite checkpointer.
- `ChatBot_frontend.py`: The Streamlit frontend. Handles user interactions, streaming responses, PDF uploads, and chat history rendering.
- `requirements.txt`: List of Python dependencies required to run the project.

# AI PDF Chatbot & Agent Powered by LangChain and LangGraph

![Chatbot UI Demo](docs/chatbot-ui-demo.png)

A sophisticated AI-powered chatbot application that enables users to upload, ingest, and query PDF documents using natural language. Built with modern technologies including LangChain, LangGraph, Next.js, and TypeScript.

## Table of Contents

- [Features](#features)
- [Architecture Overview](#architecture-overview)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Environment Variables](#environment-variables)
  - [Frontend Variables](#frontend-variables)
  - [Backend Variables](#backend-variables)
- [Local Development](#local-development)
  - [Running the Backend](#running-the-backend)
  - [Running the Frontend](#running-the-frontend)
- [Usage](#usage)
  - [Uploading/Ingesting PDFs](#uploadingingesting-pdfs)
  - [Asking Questions](#asking-questions)
  - [Viewing Chat History](#viewing-chat-history)
- [Production Build & Deployment](#production-build--deployment)
- [Customizing the Agent](#customizing-the-agent)
- [Troubleshooting](#troubleshooting)
- [Next Steps](#next-steps)

## Features

### 🤖 Intelligent Chat Interface
- **Modern UI Design**: Clean, responsive chat interface with message bubbles and user avatars
- **Real-time Responses**: Fast, streaming responses for smooth user experience
- **Source Citation**: Automatic source highlighting with page numbers and document references
- **Chat History**: Persistent conversation history with context preservation

### 📄 Document Processing
- **PDF Upload & Ingestion**: Drag-and-drop or click-to-upload PDF documents
- **Multi-Document Support**: Process multiple PDFs simultaneously
- **Smart Chunking**: Intelligent document segmentation for better retrieval
- **Metadata Extraction**: Automatic extraction of document metadata

### 🔍 Advanced RAG Capabilities
- **Semantic Search**: Advanced vector similarity search for accurate answers
- **Context-Aware Responses**: Answers based on retrieved document context
- **Source Transparency**: Clear indication of which documents and pages were used
- **Follow-up Questions**: Support for conversational follow-ups with context

### 🛠 Technical Features
- **LangGraph Integration**: Complex agent workflows with state management
- **LangChain Framework**: Comprehensive LLM integration and tool usage
- **TypeScript Support**: Full TypeScript implementation for type safety
- **Modern Stack**: Next.js 14, React 18, Tailwind CSS

## Architecture Overview

```
pdf-chatbot-ai-longchain/
├── frontend/                 # Next.js frontend application
│   ├── app/                 # App router pages
│   ├── components/          # React components
│   ├── lib/                 # Utility libraries
│   └── types/               # TypeScript type definitions
├── backend/                 # FastAPI backend server
│   ├── src/                 # Source code
│   │   ├── ingestion/       # Document processing pipeline
│   │   ├── retrieval/       # RAG retrieval logic
│   │   └── shared/          # Shared utilities
│   └── requirements.txt     # Python dependencies
└── scripts/                 # Build and utility scripts
```

### Key Components

1. **Frontend (Next.js)**
   - Chat interface with real-time messaging
   - File upload component for PDF ingestion
   - Source display with page references
   - Responsive design with Tailwind CSS

2. **Backend (FastAPI)**
   - Document ingestion pipeline
   - Vector database integration
   - LangGraph agent workflows
   - RESTful API endpoints

3. **AI/ML Stack**
   - LangChain for LLM orchestration
   - LangGraph for complex agent workflows
   - Vector embeddings for semantic search
   - Retrieval-augmented generation (RAG)

## Prerequisites

- **Node.js** (v18 or higher)
- **Python** (v3.9 or higher)
- **Git**
- **OpenAI API Key** (for LLM functionality)
- **Vector Database** (Pinecone, ChromaDB, or similar)

## Installation

### 1. Clone the Repository
```bash
git clone https://github.com/TrineshCh/RAG-Document-Intelligence-System.git
cd RAG-Document-Intelligence-System/pdf-chatbot-ai-longchain
```

### 2. Install Frontend Dependencies
```bash
cd frontend
npm install
# or
yarn install
```

### 3. Install Backend Dependencies
```bash
cd backend
pip install -r requirements.txt
```

### 4. Set Up Environment Variables
Create `.env` files in both frontend and backend directories (see Environment Variables section).

## Environment Variables

### Frontend Variables

Create a `.env.local` file in the `frontend/` directory:

```env
# API Configuration
NEXT_PUBLIC_API_URL=http://localhost:8000
NEXT_PUBLIC_WS_URL=ws://localhost:8000

# Application Configuration
NEXT_PUBLIC_APP_NAME="PDF Chatbot AI"
NEXT_PUBLIC_MAX_FILE_SIZE=10485760  # 10MB in bytes

# Feature Flags
NEXT_PUBLIC_ENABLE_ANALYTICS=false
NEXT_PUBLIC_ENABLE_DEBUG=true
```

### Backend Variables

Create a `.env` file in the `backend/` directory:

```env
# LLM Configuration
OPENAI_API_KEY=your_openai_api_key_here
OPENAI_MODEL=gpt-4-turbo-preview
OPENAI_TEMPERATURE=0.1

# Vector Database
VECTOR_DB_TYPE=pinecone  # or chroma, faiss
PINECONE_API_KEY=your_pinecone_api_key
PINECONE_INDEX_NAME=pdf-chatbot-index
PINECONE_ENVIRONMENT=your_pinecone_environment

# Database Configuration
DATABASE_URL=postgresql://user:password@localhost:5432/pdf_chatbot

# Application Settings
DEBUG=true
LOG_LEVEL=INFO
MAX_CONCURRENT_REQUESTS=10
```

## Local Development

### Running the Backend

1. **Navigate to Backend Directory**
```bash
cd backend
```

2. **Activate Virtual Environment** (Recommended)
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Start the FastAPI Server**
```bash
uvicorn src.main:app --reload --host 0.0.0.0 --port 8000
```

The backend API will be available at `http://localhost:8000`

### Running the Frontend

1. **Navigate to Frontend Directory**
```bash
cd frontend
```

2. **Start the Development Server**
```bash
npm run dev
# or
yarn dev
```

The frontend will be available at `http://localhost:3000`

## Usage

### Uploading/Ingesting PDFs

1. **Access the Upload Interface**
   - Navigate to the main chat interface
   - Click the upload button or drag-and-drop PDF files

2. **Supported File Types**
   - PDF documents (.pdf)
   - Maximum file size: 10MB (configurable)

3. **Ingestion Process**
   - Documents are automatically processed and chunked
   - Text is extracted and embedded into vector database
   - Metadata is extracted and stored
   - Progress indicators show ingestion status

### Asking Questions

1. **Type Your Question**
   - Enter questions in natural language
   - Use specific queries for better results
   - Reference document content if needed

2. **Receive AI Responses**
   - Answers are generated based on document content
   - Sources are cited with page numbers
   - Follow-up questions maintain context

3. **Source References**
   - Each answer includes source citations
   - Click on sources to view original document excerpts
   - Page numbers and document names are displayed

### Viewing Chat History

1. **Conversation Persistence**
   - All conversations are saved automatically
   - History is maintained across sessions
   - Context is preserved for follow-up questions

2. **Chat Management**
   - View previous conversations in sidebar
   - Start new chat sessions
   - Export chat history if needed

## Production Build & Deployment

### Frontend Build

```bash
cd frontend
npm run build
npm start
```

### Backend Deployment

```bash
cd backend
pip install -r requirements.txt
gunicorn src.main:app -w 4 -k uvicorn.workers.UvicornWorker
```

### Docker Deployment

```bash
# Build and run with Docker Compose
docker-compose up -d
```

## Customizing the Agent

### Modifying Prompts

Edit the prompt templates in `backend/src/prompts.py`:

```python
SYSTEM_PROMPT = """
You are an AI assistant specialized in answering questions based on provided documents.
Always cite your sources and be accurate in your responses.
"""
```

### Adding New Tools

Extend the agent capabilities by adding new tools in `backend/src/tools/`:

```python
from langchain.tools import BaseTool

class CustomTool(BaseTool):
    name = "custom_tool"
    description = "Description of what this tool does"
    
    def _run(self, query: str) -> str:
        # Tool implementation
        return result
```

### Adjusting Retrieval Parameters

Modify retrieval settings in `backend/src/config.py`:

```python
RETRIEVAL_CONFIG = {
    "chunk_size": 1000,
    "chunk_overlap": 200,
    "max_retrieved_docs": 5,
    "similarity_threshold": 0.7
}
```

## Troubleshooting

### Common Issues

1. **PDF Upload Fails**
   - Check file size limits
   - Verify PDF format compatibility
   - Ensure backend is running

2. **No Responses from AI**
   - Verify OpenAI API key is valid
   - Check backend logs for errors
   - Ensure vector database is accessible

3. **Slow Response Times**
   - Optimize chunk size and overlap
   - Consider using smaller models for faster responses
   - Check system resources

### Debug Mode

Enable debug logging by setting:
```env
DEBUG=true
LOG_LEVEL=DEBUG
```

### Performance Optimization

1. **Vector Database Tuning**
   - Adjust similarity thresholds
   - Optimize indexing strategy
   - Consider database scaling

2. **LLM Optimization**
   - Use appropriate model sizes
   - Implement response caching
   - Batch requests when possible

## Next Steps

### Planned Features

- [ ] Multi-language support
- [ ] Advanced document formats (Word, Excel)
- [ ] Collaborative chat sessions
- [ ] Advanced analytics dashboard
- [ ] Integration with cloud storage
- [ ] Mobile application

### Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

### Support

For issues and questions:
- Create an issue on GitHub
- Check the troubleshooting section
- Review the documentation

---

**Built with ❤️ using LangChain, LangGraph, Next.js, and modern web technologies.**

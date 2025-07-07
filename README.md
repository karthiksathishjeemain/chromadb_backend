"# ChromaDB Backend

A FastAPI-based backend service that provides vector storage and semantic search capabilities using ChromaDB.

## Features

- **Store Documents**: Store text summaries with metadata for semantic search
- **Semantic Search**: Query stored documents using natural language
- **Persistent Storage**: ChromaDB data persists locally in the `chroma_db` directory
- **CORS Enabled**: Ready for frontend integration
- **RESTful API**: Simple HTTP endpoints for easy integration

## Tech Stack

- **FastAPI**: Modern, fast web framework for building APIs
- **ChromaDB**: Vector database for storing and querying embeddings
- **Pydantic**: Data validation using Python type annotations
- **Uvicorn**: ASGI server for running the application

## Installation

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd chromadb_backend
   ```

2. **Create a virtual environment**:
   ```bash
   python -m venv mynv
   mynv\Scripts\activate  # On Windows
   # source mynv/bin/activate  # On macOS/Linux
   ```

3. **Install dependencies**:
   ```bash
   pip install fastapi chromadb uvicorn
   ```

## Usage

### Starting the Server

Run the application locally:

```bash
python main.py
```

The server will start on `http://localhost:3001`

### API Endpoints

#### Store Data
Store a document with metadata for later retrieval.

**POST** `/store`

```json
{
    "summary": "Your document text here",
    "cid": "unique-content-id",
    "metadata": {
        "optional": "metadata fields"
    }
}
```

**Response**:
```json
{
    "message": "Stored successfully",
    "cid": "unique-content-id"
}
```

#### Search Data
Search for similar documents using natural language queries.

**POST** `/search`

```json
{
    "query": "your search query here"
}
```

**Response**:
```json
{
    "results": [
        {
            "cid": "content-id",
            "score": 0.85,
            "metadata": {
                "cid": "content-id",
                "optional": "metadata fields"
            }
        }
    ]
}
```

## Project Structure

```
chromadb_backend/
├── main.py              # Main FastAPI application
├── chroma_db/           # ChromaDB persistent storage directory
├── mynv/                # Virtual environment
├── vercel.json          # Vercel deployment configuration
└── README.md            # This file
```

## How It Works

1. **Document Storage**: When you store a document, ChromaDB automatically generates vector embeddings from the text and stores them along with the original text and metadata.

2. **Semantic Search**: When you search, ChromaDB converts your query into embeddings and finds the most similar stored documents using cosine similarity.

3. **Scoring**: Results include a similarity score (0-1, where 1 is most similar) calculated as `1 - distance`.

## Development

### Local Development
```bash
# Install development dependencies
pip install fastapi chromadb uvicorn

# Run the server with auto-reload
uvicorn main:app --reload --host 0.0.0.0 --port 3001
```

### Testing the API

You can test the API using curl or any HTTP client:

```bash
# Store a document
curl -X POST "http://localhost:3001/store" \
     -H "Content-Type: application/json" \
     -d '{
       "summary": "This is a sample document about machine learning",
       "cid": "doc-001",
       "metadata": {"category": "AI", "author": "John Doe"}
     }'

# Search for documents
curl -X POST "http://localhost:3001/search" \
     -H "Content-Type: application/json" \
     -d '{"query": "artificial intelligence"}'
```

## Deployment

### Local Deployment
The application is ready to run locally with persistent storage.

### Cloud Deployment Notes
⚠️ **Important**: ChromaDB with persistent storage may not work on serverless platforms like Vercel due to ephemeral filesystems. For production deployment, consider:

- Using ChromaDB Cloud
- Deploying to platforms with persistent storage (Railway, Render, DigitalOcean)
- Using alternative vector databases that support cloud storage

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

[Add your license here]" 

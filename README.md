# MovieMate (TMDB ChatBot)  

Conversational AI for intelligent movie search and recommendations

## Features

- **Semantic search** over 4000+ movies using embeddings
- **Metadata filtering** (year, genre, rating, runtime)
- **Hybrid reranking** (semantic score + keyword overlap)
- **Conversational chatbot** powered by Ollama (llama3.2:3b by default)
- **Interactive Gradio UI** with streaming responses
- Fully local (except initial TMDB data fetch)

## Tech Stack

- **Data**: [TMDB API](https://www.themoviedb.org/)
- **Embeddings**: `all-MiniLM-L6-v2` (Sentence-Transformers)
- **Vector Search**: FAISS
- **Re-ranking**: `ms-marco-MiniLM-L-6-v2` (Cross-Encoder)
- **LLM**: Ollama 
- **UI**: Gradio
- **Others**: pandas, numpy, python-dotenv

## Installation

### 1. Clone & Setup Environment

```bash
git clone https://github.com/rks746/tmdb-chatbot.git
```

### 2. Install Dependencies

Run the first cell in `moviemate_notebook.ipynb` (it installs everything via pip).

### 3. TMDB API Key

1. Get a free API key at [https://www.themoviedb.org/settings/api](https://www.themoviedb.org/settings/api)
2. Create a `.env` file in the root:

```env
TMDB_API_KEY=your_actual_key_here
```

### 4. Ollama (Local LLM)

```bash
# Install Ollama from https://ollama.com
ollama pull llama3.2:3b # or any other model
```

## Quick Start

1. Open `moviemate_notebook.ipynb`
2. Run cells from top to bottom:
   - Setup & Installation
   - Configuration
   - Data Collection (downloads ~4000 movies)
   - Embedding & Vector Indexing
   - Chatbot Demo (terminal + Gradio)
3. Launch the Gradio UI at the bottom of the notebook.

## Project Structure

```
tmdb-chatbot/
├── moviemate_notebook.ipynb     # Main notebook (all code + demo)
├── data/
│   └── movies.csv               # Saved movie dataset
├── index/
│   ├── faiss_index.faiss        # FAISS vector index
│   └── faiss_index.pkl          # Document mapping
├── .env                         # TMDB API key (gitignored)
└── README.md
```

## How It Works

1. **Data Collection** – Pulls popular movies from TMDB with full details + cast/crew.
2. **Document Building** – Converts each movie into a rich natural-language string.
3. **Embedding + FAISS** – Creates 384-dim embeddings and builds a cosine-similarity index.
4. **Search Pipeline**:
   - Semantic retrieval → Metadata filtering → Keyword reranking
5. **Chatbot** – Ollama uses retrieved movies as context to answer naturally.

## Improvements & TODOs

- Add `filter_movies()` helper function
- Implement true genre-balanced data collection
- Implement a chunking algorithm 
- Docker support
- More advanced filtering (cast, director, language)

# MovieMate (TMDB ChatBot)  

Conversational AI for intelligent movie search and recommendations

## Features

- **Semantic search** over 4000 movies using vector embeddings
- **Metadata filtering** based on year, genre, rating, runtime
- **Hybrid reranking** (semantic score + keyword overlap)
- **Conversational chatbot** powered by Ollama (llama3.2:3b) or Groq (openai/gpt-oss-120b)
- **Interactive Gradio UI** for streaming responses
- **LLM Evalution** with Ragas

## Tech Stack

- **Data**: [TMDB API](https://www.themoviedb.org/)
- **Embeddings**: `all-MiniLM-L6-v2` (Sentence-Transformers)
- **Vector Search**: FAISS
- **Re-ranking**: `ms-marco-MiniLM-L-6-v2` (Cross-Encoder)
- **LLM**: run via Ollama / Groq
- **UI**: Gradio
- **Evaluation**: Ragas
- **Others**: pandas, numpy, python-dotenv

## Installation

### 1. Clone & Setup Environment

```bash
git clone https://github.com/rks746/tmdb-chatbot.git
```

### 2. Install Dependencies

Run the first cell in `moviemate_notebook.ipynb` (it installs everything via pip).

### 3. TMDB API Key

1. Get a free TMDB API key at [https://www.themoviedb.org/settings/api](https://www.themoviedb.org/settings/api)
2. Get a free Groq API key at [https://console.groq.com/keys](https://console.groq.com/keys)
3. Create a `.env` file in the root:

```env
TMDB_API_KEY=your_actual_key_here
GROQ_API_KEY=your_groq_api_key_here
```

### 4. Ollama (Local LLM) (to run LLM locally)

```bash
# Install Ollama from https://ollama.com
ollama pull llama3.2:3b # or any other model
```

## Project Structure

```
tmdb-chatbot/
├── rag_and_evaluation.ipynb     # RAG pipeline and performance evaluation
├── data_collection.ipynb        # contains code to pull movies dataset from TMDB
├── eda.ipynb                    # exploratory data analysis
├── data/
│   └── movies.csv               # Saved movie dataset
├── index/
│   ├── faiss_index.faiss        # FAISS vector index
│   └── faiss_index.pkl          # Document mapping
├── .env                         # API keys (gitignored)
└── README.md
```

## How It Works

1. **Data Collection** – Pulls popular movies from TMDB with full details + cast/crew.
2. **Document Building** – Converts each movie into a rich natural-language string.
3. **Embedding + FAISS** – Creates 384-dimension embeddings and builds a cosine-similarity index.
4. **Search Pipeline** - Semantic retrieval → Metadata filtering → Keyword reranking
5. **LLM Eval** - Judges the system output on metrics like faithfulness, context_precision, context_recall and answer_relevancy

## Improvements & TODOs

- Add `filter_movies()` helper function
- Implement true genre-balanced data collection
- Implement a chunking algorithm 
- Docker support
- More advanced filtering (cast, director, language)
- Implement multi-turn LLM evaluation

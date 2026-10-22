# 🎬 CINEBOT — Generative AI Movie Recommendation Chatbot

CINEBOT is a movie-recommendation chatbot built with **Retrieval-Augmented Generation (RAG)**. It combines semantic search over movie metadata with an open-source language model to answer natural-language movie queries and suggest films based on a user's interests, genre preferences, or mood.

## ✨ Features

- **Natural-language movie queries:** Ask for recommendations using ordinary descriptions, genres, themes, or moods.
- **Semantic retrieval:** Uses Sentence Transformers to represent movie metadata and user queries as embeddings.
- **FAISS similarity search:** Retrieves the five closest movie matches from the indexed dataset.
- **LLM-generated responses:** Uses TinyLlama to turn retrieved movie titles and the user's question into a conversational response.
- **Interactive interface:** Provides a simple chatbot UI using Gradio.
- **Movie metadata processing:** Combines movie overviews, genres, keywords, and director information into searchable tags.

## 🧠 How It Works

1. Load the TMDB 5000 Movies and Credits CSV files.
2. Merge the datasets and select the title, overview, genres, keywords, cast, and crew fields.
3. Parse metadata and extract genres, keywords, cast names, and director names.
4. Combine selected metadata into a text field (`tags`) for each movie.
5. Encode the tags using the `all-MiniLM-L6-v2` Sentence Transformer model.
6. Add the embeddings to a FAISS `IndexFlatL2` index.
7. Embed a user's query and retrieve the five nearest movie titles.
8. Pass the retrieved titles and user query into TinyLlama to generate a response.
9. Display the response through a Gradio interface.

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| Google Colab / Jupyter Notebook | Development and execution environment |
| Pandas | Loading, merging, and preprocessing movie data |
| Sentence Transformers (`all-MiniLM-L6-v2`) | Text embedding generation |
| FAISS (`faiss-cpu`) | Vector similarity search |
| Hugging Face Transformers | Loading and running the language model |
| TinyLlama (`TinyLlama-1.1B-Chat-v1.0`) | Natural-language response generation |
| Gradio | Interactive chatbot interface |
| NumPy | Numerical operations on embeddings |

## 📂 Repository Contents

- `CINEBOT.ipynb` — Notebook containing data preparation, embedding generation, retrieval, language generation, and Gradio UI code.
- `Explanation.pdf` — Project explanation, architecture, implementation overview, technologies, and example results.
- `README.md` — Project overview and usage notes.

## 🚀 Running the Notebook

The notebook was prepared for **Google Colab**.

1. Open `CINEBOT.ipynb` in Google Colab.
2. Run the dependency-installation cells.
3. Upload the two dataset files when prompted:
   - `tmdb_5000_movies.csv`
   - `tmdb_5000_credits.csv`
4. Run the notebook cells in order. The notebook preprocesses the data, builds the FAISS index, loads TinyLlama, and launches the Gradio interface.

The notebook installs these packages:

```bash
pip install transformers sentence-transformers faiss-cpu langchain gradio accelerate bitsandbytes
```

Depending on the runtime and available hardware, model downloads and inference may take some time. The notebook uses a `share=True` Gradio launch, which creates a temporary public sharing link; only use this when appropriate for your environment.

## 📊 Dataset and Scope

The project uses the **TMDB 5000 Movies** and **TMDB 5000 Credits** datasets. In the notebook, the merged data is reduced to the first 1,000 rows after null values are removed. Search quality and coverage are therefore limited to the subset indexed by the notebook.

The indexed text includes genres, keywords, overview, and director information. Although cast data is extracted during preprocessing, the final `tags` construction in the notebook does not include cast names.

## ⚠️ Notes and Limitations

- The system retrieves movie titles and uses those titles as context for TinyLlama; it does not pass full movie metadata into the generation prompt.
- Generated responses can contain inaccurate details or recommendations. Verify movie information independently when accuracy matters.
- Results depend on the dataset subset, embedding model, nearest-neighbor search, and language-model output.
- The notebook is designed for Colab and expects the CSV files to be uploaded manually.
- The notebook uses an open-source model, but available memory, compute, and runtime configuration can affect execution.

## 🔮 Possible Future Improvements

- Index the full dataset instead of only the first 1,000 rows.
- Include cast and additional useful metadata in the tags.
- Pass richer retrieved movie details to the language model.
- Add movie posters, ratings, release dates, and links.
- Add conversation history and preference-aware recommendations.
- Evaluate retrieval relevance and generated-answer quality systematically.

## 📄 Project Documentation

See [`Explanation.pdf`](Explanation.pdf) for the project's written explanation, architecture, implementation steps, and sample interface results.

---

**Project:** CINEBOT — AI Movie Chatbot using RAG and an Open-Source LLM

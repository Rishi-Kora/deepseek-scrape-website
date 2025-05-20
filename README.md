# deepseek-scrape-website
A Jupyter Notebook project demonstrating how to scrape a website, analyze its content and related links, process the text into embeddings, and interact with the data using Deepseek (via Ollama or OpenAI API) for conversational retrieval.

## Features

- **Web Scraping**: Uses a custom `Website` loader to fetch page title, full text, and hyperlinks from any URL.
- **URL Analysis**: Automatically generates prompts to analyze links for resume relevance, domain extraction, and content summarization.
- **Deepseek Model Integration**: Connects to a local Ollama server or OpenAI-compatible endpoint to leverage the `deepseek-r1:1.5b` model.
- **Document Processing**: Reads model responses into a text file, wraps in a `Document`, and splits into manageable chunks.
- **Vector Store**: Computes embeddings (OpenAI or Hugging Face) and stores vectors persistently with Chroma.
- **Conversational Retrieval**: Builds a question-answer chain using `ChatOpenAI` or local Deepseek model, enriched with memory.
- **Interactive UI**: Provides code patterns for launching a Gradio app with URL input and chat interface.

## Requirements

- Python 3.8+
- Jupyter Notebook
- An OpenAI API key (set `OPENAI_API_KEY` in a `.env` file)
- Ollama running locally (`http://localhost:11434`) with `deepseek-r1:1.5b` model
- (Optional) Hugging Face API token for remote embeddings

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/deepseek-scrape-website.git
   cd deepseek-scrape-website
   ```

2. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Create a `.env` file in the root directory:
   ```env
   OPENAI_API_KEY=your_openai_api_key
   ```

5. Ensure Ollama is running locally with the Deepseek model:
   ```bash
   ollama run deepseek-r1:1.5b
   ```

## Notebook Walkthrough

Open the notebook:
```bash
jupyter notebook deepseek_scrape_website.ipynb
```

### Core Steps

1. **Load and Scrape**: Instantiate `Website(url)` to fetch title, text, and links.
2. **Analyze URLs**: Send link data to Deepseek for domain extraction and content summarization.
3. **Save Responses**: Write model output to `output.txt` and wrap in a LangChain `Document`.
4. **Text Splitting**: Split the document into overlapping chunks using `CharacterTextSplitter`.
5. **Embeddings & Chroma**: Generate embeddings and store in a persistent Chroma vector database.
6. **Conversational Chain**: Create a `ConversationalRetrievalChain` with `ChatOpenAI`, memory, and retriever for chat over your content.
7. **Gradio UI**: (Optional) Launch a Gradio Blocks app for URL input and chat interface.

## Configurable Parameters

- `db_name`: Directory for vector store (e.g., `scrape_website`).
- `MODEL`: AI model name (default: `o4-mini` or change to use Deepseek).
- Splitting parameters: `chunk_size`, `chunk_overlap`.
- Memory settings: `temperature`, `return_messages`.

## Contributing

1. Fork the repo.
2. Create a feature branch: `git checkout -b feature/your-feature`.
3. Commit your changes: `git commit -m "Add new feature"`.
4. Push to GitHub: `git push origin feature/your-feature`.
5. Open a Pull Request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

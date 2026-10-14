# RAG: Chat with your PDF

A Google Colab notebook that answers questions from an uploaded PDF using Retrieval-Augmented Generation (RAG). Answers come only from the document and show the source page numbers, so they can be checked.

## How it works

1. **Load the PDF** and extract the text page by page (pypdf).
2. **Split into chunks** of about 800 characters with 150 characters of overlap, keeping the page number for each chunk.
3. **Create embeddings** for every chunk with sentence-transformers (`all-MiniLM-L6-v2`).
4. **Search with FAISS**: the question is embedded and the 4 most similar chunks are retrieved.
5. **Ask the LLM** (Groq API) to answer only from those chunks, and to say so when the answer is not in the document.
6. **Show the answer** with the page numbers it came from.

## Tech stack

- Python
- pypdf
- sentence-transformers
- FAISS
- Groq API (LLM)
- Gradio (chat interface)
- Google Colab

## Demo

<!-- Add a screenshot here: drag the image into this file on GitHub, or use ![Demo](demo.png) -->
Screenshot / demo recording: *(add link here)*

## How to run

1. Open `RAG_Chat_with_PDF.ipynb` in Google Colab.
2. Create a free API key at [console.groq.com](https://console.groq.com).
3. In Colab, click the key icon (Secrets) on the left, add a secret named `GROQ_API_KEY`, paste your key, and turn on notebook access.
4. Run the cells from top to bottom, one at a time.
5. Upload a PDF when asked, then ask your questions in the chat interface.

The API key is read from Colab Secrets. It is not stored in the code.

## Limitations

- Works on PDFs with selectable text. Scanned image PDFs need OCR, which is not included.
- Answer quality depends on the retrieved chunks and the chosen model, and the model can still be wrong.
- Runs as a Colab notebook; it is not deployed as a hosted app.

## What I learned

- How embeddings and vector search find relevant text.
- Why documents are split into overlapping chunks before searching.
- How to limit an LLM to the given context so it hallucinates less.

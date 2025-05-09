# PDF Summarizer with Groq and LangChain

This project provides a Python script that loads PDF documents from an `assets` directory, combines their text content, and uses Groq's `ChatGroq` large language model via LangChain to generate concise summaries. It leverages `PyMuPDFLoader` for PDF parsing, `tiktoken` for token handling, and LangChain's prompt templates and output parsers for structured LLM interactions.

---

## Features

* **Bulk PDF Loading**: Automatically discovers and loads all PDF files under `./assets`.
* **Text Extraction**: Uses `PyMuPDFLoader` to extract text from each page of the PDFs.
* **Context Formatting**: Merges extracted page contents into a single context string for summarization.
* **LLM Summarization**: Utilizes Groq's `deepseek-r1-distill-llama-70b` model with LangChain to produce reliable, non-hallucinatory summaries.
* **Configurable Summary Length**: Specify the desired word count for the summary.

---

## Prerequisites

* Python 3.9+
* A Groq API key. You can sign up at [Groq](https://groq.com/) to obtain your key.

---

## Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/Amir-Hossein-shamsi/PDF-Summarizer.git
   cd pdf-summarizer-groq
   ```

2. Create and activate a Python virtual environment:

   ```bash
   python -m venv venv
   source venv/bin/activate    # On Windows: venv\\Scripts\\activate
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Place your PDF files in the `assets/` folder.

---

## Configuration

The script expects your Groq API key to be set in the source (or via environment variable). Edit the `groq_api_key` variable or export it:

```bash
export GROQ_API_KEY="gsk_..."
```

In the script, you can also directly assign:

```python
groq_api_key = os.getenv("GROQ_API_KEY", "gsk_...")
```

---

## Usage

Run the summarization script:

```bash
python summarize_pdfs.py
```

By default, the script will:

1. Walk the `assets/` directory to find all `.pdf` files.
2. Load and extract text from each PDF using `PyMuPDFLoader`.
3. Concatenate the extracted text into a single context string.
4. Invoke the Groq LLM via a LangChain chain to generate a **50-word** summary of the first 5000 characters of the context.
5. Print the summary to the console.

### Customizing the Summary

To change the summary length or context slice, modify the invocation section:

```python
response = summary_chain.invoke({
    'context': context[:5000],  # adjust character slice
    'words': 100               # desired summary length in words
})
print(response)
```

---

## Code Structure

```
.
├── assets/               # Directory for PDF files
├── summarize_pdfs.py     # Main Python script
├── requirements.txt      # Python dependencies
└── README.md             # This documentation
```

* **summarize\_pdfs.py**: Contains all code for loading PDFs, formatting text, and calling the LLM.
* **requirements.txt**: Lists required packages (e.g., `langchain-groq`, `langchain`, `tiktoken`, `PyMuPDF`, `pydantic`).

---

## Dependencies

```text
langchain-groq
langchain
langchain-community
pydantic
tiktoken
PyMuPDF
```

Install via:

```bash
pip install langchain-groq langchain langchain-community pydantic tiktoken PyMuPDF
```

---

## Contributing

Contributions are welcome! Please fork the repo and submit a pull request with your improvements.

---

## License

This project is released under the MIT License.

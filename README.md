# Retrieval Augmented Generation (RAG)

A powerful Python application that demonstrates Retrieval Augmented Generation (RAG) using Google's Gemini AI and LangChain. This project enables intelligent question-answering over PDF documents by combining document retrieval with large language model generation.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)

## Features

- ** PDF Document Processing**: Extract and process text from multiple PDF files
- ** Intelligent Document Retrieval**: Use FAISS vector database to efficiently retrieve relevant information from large document collections
- ** AI-Powered Generation**: Leverage Google's Gemini Pro model to generate accurate, context-aware answers
- ** Interactive Chat Interface**: User-friendly Streamlit web interface for document interaction
- ** Semantic Search**: Advanced embedding-based similarity search for finding relevant document chunks
- ** Context-Aware Responses**: Combines retrieved context with LLM capabilities for detailed answers
- ** Fast Vector Search**: FAISS-based indexing for rapid similarity search at scale

##  How It Works

![RAG Pipeline](https://mallahyari.github.io/rag-ebook/diagrams/rag_pipeline_simplified.png)

The application implements a complete RAG pipeline:

1. **Document Ingestion**: Upload PDF documents through the web interface
2. **Text Extraction**: Extract text content from PDF files using PyPDF2
3. **Text Chunking**: Split documents into manageable chunks using RecursiveCharacterTextSplitter
4. **Embedding Generation**: Convert text chunks into vector embeddings using Google's embedding model
5. **Vector Storage**: Store embeddings in FAISS vector database for efficient retrieval
6. **Query Processing**: Convert user questions into embeddings
7. **Similarity Search**: Find most relevant document chunks based on semantic similarity
8. **Answer Generation**: Generate detailed answers using Gemini Pro with retrieved context

##  Quick Start

### Prerequisites

- Python 3.8 or higher
- Google API key for Gemini AI ([Get it here](https://makersuite.google.com/app/apikey))
- pip package manager

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/CodeX-Addy/Retrieval_Augmented_Generation.git
   cd Retrieval_Augmented_Generation
   ```

2. **Install required dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up environment variables**
   
   Create a `.env` file in the project root directory:
   ```bash
   touch .env
   ```
   
   Add your Google API key to the `.env` file:
   ```
   GOOGLE_API_KEY=your_google_api_key_here
   ```

##  Usage

### Option 1: Streamlit Web Application (Recommended)

Launch the interactive web interface:

```bash
streamlit run app.py
```

This will open a browser window with the application. Then:

1. **Upload PDFs**: Use the sidebar to upload one or more PDF files
2. **Process Documents**: Click "Submit & Process" to extract and index the content
3. **Ask Questions**: Enter your questions in the text input field
4. **Get Answers**: Receive detailed, context-aware responses based on your documents

### Option 2: Command-Line Interface

For programmatic access or integration into other scripts:

```bash
python chatbot-assistance.py
```

**Note**: This version requires you to modify the script to specify PDF file paths directly in the code.

##  Project Structure

```
Retrieval_Augmented_Generation/
│
├── app.py                      # Main Streamlit web application
├── chatbot-assistance.py       # Command-line version of the chatbot
├── requirements.txt            # Python dependencies
├── .env                        # Environment variables (create this)
├── .gitignore                 # Git ignore rules
├── LICENSE                    # MIT License
├── README.md                  # This file
└── faiss_index/               # Generated FAISS vector store (created at runtime)
```

##  Configuration

### Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `GOOGLE_API_KEY` | Your Google Generative AI API key | Yes |

### Model Configuration

The application uses the following models:
- **Embeddings**: `models/embedding-001` (Google Generative AI)
- **Generation**: `gemini-pro` (Google Generative AI)
- **Temperature**: 0.3 (for consistent responses)

### Vector Database

- **Current Implementation**: FAISS (Facebook AI Similarity Search)
- **Alternative Support**: ChromaDB is included in dependencies for potential future use or custom implementations

### Text Chunking Parameters

You can adjust these parameters in the code for better performance:
- **Chunk Size**: 100 characters (default - consider increasing to 500-1000 for better context)
- **Chunk Overlap**: 100 characters (default)

**Note**: The current chunk size of 100 characters is quite small and may be suboptimal for some use cases. For better retrieval performance, consider increasing it to 500-1000 characters depending on your document structure.

##  Technologies Used

- **[Streamlit](https://streamlit.io/)**: Web application framework
- **[LangChain](https://python.langchain.com/)**: Framework for building LLM applications
- **[Google Generative AI (Gemini)](https://ai.google.dev/)**: Large language model for generation
- **[FAISS](https://github.com/facebookresearch/faiss)**: Vector similarity search library
- **[PyPDF2](https://pypdf2.readthedocs.io/)**: PDF text extraction
- **[python-dotenv](https://github.com/theskumar/python-dotenv)**: Environment variable management

##  Dependencies

```
google-generativeai
python-dotenv
langchain
PyPDF2
faiss-cpu
langchain_google_genai
chromadb
streamlit
```

##  Contributing

Contributions are welcome! Here's how you can help:

1. Fork the repository
2. Create a new branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Commit your changes (`git commit -m 'Add some amazing feature'`)
5. Push to the branch (`git push origin feature/amazing-feature`)
6. Open a Pull Request

Please ensure your code follows the existing style and includes appropriate documentation.

##  Use Cases

- **Research**: Query academic papers and research documents
- **Legal**: Search through legal documents and contracts
- **Education**: Study materials and textbooks question-answering
- **Business**: Analyze reports, policies, and documentation
- **Personal**: Organize and query personal document collections

##  Security & Privacy

- API keys are stored securely in `.env` files (not committed to version control)
- Documents are processed locally
- FAISS index is stored locally on your machine
- No data is shared with third parties except Google AI for embeddings and generation

##  Limitations

- Currently supports PDF files only
- Requires internet connection for API calls to Google Generative AI
- Answer quality depends on document content and question clarity
- Large documents may take longer to process
- Default chunk size (100 characters) may need adjustment for optimal performance with your specific documents

##  License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

##  Acknowledgments

- RAG diagram from [RAG eBook by mallahyari](https://mallahyari.github.io/rag-ebook/)
- Built with [LangChain](https://python.langchain.com/) and [Google Generative AI](https://ai.google.dev/)
- Inspired by the growing field of Retrieval Augmented Generation

##  Contact

**Aditya Tomar** - adityatomar.dev0@gmail.com

Project Link: [https://github.com/CodeX-Addy/Retrieval_Augmented_Generation](https://github.com/CodeX-Addy/Retrieval_Augmented_Generation)

---

⭐ If you find this project helpful, please consider giving it a star!


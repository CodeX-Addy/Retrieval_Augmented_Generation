# 📚 Retrieval Augmented Generation (RAG) Demo

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.0+-red.svg)](https://streamlit.io/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A powerful demonstration of **Retrieval Augmented Generation (RAG)** using Google's Gemini AI, LangChain, and FAISS vector database. This application allows you to chat with your PDF documents using natural language, making document analysis and information extraction effortless.

## 🎯 What is RAG?

Retrieval Augmented Generation (RAG) is an AI framework that combines the power of large language models with external knowledge retrieval. Instead of relying solely on the model's training data, RAG:

1. **Retrieves** relevant information from your documents
2. **Augments** the query with this context
3. **Generates** accurate, context-aware responses

This approach significantly reduces hallucinations and provides answers grounded in your specific documents.

## 🌟 Features

- **📄 Document Retrieval**: Uses FAISS (Facebook AI Similarity Search) vector database to efficiently retrieve relevant information from large sets of documents
- **🤖 AI-Powered Generation**: Leverages Google's Gemini Pro LLM to generate detailed, contextual answers
- **🔍 Semantic Search**: Employs state-of-the-art embeddings for accurate document chunk retrieval
- **📊 Multi-format Support**: Processes PDF documents of any size
- **💬 Interactive Chat**: Two interfaces available:
  - **Streamlit Web App**: User-friendly web interface for uploading and querying PDFs
  - **CLI Tool**: Command-line interface for batch processing

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    RAG Pipeline Flow                         │
└─────────────────────────────────────────────────────────────┘

1. Document Loading          2. Text Processing         3. Embedding
   ┌──────────┐                ┌──────────┐              ┌──────────┐
   │   PDF    │─────────────>  │  Split   │──────────>   │  Embed   │
   │  Files   │                │  Chunks  │              │  Vectors │
   └──────────┘                └──────────┘              └──────────┘
                                                                │
                                                                ▼
4. Query Processing          5. Retrieval               6. Vector Store
   ┌──────────┐                ┌──────────┐              ┌──────────┐
   │   User   │                │ Similar  │              │  FAISS   │
   │  Query   │──────────────> │ Chunks   │ <────────────│  Index   │
   └──────────┘                └──────────┘              └──────────┘
       │                              │
       │                              ▼
       │                       7. Context Assembly
       │                          ┌──────────┐
       └────────────────────────> │  Gemini  │
                                  │   Pro    │
                                  └──────────┘
                                       │
                                       ▼
                                  8. Response
                                  ┌──────────┐
                                  │  Answer  │
                                  └──────────┘
```

![RAG Pipeline](https://mallahyari.github.io/rag-ebook/diagrams/rag_pipeline_simplified.png)

## 📋 Prerequisites

Before you begin, ensure you have the following:

- **Python 3.8 or higher** installed on your system
- **Google AI API Key** (Gemini API access)
  - Get your free API key from [Google AI Studio](https://makersuite.google.com/app/apikey)
- **Git** for cloning the repository

## 🚀 Installation

### Step 1: Clone the Repository

```bash
git clone https://github.com/CodeX-Addy/Retrieval_Augmented_Generation.git
cd Retrieval_Augmented_Generation
```

### Step 2: Create a Virtual Environment (Recommended)

```bash
# On Windows
python -m venv venv
venv\Scripts\activate

# On macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

The following packages will be installed:
- `google-generativeai` - Google's Gemini AI SDK
- `python-dotenv` - Environment variable management
- `langchain` - LLM framework
- `langchain_google_genai` - LangChain integration for Google AI
- `PyPDF2` - PDF processing
- `faiss-cpu` - Vector similarity search
- `chromadb` - Alternative vector database (optional)
- `streamlit` - Web app framework (for app.py)

### Step 4: Configure API Key

Create a `.env` file in the project root directory:

```bash
# Create .env file
touch .env
```

Add your Google API key to the `.env` file:

```
GOOGLE_API_KEY=your_api_key_here
```

⚠️ **Important**: Never commit your `.env` file to version control. It's already included in `.gitignore`.

## 💻 Usage

This project provides two interfaces for interacting with your PDF documents:

### Option 1: Streamlit Web Application (Recommended for Beginners)

The web interface provides an intuitive way to upload and query multiple PDF documents.

**Start the application:**

```bash
streamlit run app.py
```

**How to use:**

1. **Launch**: The app will open in your default browser (usually at `http://localhost:8501`)
2. **Upload PDFs**: 
   - Click on the sidebar menu
   - Use the file uploader to select one or more PDF files
   - Click "Submit & Process" button
   - Wait for the success message
3. **Ask Questions**: 
   - Type your question in the text input field
   - Press Enter
   - The AI will provide answers based on your PDF content

**Example Questions:**
- "What is the main topic discussed in these documents?"
- "Summarize the key points from chapter 3"
- "What are the conclusions mentioned?"

### Option 2: Command-Line Interface

For batch processing or automation, use the CLI version.

**Modify the script first:**

Edit `chatbot-assistance.py` and update line 84 with your PDF file paths:

```python
pdf_documents = ["path/to/your/file1.pdf", "path/to/your/file2.pdf"]
```

**Run the script:**

```bash
python chatbot-assistance.py
```

**Workflow:**
1. The script processes all specified PDFs
2. Creates a FAISS index with document embeddings
3. Prompts you to ask a question
4. Returns an AI-generated answer based on the documents

## 📁 Project Structure

```
Retrieval_Augmented_Generation/
│
├── app.py                    # Streamlit web application
├── chatbot-assistance.py     # CLI-based chatbot
├── requirements.txt          # Project dependencies
├── .env                      # API keys (create this)
├── .gitignore               # Git ignore rules
├── LICENSE                   # MIT License
├── README.md                # This file
│
└── faiss_index/             # Generated vector database (after processing)
    ├── index.faiss          # FAISS index file
    └── index.pkl            # Metadata pickle file
```

## 🔧 How It Works

### 1. **Document Loading** 📥
```python
# PDFs are loaded and text is extracted
get_pdf_text(pdf_docs)
```
- Reads PDF files using PyPDF2
- Extracts text from all pages

### 2. **Text Chunking** ✂️
```python
# Text is split into manageable chunks
get_text_chunks(text)
```
- Uses `RecursiveCharacterTextSplitter`
- Chunk size: 100 characters with 100 character overlap
- Overlap ensures context isn't lost at boundaries

### 3. **Embedding Generation** 🧮
```python
# Creates vector embeddings using Google AI
GoogleGenerativeAIEmbeddings(model="models/embedding-001")
```
- Converts text chunks into high-dimensional vectors
- Captures semantic meaning of the text

### 4. **Vector Storage** 💾
```python
# Stores embeddings in FAISS index
FAISS.from_texts(text_chunks, embedding=embeddings)
```
- Creates a searchable index
- Enables fast similarity search

### 5. **Query Processing** 🔍
```python
# Finds relevant chunks for user query
new_db.similarity_search(user_question)
```
- Embeds the user's question
- Finds most similar document chunks

### 6. **Answer Generation** 💬
```python
# Gemini Pro generates contextual answer
ChatGoogleGenerativeAI(model="gemini-pro")
```
- Receives question + relevant context
- Generates detailed, accurate response

## 🎓 Key Concepts Explained

### What is FAISS?

**FAISS (Facebook AI Similarity Search)** is a library for efficient similarity search and clustering of dense vectors. In RAG:
- Stores document embeddings
- Performs ultra-fast nearest neighbor search
- Scales to billions of vectors
- Enables finding relevant document chunks in milliseconds

### What are Embeddings?

**Embeddings** are numerical representations of text that capture semantic meaning:
- Text → Vector (e.g., 768 dimensions)
- Similar meanings → Similar vectors
- Enables mathematical comparison of text similarity
- Google's `embedding-001` model is used in this project

### What is LangChain?

**LangChain** is a framework for building LLM applications:
- Provides abstractions for common LLM patterns
- Manages prompts and chains
- Handles document loading and splitting
- Integrates multiple AI providers

## 🔍 Troubleshooting

### Issue: `ImportError` for missing packages

**Solution:**
```bash
pip install --upgrade -r requirements.txt
```

### Issue: API Key Error

**Solution:**
- Verify your `.env` file exists in the project root
- Check the API key format: `GOOGLE_API_KEY=your_key_here`
- Ensure your API key is valid at [Google AI Studio](https://makersuite.google.com/)

### Issue: FAISS index not found

**Solution:**
- Make sure you've processed documents first (click "Submit & Process" in web app)
- Check that `faiss_index/` directory is created
- Ensure PDFs were successfully uploaded

### Issue: Streamlit not opening in browser

**Solution:**
```bash
# Manually specify the port
streamlit run app.py --server.port 8502

# Or open manually
# Navigate to http://localhost:8501
```

### Issue: Out of memory when processing large PDFs

**Solution:**
- Process PDFs one at a time
- Reduce chunk size in the code
- Use smaller PDF files for testing

## 📊 Example Use Cases

1. **Research Paper Analysis**: Upload multiple research papers and ask comparative questions
2. **Legal Document Review**: Query specific clauses, dates, or terms across contracts
3. **Study Aid**: Upload textbooks/notes and get explanations of concepts
4. **Technical Documentation**: Search through API docs, manuals, and guides
5. **Report Summarization**: Extract key insights from lengthy business reports

## 🛡️ Security & Privacy

- **API Keys**: Stored locally in `.env` file (not committed to Git)
- **Documents**: Processed locally, embeddings stored on your machine
- **API Calls**: Only queries and embeddings sent to Google AI (not full documents)
- **No Data Persistence**: FAISS index can be deleted anytime

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Google AI** for Gemini API
- **LangChain** for the RAG framework
- **Facebook Research** for FAISS
- **Streamlit** for the web framework

## 📚 Additional Resources

- [RAG Explained (Official)](https://ai.meta.com/blog/retrieval-augmented-generation-streamlining-the-creation-of-intelligent-natural-language-processing-models/)
- [LangChain Documentation](https://python.langchain.com/docs/get_started/introduction)
- [FAISS Documentation](https://faiss.ai/)
- [Google Gemini API](https://ai.google.dev/)
- [RAG eBook](https://mallahyari.github.io/rag-ebook/)

## 📧 Contact

For questions or feedback, please open an issue on GitHub.

---

**Built with ❤️ using RAG, Google Gemini, and LangChain**


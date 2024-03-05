# Chat with PDF using Gemini

This Streamlit application allows users to ask questions related to the content of uploaded PDF files. The underlying mechanism involves extracting text from PDFs, dividing it into chunks, and using Google Generative AI for question-answering.

## Dependencies

Make sure to install the required dependencies before running the application. You can install them using:

```bash
pip install streamlit PyPDF2 langchain langchain_google_genai google gensim langchain_community python-dotenv

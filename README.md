# Demonstration of Retrieval Augmented Generation

## Features

- **Document Retrieval**: Use FAISS or Chroma as vector databases to efficiently retrieve relevant information from large sets of documents.
- **Generation Model**: Use a   Large Language Model (LLM) to generate answers based on retrieved context.
- **Query Augmentation**: Enhances generated answers by supplementing queries with relevant retrieved information.
- **Multi-format Support**: Supports querying across text files, PDFs, and databases.

This Streamlit application allows users to ask questions related to the content of uploaded PDF files. The underlying mechanism involves extracting text from PDFs, dividing it into chunks, and using Google Generative AI for question-answering.



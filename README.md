# satheshkumar-p-wasserstoff-AiInternTask



This project is a dynamic pipeline that processes PDF documents, extracts meaningful summaries and domain-specific keywords, and stores the results in a MongoDB database. The system handles multiple PDFs from a folder, manages large files, and processes them efficiently.

## Table of Contents

- [Project Overview](#project-overview)
- [Approach](#approach)
- [Features](#features)
- [Installation](#installation)
- [Project Structure](#project-structure)
- [Usage](#usage)
- [MongoDB Setup](#mongodb-setup)
- [Example Output](#example-output)
- [Future Enhancements](#future-enhancements)

## Project Overview

The goal of this project is to automatically summarize large numbers of PDFs and extract relevant keywords from them in an efficient manner. Summarizing and extracting domain-specific keywords helps in gaining quick insights from a variety of documents without manually reading them. MongoDB is used to store the extracted information, ensuring easy retrieval of the results.

The project is designed with simplicity, efficiency, and scalability in mind, using Python for the text extraction and natural language processing, and MongoDB for storage.

## Approach

### 1. **PDF Ingestion & Text Extraction**
The first challenge was to read PDF files and extract their textual content. This was handled using the `PyPDF2` library, which allows for reading PDFs and extracting text page-by-page. Some PDFs may vary in complexity (textual layout, images, etc.), so the project is designed to handle basic text extraction reliably.

**Code Implementation**:
- Each PDF file in the specified folder is opened and read using `PyPDF2`.
- The text from each page is concatenated to form the full document text.
- A try-except block ensures that even if some PDFs fail (e.g., corrupted or unreadable files), the pipeline continues processing other PDFs.

### 2. **Summarization**
For summarization, the goal was to generate brief, meaningful summaries of each document. Since the task required simplicity, we opted for a basic method of taking the first two sentences from the extracted text to form the summary. More advanced methods, like machine learning models, could be integrated in the future.

**Approach**:
- The text is split into sentences using Python’s string manipulation.
- The first two sentences are concatenated to create a simple summary.

**Improvements**:
- In future versions, machine learning models (like BERT, GPT) could be employed to create more context-aware summaries.

### 3. **Keyword Extraction**
The next task was to identify the most important terms from each document. This was achieved using the **TF-IDF (Term Frequency-Inverse Document Frequency)** method from the `scikit-learn` library. TF-IDF is a common approach for determining which words are most relevant to a document while filtering out common words (e.g., "the", "is").

**Code Implementation**:
- The `TfidfVectorizer` is used to analyze the document and assign a weight to each term based on its importance.
- The top 5 terms with the highest TF-IDF scores are selected as the document’s keywords.

**Approach Rationale**:
- TF-IDF is a simple, yet effective, method for identifying key terms in documents without needing a predefined domain-specific dictionary.

### 4. **MongoDB Integration**
After extracting the text, generating summaries, and identifying keywords, the results are stored in a MongoDB database. MongoDB is a NoSQL database, which makes it suitable for storing the unstructured JSON data generated from each document.

**Implementation**:
- A MongoDB collection is created where each document is stored with its file name, summary, and keywords.
- The `pymongo` library is used to interact with MongoDB from Python.

### 5. **Error Handling**
The pipeline ensures that any issues (e.g., unreadable PDFs) are logged, but they do not crash the entire process. This was crucial to ensure the system could handle large batches of files reliably.

## Features

- **PDF Ingestion**: Automatically reads and processes all PDF files from a specified folder.
- **Text Summarization**: Extracts the first two sentences of the text to create a brief summary.
- **Keyword Extraction**: Uses TF-IDF to identify the top 5 keywords in each document.
- **MongoDB Storage**: Stores file names, summaries, and keywords in a MongoDB collection.
- **Error Handling**: Logs any errors encountered during file processing.




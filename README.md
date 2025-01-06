# NEU_QNA

An answer engine that answers to questions about master’s programs at Khoury College of Computer Science at Northeastern University

## Demo

https://drive.google.com/file/d/1iSFw-xlTEFxJzVF4mJc5yaclfw-QsYNz/view?usp=drive_link

## Setup Instructions

1. Visit [LangFlow](https://www.langflow.org/) and log in (it's free to use).

2. Import the RAG workflow:

- Navigate to the following link: [NEU QNA RAG.json](https://github.com/Zhiqian-Zhang/NEU_QNA/blob/main/rag/NEU%20QNA%20RAG.json).
- Download the JSON file to your local machine.
- In LangFlow, use the Import feature to upload the JSON file and load the workflow into your environment.

## RAG System Design

This Retrieval-Augmented Generation (RAG) system consists of two main flows: the **Load Data Flow** and the **Retriever Flow**. This system is designed to efficiently process and retrieve relevant information to generate accurate responses.

---

## Load Data Flow

1. **Input**

   - Upload a text file containing Northeastern University (NEU) frequently asked questions.

2. **Text Processing**

   - The text is split into smaller, manageable chunks for processing.

3. **Embedding Generation**

   - Each chunk is converted into a high-dimensional vector representation using OpenAI's `text-embedding-ada-002` model.

4. **Storage in Database**
   - These embeddings, along with their corresponding text, are stored in **Astra DB**, a serverless and scalable vector database, enabling efficient similarity searches.

---

## Retriever Flow

1. **Query Embedding**

   - When a user inputs a question, it is converted into a vector using the same `text-embedding-ada-002` model.

2. **Vector Search**

   - This query vector is compared against the embeddings stored in Astra DB to retrieve the most relevant vectors (and their associated text).

3. **Context Construction**

   - The retrieved text chunks are used to construct a context for answering the user’s question.

4. **Prompt Creation**

   - A prompt is generated by combining the retrieved context with the user’s question.

5. **Response Generation**
   - The prompt is passed to OpenAI’s language model to generate a detailed, accurate response.

---

## Technologies Used

- **OpenAI's text-embedding-ada-002**: For embedding generation.
- **Astra DB**: A serverless vector database for storing and searching embeddings.
- **OpenAI Language Model**: For generating responses based on the retrieved context.

---

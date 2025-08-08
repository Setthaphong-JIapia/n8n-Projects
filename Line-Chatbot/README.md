🧾 README Explanation (for GitHub)
## Overview
This project is a document ingestion and question-answering system built using:

Google Drive (for document storage),

Google Gemini (for both text embedding and chat model),

Pinecone (for vector storage and retrieval),

and an AI Agent that handles user queries using RAG (Retrieval-Augmented Generation).

The system is split into two main flows:

## 1. Document Upload & Embedding Workflow
This flow watches a Google Drive folder. When a new file is added, it processes and stores its embeddings for later semantic search.

Steps:

Trigger:

Starts manually (Execute Workflow) or automatically when a file is uploaded to a specific Google Drive folder (Google Drive Trigger).

File Fetching:

The uploaded file is retrieved from the Drive.

Embedding:

The file’s content is passed to Google Gemini Embeddings API, which transforms the text into vector embeddings.

Storage:

These embeddings are stored in Pinecone Vector Store for later retrieval during user queries.

## 2. Question Answering Workflow (RAG)
This flow handles incoming user questions and responds using a combination of memory, vector search, and Gemini’s language model.

Steps:

Webhook Trigger:

A user question is received through a Webhook (via POST request).

Field Editing:

The input fields can be modified if needed (e.g., formatting, structuring).

AI Agent:

The question is sent to an AI Agent, which:

Uses Pinecone to fetch relevant content embeddings.

Uses Simple Memory to track previous conversation history.

Uses Google Gemini Chat Model to generate a final answer using both memory and retrieved context.

Response:

The AI Agent sends the final answer via an HTTP request back to the system or client.

## Technologies Used
Component	Description
Google Drive	File source and monitoring
Google Gemini	Used for both embeddings and chat response
Pinecone	Vector store for semantic retrieval
Webhook & HTTP	Interface for accepting questions and sending replies
Simple Memory	Maintains chat history for contextual answers
AI Agent (RAG)	Combines retrieval + generation for better answers

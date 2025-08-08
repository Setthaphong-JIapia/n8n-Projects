## Workflow Diagram

```mermaid
flowchart TD
    A[Execute Workflow] --> B[Search Folder in Google Drive]
    B --> C[Get Uploaded File from Google Drive]
    C --> D[Generate Embeddings with Google Gemini]
    D --> E[Store Embeddings in Pinecone Vector Store]

    %% Real-time file monitoring
    F[Google Drive Trigger: fileCreated] --> C

    %% Question answering flow
    G[Webhook (POST)] --> H[Edit Fields]
    H --> I[AI Agent]

    I --> J[Google Gemini Chat Model]
    I --> K[Simple Memory]
    I --> L[Answer Questions with Vector Store]
    L --> M[Pinecone Vector Store]
    L --> N[Google Gemini Chat Model]
    I --> O[Send Response via HTTP Request]

    %% Embedding node reused
    subgraph Embedding
        D
    end
```

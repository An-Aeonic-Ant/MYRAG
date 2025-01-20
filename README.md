# Retrieval-Augmented Generation (RAG) for Personalized Title Generation

This repository contains the implementation of a RAG model designed to generate personalized titles based on user-entered descriptions and their past preferences. The project combines retrieval systems and generative AI to deliver user-specific outputs.

## How It Works

The system retrieves relevant instances based on a user's history and uses a Gemma pipeline to generate new titles aligned with the user's style and preferences. The point is that the titles stored previously, whether model generated or edited by the user, will always be as per the user's preference. Hence, they can be used as soft prompts to guide the model into generating titles of similar flavor


### 1. **Input**
The user provides a description of an item or task.

### 2. **Retrieval**
- Generate embeddings of the input description.
- Find the `k` most similar documents based on the cosine similarity of their embeddings.

### 3. **Generation**
- Pass the retrieved documents and their title in the form of examples to the title generation model as soft prompts.
- Default examples are used if no similar documents are present in the database.
- If a document in the database is highly similar to the input description, its title is returned directly.

### 4. **Output**
Returns a personalized title that adheres to the specified length constraint and matches the user's preferences.

## Technical Details

The implementation makes use of state-of-the-art models and libraries:

- **Pipeline:** Hugging Face Transformers
- **Title Generation Model:** `google/gemma-2-2b-it`
- **Embedding Model:** `all-MiniLM-L6-v2`
- **Similarity Metric:** Cosine similarity

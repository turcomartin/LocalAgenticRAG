Stori’s Generative AI Challenge

Welcome to the Challenge!
Hey there! We're thrilled you're interested in joining our Generative AI (GenAI) team at Stori. We
have an exciting task for you that will help us solve some real-world questions using the power
of Retrieval-Augmented Generation (RAG). Let's get started!

## Basic RAG Implementation
**Objective**: Implement a RAG application that retrieves relevant documents from a static dataset
and generates a response based on those documents.

**Task Description:** We need to answer some questions using a collection of documents. You'll
build a RAG application to achieve this. Here are the steps:
1. **Data Preparation and Basic Retrieval (0.5 hours)**
- Start with a small dataset of text documents (this will be provided).

**<span style="color:red">This wasn't provided</span>**

**<span style="color:orange">The files should range a wide variety of formats. At least a DOC with tables, etc. Forcing the candidate to think about using an alternative DOC parser (LlamaParse, TextTract,etc) </span>**

- Index the documents using TF-IDF or BM25 (sparse retrieval).
- Implement a basic function that takes a query and returns the top-k relevant documents from
the dataset using cosine similarity.
2. **Generation Mechanism (0.5 hours)**
- Use a pre-trained language model (e.g., OpenAI models) to generate responses based on
the retrieved documents.

**<span style="color:blue"> Going to use Llama 3.1 (8B) models via Ollama </span>**
- Combine the retrieved documents into a single input for the language model.
3. **Enhanced Retrieval (0.5 hours)**
- Upgrade the retrieval method to a more advanced technique, such as dense retrieval using
BERT embeddings or similar.
**<span style="color:blue"> Going to use nomic-embed-text, better than ada-002 and local</span>**
- Implement a more efficient indexing method suitable for larger datasets, like FAISS, Chroma,
or Qdrant.
4. **Evaluation (1 hour)**
- Create a set of test queries and expected responses.

**<span style="color:blue"> Going to create some organic examples and synthetic data</span>**
- Evaluate the system's ability to retrieve relevant documents and generate coherent
responses.

**<span style="color:blue">Evaluate both retriever performance and answer performance</span>**

**What to Submit:**
- Source code for the retrieval and generation mechanisms. You don’t need to build from
scratch; you can use Scipy, NLTK, LlamaIndex, or LangChain.
- Evaluation results and analysis, comparing the results of both retrievers.

**<span style="color:blue">Semantic and Lexical search, will probably use ElasticSearch 😁. No, we will go with a fully local approach</span>**

## Contextual Generation and Dialogue State

**<span style="color:blue">Streamlit app</span>**

Management
**Objective:** Enhance the RAG application to handle multi-turn conversations and maintain
context.
**Task Description:** We need our RAG system to be more powerful by integrating multi-turn
conversations. Here are the steps:

**1. Contextual Generation (1.5 hours)**
- Improve the generation mechanism to better utilize the context from retrieved documents.
Consider a re-ranking approach or a Self-RAG approach.

**<span style="color:blue">Agentic Rag</span>**

**2. Conversation History (0.5 hours)**
- Implement a dialogue state management system to track conversation history.

**<span style="color:blue">Gotta take into account past interaction to </span>**

**3. Advanced Evaluation (1 hour)**
- Design a comprehensive evaluation framework with automated metrics (e.g., Faithfulness,
Relevance, Correctness) and human evaluation.
- Conduct testing to assess the system's performance in real-world scenarios (try to come up
with some questions a customer would likely ask).
**What to Submit:**
- Source code for contextual generation and dialogue state management.
- Comprehensive evaluation report, including automated metrics, human evaluation, and
performance analysis.

We hope you enjoy tackling these challenges and showcasing your skills. We can't wait to see
your innovative solutions and welcome you to our team at Stori. Good luck!


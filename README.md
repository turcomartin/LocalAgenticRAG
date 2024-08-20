# Intro
The following collection of notebooks show how to create your own Graph Based RAG agent. The great thing about using a graph approach is that it allows you to customize the behaviour of your AI agent and don't depend on the obscure details of a wrapper. Giving you, almost 100% of the control. A 100% framework free version is possible but it will take significant time to re-design some pieces from scratch.

This entire project was done using local LLM in a Macbook Air M2.
The latest version of Llama 3.1 was used and the novel **json mode** made some parts of the process much easier.

Also the model **Mistral Instruct** in its 7B version was used to aid in the question/answer generation dataset for the evaluation dataset.


# Notebooks
There are 6 notebooks in the __notebooks__ folder.

### 1 - Database Construction

The first notebooks shows how to create 4 differente databases with different indexing methods each.

- BDM25
- TF-IDF
- Chroma
- FAISS


The first step was to parse and chunk the document. For that I used the **RecursiveCharacterSplitter** to generate chunks of even size and allow some overlapping. 

These chunks were vectorized using a locally hosted embeddings model called **nomic-embed-text**. Benchmarks indicate that it surpasses
the OpenAI models **text-embedding-ada-002** and **text-embedding-3-small**. They also have a smaller dense representation being almost half the size.

### 2 - Simple Querying
Once the different vectorstores were created and saved. I went ahead and try them out of the box. In order to get some baseline measurements and a feeling for their performance.

The documents were fed alongside its page number, it's nice to query the database and get a response with references on it so we can look them up later. Like in the example.

```
This extract is from page 2

Once the different vectorstores were created and saved. I went ahead and try them out of the box. In order to get some baseline measurements and a feeling for their performance.

This extract is from page 4

The documents were fed alongside its page number, it's nice to query the database and get a response with references on it so we can look them up later.

```
### 3 - Creating the evalution dataset
In this stage I used Mistral Instruct to generate question and answers pairs from randomly drawn chunks of text. The quality of the questions formulated was superb.

I recommend looking at the prompt to learn how they were constructed.


### 4 - Evaluation
In notebook number 4 I execute the questions on the evaluation dataset to get the answers out of the Basic Agents created in the notebook number 2. All of them were executed under same temperature 0 conditions and with the same model.


### 5 - Agentic RAG
Below there is a desing made by me a complete Agentic RAG implementation using **LangGraph**, a graph based agent design tool made by **LangChain**. It allows to use to define nodes, conditional edges and pipeline nodes. 

A routing step was included at the beginning of the graph because not all questions require a retrieval step. 
In the case that retrieval is needed a Hybrid retrieve involving FAISS and TF-IDF vectorstores was put in place. 

![alt text](image-1.png)

Some pieces to furhter develop are areas such as Guardrails, HyDE and self-reflection that were not implemetented in this version.

Here is the **LangGraph** representation of it
![alt text](rag-graph.jpeg)

The memory was treated a separate object, not using **LangGraph** native mechanism because it is still buggy. I opted out for using a traditional approach and just storing the messages one by one in a separate array. These would have to be stored in an external database anyway as the entire agent is actually stateless. 

Re-Ranking was put in place to filter out those chunks that were retrieved but not relevant to the user's query. 

One of the biggest drawbacks of using a local LLM is that, depending on your computing power, inference can take a significant amount of time. In my case a single run of the agent took about 20 senconds. That might be fine in a personal use case, just running a thing on your laptop. For a user based product I would a more powerful alternative cloud based alternative. 

At the end of the notebook I run the evaluation test again and get ready to make some measurements in the following and final notebook.

### 6 -  Metrics

Some 4 famous metrics have been by the evaluation framework RAGAS.
![alt text](image-2.png)

However one must be careful at the time of using any evaluation framework because we must measure in order to optimize a certain metric. 

There are some other tools like

https://github.com/Marker-Inc-Korea/AutoRAG

That take measurements of the RAG performance in order to propose different RAG architectures that will fit better the training data (q/a pairs made beforehand)

I found almost impossible to run the entire RAGAS pipeline on a local LLM. I had restrain myself to just measure **answer similarity**, which, in all cases resulted in a score of about 0.9 without significant changes between the different methods. 

Does that mean that the agent based method is not better? No, because the evaluation dataset was directed towards topic specific questions and not a conversation. A different evaluation approach should be taken for those casee.


# Final Remarks
Locally hosted LLMs are just going to get better. NVIDIA just released a version of Llama 3.1 half the original size. Tools to construct this agents are still in their early stages and change very quickly, thus, unrealiable for their use in industry. 

Thank you for making it this far and I hope you learnt something along the way. Certainly I did 😄
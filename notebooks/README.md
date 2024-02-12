# notebooks
### 1. Jan 22, 2024. [gte-large_LangChain_ChromaDB_Llama2-7B.ipynb](notebooks/gte-large_LangChain_ChromaDB_Llama2-7B.ipynb).

Architecture:
* [RecursiveCharacterTextSplitter](https://api.python.langchain.com/en/latest/text_splitter/langchain.text_splitter.RecursiveCharacterTextSplitter.html#),
* ["thenlper/gte-large" embedding model](https://huggingface.co/thenlper/gte-large) with 512 tokens length limitation,
* [ChromaDB](https://python.langchain.com/docs/integrations/vectorstores/chroma) as a vector store,
* [RetrievalQA](https://api.python.langchain.com/en/latest/chains/langchain.chains.retrieval_qa.base.RetrievalQA.html) with k=8 documents,
* [TheBloke/Llama-2-7b-Chat-GPTQ](https://huggingface.co/TheBloke/Llama-2-7B-Chat-GPTQ) as LLM


### 2. Jan 29, 2024. [gte-large_LangChain_ChromaDB_Llama2-7B_ver2.ipynb](gte_large_LangChain_ChromaDB_Llama2_7B_ver2.ipynb).

Architecture:
* [RecursiveCharacterTextSplitter](https://api.python.langchain.com/en/latest/text_splitter/langchain.text_splitter.RecursiveCharacterTextSplitter.html#) with chunk size 256,
* ["thenlper/gte-large" embedding model](https://huggingface.co/thenlper/gte-large) with 512 tokens length limitation,
* [ChromaDB](https://python.langchain.com/docs/integrations/vectorstores/chroma) as a vector store,
* [RetrievalQA](https://api.python.langchain.com/en/latest/chains/langchain.chains.retrieval_qa.base.RetrievalQA.html) with k=10 documents,
* [TheBloke/Llama-2-7b-Chat-GPTQ](https://huggingface.co/TheBloke/Llama-2-7B-Chat-GPTQ) as LLM
* Additional changes:
  - There are 3 documents in the vector database and the search is performed among them
  - RetrievalQA gives 10 documents (instead of 8) as a LLM context
  - 'result' dictionary was added after each query for retrieved documents viewing
  - for retrieval "similarity_score_threshold" search type was used ith the 0.5 threshold


### 3. Feb 13, 2024. [RAG_ParentDocumentRetriever.ipynb](RAG_ParentDocumentRetriever.ipynb).

Architecture:
* [ParentDocumentRetriever](https://python.langchain.com/docs/modules/data_connection/retrievers/parent_document_retriever) with parent chunk size 2000 and child 256 (RecursiveCharacterTextSplitter),
* ["BAAI/bge-small-en-v1.5" embedding model](https://huggingface.co/BAAI/bge-small-en-v1.5) with 512 tokens length limitation and 384 dimensions vectors.
* [ChromaDB](https://python.langchain.com/docs/integrations/vectorstores/chroma) as a vector store,
* [RetrievalQA](https://api.python.langchain.com/en/latest/chains/langchain.chains.retrieval_qa.base.RetrievalQA.html) with k=10 documents,
* [TheBloke/Llama-2-7b-Chat-GPTQ](https://huggingface.co/TheBloke/Llama-2-7B-Chat-GPTQ) as LLM
* Additional changes:
  - There are 3 documents in the vector database and the search is performed among them
  - New 36 questions
  - All questions are asked, the result answers and context documents are in the resulted table
  - Access to LangChain Smith to track the project

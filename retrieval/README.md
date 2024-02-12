LangChain's **RetrievalQA** chain has 4 different strategies, which can be used to retrieve documents:
* ***Stuff***. Takes multiple small documents and combines them into a single prompt for the LLM. It is cost-efficient because it involves only one request to the LLM. The chain type stuff is the simplest method. It uses all related text from the documents as the context in the prompt to the LLM. **Pros**: You only make a single call to the LLM. And when it generates text, it has access to all the data simultaneously. It’s cost-efficient since you only make one call to the LLM. **Cons**: This can sometimes exceed the token limit for a LLM.

Example:
```python
template = "Answer the following question based on the retrieved documents: {question}\n\n{summaries}"
prompt_template = PromptTemplate(template=template, input_variables=["question", "summaries"])

qa_chain = load_qa_chain(OpenAI(), chain_type="stuff", prompt_template=prompt_template, document_variable_name="summaries")
qa = RetrievalQA.from_chain_type(llm=OpenAI(), chain_type="stuff", retriever=docsearch.as_retriever(), chain_type_kwargs={"prompt": prompt_template, "document_variable_name": "summaries"})
```


  
* ***Refine***. Looks at each document individually and updates its answer with each new document. It is useful when there are too many documents, but it can be slow and confusing if they reference each other. Refine also separates texts into batches, but it feeds the first batch to LLM, the answer, and the second to LLM. It refines the answer by going through all the batches.

Example:
```python
refine_template = "You asked: {question}\nWe answered: {existing_answer}\nWe found some more information that might be relevant:\n{context_str}\nCan you improve the answer based on this information? If not, just repeat the original answer."
refine_prompt_template = PromptTemplate(template=refine_template, input_variables=["question", "existing_answer", "context_str"])

qa_chain = load_qa_chain(llm=llm, chain_type="refine", refine_prompt=refine_prompt_template)
qa = RetrievalQA.from_chain_type(llm=OpenAI(), chain_type="refine", retriever=docsearch.as_retriever(), chain_type_kwargs={"refine_prompt": refine_prompt_template})
```


  
* ***Map reduce***. Consists of a map step, where each document is individually summarized, and a reduce step where these mini-summaries are combined. An optional compression step can be added. This method runs an initial prompt on each chunk of data and then uses a different prompt to combine all the initial outputs. Map_reduce separates texts into batches, where you can define the batch size. It feeds each batch with the question to LLM separately and comes up with the final answer based on the answers from each batch. **Pros**: It can scale to more documents and documents of larger length. Since the calls to the LLM are on independent, individual documents they can be parallelized. **Cons**: This requires more calls to the LLM. You can also get some information during the final combined call.

Example:
```python
# Create a custom map prompt template that asks the language model to extract the main idea of each document
map_template = "Write the main idea of the following document in one sentence:\n\n{text}"
map_prompt_template = PromptTemplate(template=map_template, input_variables=["text"])

# Create a custom combine prompt template that asks the language model to use the main ideas to answer the question
combine_template = "Use the main ideas of the retrieved documents to answer the question: {question}\n\n{texts}"
combine_prompt_template = PromptTemplate(template=combine_template, input_variables=["question", "texts"])

# Pass the custom prompt templates to the load_qa_chain function or the from_chain_type method
qa_chain = load_qa_chain(llm=llm, chain_type="map_reduce", map_prompt=map_prompt_template, combine_prompt=combine_prompt_template)
qa = RetrievalQA.from_chain_type(llm=OpenAI(), chain_type="map_reduce", retriever=docsearch.as_retriever(), chain_type_kwargs={"map_prompt": map_prompt_template, "combine_prompt": combine_prompt_template})
```



* ***Re-rank***. Tries to get an answer for each document and assigns it a confidence score, picking the highest confidence answer in the end. Rerank separates texts into batches, feeds each batch to LLM, returns a score of how fully it answers the question, and comes up with the final answer based on the high-scored answers from each batch.

Example:
```python
# Create a custom map prompt template that asks the language model to write a summary of each document
map_template = "Write a summary of the following document in one sentence:\n\n{text}"
map_prompt_template = PromptTemplate(template=map_template, input_variables=["text"])

# Create a custom score prompt template that asks the language model to rate the relevance of each summary to the question on a scale of 1 to 5
score_template = "Rate the relevance of this summary to the question {question} on a scale of 1 to 5:\n\n{text}"
score_prompt_template = PromptTemplate(template=score_template, input_variables=["question", "text"])

# Pass the custom prompt templates to the load_qa_chain function or the from_chain_type method
qa_chain = load_qa_chain(llm=llm, chain_type="map_rerank", map_prompt=map_prompt_template, score_prompt=score_prompt_template)
qa = RetrievalQA.from_chain_type(llm=OpenAI(), chain_type="map_rerank", retriever=docsearch.as_retriever(), chain_type_kwargs={"map_prompt": map_prompt_template, "score_prompt": score_prompt_template})
```


Source: https://www.comet.com/site/blog/evaluating-rag-pipelines-with-ragas/, https://github.com/langchain-ai/langchain/issues/7347

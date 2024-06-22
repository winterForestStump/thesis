# Evaluation

RAGs have become the standard architecture for providing LLMs with context in order to avoid hallucinations. However even RAGs can suffer from hallucination, as is often the case when the retrieval fails to retrieve sufficient context or even retrieves irrelevant context that is then weaved into the LLM’s response. Just like in any machine learning system, the performance of individual components within the LLM and RAG pipeline has a significant impact on the overall experience.

### Retrieval part of the pipeline:

*Context relevancy* gauges the relevancy of the retrieved context, calculated based on both the question and contexts. The values are binary 0 or 1, where 0 - the context is not relevant to the question, 1 - relevant. Ideally, the retrieved context should exclusively contain essential information to address the provided query.

### Generation part of the pipeline:

*Faithfilness* measures the factual consistency of the generated answer against the given context. It is calculated from answer and retrieved context. The answer is binary 0 or 1 range. Higher the better. The generated answer is regarded as faithful if all the claims that are made in the answer can be inferred from the given context.

*Answer relevancy* focuses on assessing how pertinent the generated answer is to the given prompt. 


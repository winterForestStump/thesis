# Evaluation



RAGs have become the standard architecture for providing LLMs with context in order to avoid hallucinations. However even RAGs can suffer from hallucination, as is often the case when the retrieval fails to retrieve sufficient context or even retrieves irrelevant context that is then weaved into the LLM’s response. Just like in any machine learning system, the performance of individual components within the LLM and RAG pipeline has a significant impact on the overall experience. [Ragas](https://github.com/explodinggradients/ragas) offers metrics tailored for evaluating each component of your RAG pipeline in isolation.

### Retrieval part of the pipeline:

*Context precision* evaluates whether all of the ground-truth relevant items present in the contexts are ranked higher or not. Ideally all the relevant chunks must appear at the top ranks. This metric is computed using the question and the contexts, with values ranging between 0 and 1, where higher scores indicate better precision.

*Context recall* measures the extent to which the retrieved context aligns with the annotated answer, treated as the ground truth. It is computed based on the ground truth and the retrieved context, and the values range between 0 and 1, with higher values indicating better performance. To estimate context recall from the ground truth answer, each sentence in the ground truth answer is analyzed to determine whether it can be attributed to the retrieved context or not. In an ideal scenario, all sentences in the ground truth answer should be attributable to the retrieved context.

*Context relevancy* gauges the relevancy of the retrieved context, calculated based on both the question and contexts. The values fall within the range of (0, 1), with higher values indicating better relevancy. Ideally, the retrieved context should exclusively contain essential information to address the provided query.

### Generation part of the pipeline:

*Faithfilness* measures the factual consistency of the generated answer against the given context. It is calculated from answer and retrieved context. The answer is scaled to (0,1) range. Higher the better. The generated answer is regarded as faithful if all the claims that are made in the answer can be inferred from the given context.

*Answer relevancy* focuses on assessing how pertinent the generated answer is to the given prompt. A lower score is assigned to answers that are incomplete or contain redundant information. This metric is computed using the question and the answer, with values ranging between 0 and 1, where higher scores indicate better relevancy. An answer is deemed relevant when it directly and appropriately addresses the original question. Importantly, Ragas assessment of answer relevance does not consider factuality but instead penalizes cases where the answer lacks completeness or contains redundant details.


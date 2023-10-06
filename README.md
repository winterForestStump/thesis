# thesis
Enhancing Financial Analysis with Question-Answering Models (for $0). The idea is:
* use open-sourse LLM: BERT (distilbert-base-uncased)
* use 10k SEC filings as text corpus -> out of 184K filings randomly pick 50-100
* creating a dataset with context, questions and answers
* train and test the model: exaact match and F1 score metrics (SQuAD v2 benchmark)
* test the model
* optinal: create an app for QA


## plan
1. Introduction:
  ""The research problem addressed in this thesis is to investigate the practical implementation and efficacy of question-answering models in enhancing traditional financial analysis methods. Specifically, this study aims to explore how advanced natural language processing techniques, including question-answering models, can be leveraged to extract meaningful insights, sentiment, and critical information from textual data within financial documents such as annual reports (10-K filings) to empower investors, analysts, and financial professionals in making more informed decisions and assessments.""

2. Literature Review:
* Review existing literature on financial analysis, natural language processing (NLP), and question-answering models.

3. Data Collection and Preprocessing:
* Describe the process of dataset collection of 10-K filings and QA dataset creation (question, context, answer).
* Randomly chosen 100 filings

4. Question-Answering Model Selection:
* Choose an open-source question-answering model: BERT / Llama 2 / others

5. Model Training:
* Describe fine-tuning process
* Modifications or adaptations made to the model architecture or training process to fit the financial analysis context.

6. Experimental Setup:
* Specify evaluation metrics: Exact match and F1 score.

7. Results and Analysis:
* Present the results, showing how the question-answering model performed
* Visualizations
* Analyze the strengths, weaknesses and challenges of the model

8. Applications and Use Cases:
* Practical applications of QA model in enhancing financial analysis.
* Real-world scenarios or use cases for investors, analysts, or financial (un)professionals

9. Conclusion and Future Work:
* Summarization of findings and the contributions. Future research or improvements to QA models for financial analysis.


## literature
* FinGPT: Open-Source Financial Large Language Models: https://arxiv.org/pdf/2306.06031.pdf
* FinGPT repository: https://github.com/AI4Finance-Foundation/FinGPT
* FinNLP repository: https://github.com/AI4Finance-Foundation/FinNLP
* Financial News Analytics Using Fine-Tuned Llama 2 GPT Model: https://arxiv.org/pdf/2308.13032.pdf
* Llama 2 Responsible Use Guide: https://ai.meta.com/static-resource/responsible-use-guide/
* BloombergGPT: A Large Language Model for Finance: https://arxiv.org/pdf/2303.17564.pdf
* The MosaicML MPT-7B: https://www.mosaicml.com/blog/mpt-7b
* finnhub-python: https://github.com/Finnhub-Stock-API/finnhub-python
* FlashAttention: https://github.com/Dao-AILab/flash-attention
* Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks: https://arxiv.org/pdf/2005.11401.pdf
* Composer. A PyTorch Library for Efficient Neural Network Training: https://github.com/mosaicml/composer
* GLM-130B: An Open Bilingual Pre-Trained Model: http://keg.cs.tsinghua.edu.cn/glm-130b/posts/glm-130b/
* BloombergGPT aims to be a domain-specific AI for business news: [news article](https://www.niemanlab.org/2023/04/what-if-chatgpt-was-trained-on-decades-of-financial-news-and-data-bloomberggpt-aims-to-be-a-domain-specific-ai-for-business-news/)
* BloombergGPT: The first Large Language Model for Finance: [Medium articlle](https://medium.com/codex/bloomberggpt-the-first-large-language-model-for-finance-61cc92075075)
* pythonontheplane123/LLM_course_part_1: https://github.com/pythonontheplane123/LLM_course_part_1
* HuggingFaceDatasetLoader: https://github.com/langchain-ai/langchain/blob/master/libs/langchain/langchain/document_loaders/hugging_face_dataset.py
* Self-Instruct: Aligning LM with Self Generated Instructions: https://github.com/yizhongw/self-instruct
* Alpaca: A Strong, Replicable Instruction-Following Model: https://crfm.stanford.edu/2023/03/13/alpaca.html
* An intro to ROUGE, and how to use it to evaluate summaries: https://www.freecodecamp.org/news/what-is-rouge-and-how-it-works-for-evaluation-of-summaries-e059fb8ac840/#:~:text=For%20example%2C%20ROUGE%2D1%20refers,2%20precision%20and%20recall%20scores
* https://fullstackdeeplearning.com/llm-bootcamp/spring-2023/augmented-language-models/
* https://medium.com/@onkarmishra/using-langchain-for-question-answering-on-own-data-3af0a82789ed

## dataset
[data]

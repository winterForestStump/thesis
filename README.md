# thesis
Conducting sentiment analysis and risk assessment in 10-K filings using pre-trained language models (LLMs) fr $0

## plan
1. Data Collection and Preprocessing:
* Gather a diverse dataset of 10-K filings from various companies and industries from the SEC's EDGAR database.
* Preprocess the text data: cleaning, tokenizing, and handling issues like punctuation, stop words, and special characters (\n, \t, \xa0).

2. Selecting a Pre-trained LLM:
* Choose a suitable open-source pre-trained language model: BERT, Llama 2, MPT-7B. 

3. Sentiment Analysis:
* Annotate a subset of your 10-K filings for sentiment analysis, categorizing sections or sentences as positive, negative, or neutral - this will serve as training data.
* Fine-tune the LLM on this annotated dataset for sentiment analysis.
* Evaluate the model's performance using standard metrics like accuracy, precision, recall, F1-score, and possibly domain-specific metrics relevant to sentiment analysis in financial documents.

4. Risk Assessment:
* Define risk categories or levels that you want to assess within 10-K filings. For example, you might categorize risks as financial, operational, legal, etc.
* Annotate a subset of your dataset with risk-related sections or sentences and categorize them into the predefined risk categories.
* Fine-tune the LLM on this annotated dataset for risk assessment.
* Evaluate the model's ability to accurately categorize sections of 10-K filings into risk categories. Use relevant evaluation metrics, and consider performing a qualitative analysis to understand any false positives or negatives.

5. Interpretability and Visualization:
* Develop a system to visualize the results of sentiment analysis and risk assessment. You can use techniques like word clouds, topic modeling, or heatmaps to highlight key findings within the 10-K filings.

6. User-Friendly Interface:
* Create a user-friendly interface (Streamlit?) that allows investors or users to input 10-K filings and receive sentiment and risk assessments in a user-readable format.

7. Evaluation and Testing:
* Conduct thorough evaluation and testing of system using a test dataset or through a user study.
* Collect feedback to improve the model's performance and usability.

8. Documentation and Reporting:
* Document methodology, experiments, results, and any challenges encountered during the research process.

9. Ethical Considerations:
* Is there possible bias in the data or the model? How it can be addressed?

10. Future Work:
* Suggest areas for future research or improvements to your model and system.


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

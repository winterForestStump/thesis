# thesis
Enhancing Financial Analysis with Question-Answering Models for $0


# plan
1. Introduction:
* the field of financial analysis and the importance of textual data in financial documents like annual reports (10-K filings).
* the research problem 'How can question-answering models be used to enhance financial analysis?', provide an overview of your approach and mention the significance of your research:

  ""The research problem addressed in this thesis is to investigate the practical implementation and efficacy of question-answering models in enhancing traditional financial analysis methods. Specifically, this study aims to explore how advanced natural language processing techniques, including question-answering models, can be leveraged to extract meaningful insights, sentiment, and critical information from textual data within financial documents such as annual reports (10-K filings) to empower investors, analysts, and financial professionals in making more informed decisions and assessments.""

2. Literature Review:
* Review existing literature on financial analysis, natural language processing (NLP), and question-answering models.
* Highlight relevant studies on sentiment analysis, risk assessment, and financial metrics extraction from textual data.
* Identify gaps in the literature that your research aims to address.

3. Data Collection and Preprocessing:
* Describe the process of dataset collection of 10-K filings. Mention any preprocessing steps applied.

4. Question-Answering Model Selection:
* Choose an open-source question-answering model: Llama 2, GPT-3, MPT-7B.
* Explain why you chose the model (strengths and potential limitations).

5. Model Training:
* Describe fine-tuning process
* Explain any modifications or adaptations made to the model architecture or training process to fit the financial analysis context.

6. Experimental Setup:
* Detail the experimental setup (dividing the dataset into training, validation, and test sets)
* Specify evaluation metrics relevant to financial analysis (accuracy, precision, recall, F1-score, or domain-specific metrics).

7. Results and Analysis:
* Present the results, showing how the question-answering model performed in various financial analysis tasks.
* Visualizations and examples to illustrate the model's performance.
* Analyze the strengths and weaknesses of the model, discussing any challenges encountered.

8. Applications and Use Cases:
* Practical applications of your question-answering model in enhancing financial analysis.
* Real-world scenarios or use cases where the model can be valuable for investors, analysts, or financial professionals.

9. Comparison with Existing Methods:
* Compare the performance of the model with existing methods or benchmarks in financial analysis.
* Highlight the advantages of the approach, if any.

10. Interpretability and Visualization:
* Explain how the model's outputs interpretable and user-friendly for financial analysts.
* Visualizations or dashboards that convey financial insights.

11. Ethical Considerations:
* Ethical considerations related to the use of AI in financial analysis, such as bias, fairness, and transparency.

12. Conclusion and Future Work:
* Summarization of findings and the contributions of your research.
* Avenues for future research or improvements to question-answering models for financial analysis.

13. References:
* Citation of all the sources and references used in the thesis.


# literature
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


#dataset
[winterForestStump/10-K_sec_filings](https://huggingface.co/datasets/winterForestStump/10-K_sec_filings)

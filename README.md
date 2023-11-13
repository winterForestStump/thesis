# thesis
* What is the goal? - To enhance financial analysis of public companies filings with with $0 costs. 
* Decide on the evaluation criteria -
* Choose a model - open-source LLaMA 2
* Develop the right data mix - use 10K SEC filings
* Efficient fine-tuning or RAG


### plan of the paper
1. Introduction: ""The research problem addressed in this thesis is to investigate the practical implementation and efficacy of question-answering models in enhancing traditional financial analysis methods. Specifically, this study aims to explore how advanced natural language processing techniques, including question-answering models, can be leveraged to extract meaningful insights, sentiment, and critical information from textual data within financial documents such as annual reports (10-K filings) to empower investors, analysts, and financial professionals in making more informed decisions and assessments.""

2. Literature Review (natural language processing (NLP) and question-answering models) 

3. Data Collection and Preprocessing (the process of dataset collection and QA dataset creation of 10-K filings; select randomly 100 filings to create question, context, answerdictionaries)

4. Question-Answering Model Selection (open-source question-answering model: BERT / Llama 2 / others)

5. Model Training. (fine-tuning process, modifications or adaptations made to the model architecture or training process to fit the financial analysis context)

6. Evaluation metrics: Exact match. Create a set of questions (prompts) and answers for them, retrieved from the documents. Calculate the exact match between the model resultsa and true values

7. Results and Analysis (present the results, visualizations, strengths/weaknesses/challenges of the model)

8. Applications and Use Cases (practical applications of QA model/ real-world scenarios or use cases for investors, analysts, or financial (un)professionals)

9. Conclusion and Future Work (summarization of findings and the contributions/ future research or improvements to QA models for financial analysis)


### literature
* Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks: [paper](https://arxiv.org/pdf/2005.11401.pdf)
* [A Survey of Large Language Models](https://arxiv.org/abs/2303.18223)
* [Holistic Evaluation of Language Models](https://arxiv.org/abs/2211.09110)
* [LoRA: Low-Rank Adaptation of Large Language Models](https://arxiv.org/abs/2106.09685)
* [QLoRA: Efficient Finetuning of Quantized LLMs](https://arxiv.org/abs/2305.14314)
* FinGPT model: [GitHub repository](https://github.com/AI4Finance-Foundation/FinGPT), [fine-tuning](https://byfintech.medium.com/beginners-guide-to-fingpt-training-with-lora-chatglm2-6b-9eb5ace7fe99)
* BloombergGPT. The first Large Language Model for Finance: [paper](https://arxiv.org/pdf/2303.17564.pdf), [Medium articlle](https://medium.com/codex/bloomberggpt-the-first-large-language-model-for-finance-61cc92075075)
* Self-Instruct: Aligning LM with Self Generated Instructions: [Github repo](https://github.com/yizhongw/self-instruct)
* [LangChain for QA](https://medium.com/@onkarmishra/using-langchain-for-question-answering-on-own-data-3af0a82789ed)
* HuggingFace. Fine-tuning a model on a question-answering task: [Notebook1](https://github.com/huggingface/notebooks/blob/main/examples/question_answering.ipynb), [Notebook2](https://github.com/huggingface/notebooks/blob/main/examples/question_answering.ipynb)
* [Anyscale. Numbers every LLM Developer should know](https://www.anyscale.com/blog/num-every-llm-developer-should-know)
* [Anyscale. Building RAG-based LLM Applications for Production (Part 1)](https://www.anyscale.com/blog/a-comprehensive-guide-for-building-rag-based-llm-applications-part-1)
* [Anyscale. Using LoRa for fine-tuning Llama 2](https://www.anyscale.com/blog/fine-tuning-llms-lora-or-full-parameter-an-in-depth-analysis-with-llama-2?ref=hackernoon.com)
* [Why You (Probably) Don’t Need to Fine-tune an LLM](https://www.tidepool.so/2023/08/17/why-you-probably-dont-need-to-fine-tune-an-llm/?ref=hackernoon.com)
* [FAISS, several methods for similarity search](https://github.com/facebookresearch/faiss)


### dataset
[data](data)

### remarks
* Models like The MosaicML MPT-7B [model](https://www.mosaicml.com/blog/mpt-7b) or [Llama2 7B](https://ai.meta.com/llama/) are too large to run on Google Colab free account even though they are the smallest in their respective families. With a free colab account, 12Gb RAM memory is available. Estimation of the RAM required for 7B parameters model: model parameters 28 Gb, model overhead 3-6 Gb, I/O buffers 1-2 Gb, OS/Framework overhead 2-4 Gb, In total - 34-40 Gb.
* [llama.cpp](https://github.com/ggerganov/llama.cpp) is a plain C/C++ implementation of LLaMA model using 4-bit integer quantization. [TheBloke/Llama-2-13B-chat-GGUF](https://huggingface.co/TheBloke/Llama-2-13B-chat-GGUF) model with 13B parameters requires 11.73 Gb maximum
* FAISS supports searching only from RAM, as disk databases are orders of magnitude slower, even with SSDs.
* The [RAG-Token Model](https://huggingface.co/facebook/rag-token-nq) of the the [paper](https://arxiv.org/pdf/2005.11401.pdf) is a uncased model, which means that capital letters are simply converted to lower-case letters. The complete lecagy index requires over 75 GB of RAM.

# thesis
Reading and Understanding Annual Reports (SEC 10-K Filings) using LLM and RAG Method


### Master's Thesis Plan
- Introduction
  + Overview of the importance of SEC 10-K filings in financial decision-making. Challenges associated with analyzing 10-K reports (emphasizing length and complexity). Introduction to the proposed method using LLMs and RAG.
  + Detailing the goal, which is to develop a method for easy reading and understanding of financial annual reports. Emphasizing the use of open-source LLMs and the advantages it offers over relying on APIs.
  + Discussing the scope of the research and its potential impact on democratizing access to financial information. Highlighting the significance of the proposed system in improving accessibility and understanding of financial reports.
  + Challenges in processing 10-K filings, including the use of neural networks for section recognition.
  + Overview of the SEC's EDGAR database and challenges in retrieving 10-K filings. Introduction to potential solutions.
- Literature Review
  + Reviewing relevant literature on the use of LLMs in financial analysis. Highlighting previous work for stock price performance prediction.
- System Design
  + Detailing the components, including report materials, reader's questions, and the core system using LLMs and RAG.
  + Emphasizing the choice of the model.
  + Step-by-step explanation of the implementation process, covering embedding, vector storage, similarity-based retrieval, and RAG.
- Experimental Setup
  + Discussion on the various methods for obtaining 10-K filings, including the use of the EDGAR-CORPUS dataset and scraping EDGAR website. Explanation of the chosen method for the experimental phase (pros and cons).
  + Detailing the list of 42 questions prepared for the natural language queries.
  + Explanation of the system setup, including the use of a locally running open-source LLM.
  + Explanation of the limitations associated with using Colab VMs for experiments. Acknowledgment of potential challenges in resource availability and fluctuations.
- Evaluation
  + Discussion on commonly used evaluation metrics (Precision, Recall, F1 Score, Mean Average Precision, and AUC-ROC). Emphasizing challenges in aligning evaluation metrics with practical use cases.
  + Evaluation of system results and comparison with benchmarks (ChatGPT answers and Kay x Cybersyn x LangChain API responses)
- Results and Analysis
  + Showcase of results obtained from the experimental phase, including the performance of the LLM and RAG system.
  + Interpretation of results in the context of the proposed method's effectiveness. Discussion on potential improvements and areas for future research.
- Conclusion
  + Summarizing key findings from the research, including the effectiveness of the proposed method.
  + Highlighting the contributions of the thesis to the field of financial analysis and AI-enabled tutoring systems.
  + Identifying potential avenues for future research and enhancements to the proposed system.
  + Concluding the thesis with a recap of the objectives, findings, and overall significance of the research.


### datasets
1. [scraped 10-k filings, extracted by my own](data). Plain text, refine is needed. The same dataset on [Hugging Face Hub](https://huggingface.co/datasets/winterForestStump/10k_SEC_10examples_text_corpus)
2. [EDGAR-CORPUS](https://zenodo.org/records/5528490). Annual reports from 1993 to 2020 splited into their corresponding items (sections), and provided in a clean, easy-to-use JSON format. [Link to HF dataset](https://huggingface.co/datasets/eloukas/edgar-corpus) and [edgar-crawler github repository](https://github.com/nlpaueb/edgar-crawler)
3. [Kay x Cybersyn x LangChain](https://python.langchain.com/docs/integrations/retrievers/sec_filings?ref=blog.langchain.dev). API retriver of SEC filings (can be used for evaluation)


### questions
We have prepared a list of [42 questions](questions.txt) that are most commonly used in analyzing corporate reports. These questions will be used to test the system

### models / frameworks / databases
1. [TheBloke/Llama-2-13B-chat-GGUF model](https://huggingface.co/TheBloke/Llama-2-13B-chat-GGUF)
2. [Yukang/Llama-2-7b-longlora-100k-ft model](https://huggingface.co/Yukang/Llama-2-7b-longlora-100k-ft), [github](https://osu-nlp-group.github.io/TableLlama/), [github](https://github.com/dvlab-research/LongLoRA)
3. [FinGPT model](https://github.com/AI4Finance-Foundation/FinGPT), [FinGPT/fingpt-mt_llama2-7b_lora on Hugging Face](https://huggingface.co/FinGPT/fingpt-mt_llama2-7b_lora)
4. [ChromaDB](https://github.com/chroma-core/chroma)
5. [LangChain Retrieval](https://python.langchain.com/docs/use_cases/question_answering/)
6. [SentenceTransformers](https://www.sbert.net/). for embedding, [models on HF](https://huggingface.co/sentence-transformers)
7. [Self-RAG](https://github.com/AkariAsai/self-rag)
8. [Pyserini toolkit](https://github.com/castorini/pyserini), for reproducible information retrieval research with sparse and dense representations

### evaluation
Human evaluation with comparison to ChatGPT answers and retrived answers from Kay x Cybersyn x LangChain API


### additional literature
* [Anyscale. Numbers every LLM Developer should know](https://www.anyscale.com/blog/num-every-llm-developer-should-know)
* [Anyscale. Building RAG-based LLM Applications for Production (Part 1)](https://www.anyscale.com/blog/a-comprehensive-guide-for-building-rag-based-llm-applications-part-1)
* [Anyscale. Using LoRa for fine-tuning Llama 2](https://www.anyscale.com/blog/fine-tuning-llms-lora-or-full-parameter-an-in-depth-analysis-with-llama-2?ref=hackernoon.com)
* [Why You (Probably) Don’t Need to Fine-tune an LLM](https://www.tidepool.so/2023/08/17/why-you-probably-dont-need-to-fine-tune-an-llm/?ref=hackernoon.com)


### remarks
* Models like The MosaicML MPT-7B [model](https://www.mosaicml.com/blog/mpt-7b) or [Llama2 7B](https://ai.meta.com/llama/) are too large to run on Google Colab free account even though they are the smallest in their respective families. With a free colab account, 12Gb RAM memory is available. Estimation of the RAM required for 7B parameters model: model parameters 28 Gb, model overhead 3-6 Gb, I/O buffers 1-2 Gb, OS/Framework overhead 2-4 Gb, In total - 34-40 Gb.
* [llama.cpp](https://github.com/ggerganov/llama.cpp) is a plain C/C++ implementation of LLaMA model using 4-bit integer quantization. [TheBloke/Llama-2-13B-chat-GGUF](https://huggingface.co/TheBloke/Llama-2-13B-chat-GGUF) model with 13B parameters requires 11.73 Gb maximum
* FAISS supports searching only from RAM, as disk databases are orders of magnitude slower, even with SSDs.
* The [RAG-Token Model](https://huggingface.co/facebook/rag-token-nq) of the the [paper](https://arxiv.org/pdf/2005.11401.pdf) is a uncased model, which means that capital letters are simply converted to lower-case letters. The complete lecagy index requires over 75 GB of RAM.
* There are apps [LangChain](https://langchain-text-splitter.streamlit.app/) and [Chunkviz](https://chunkviz.up.railway.app/#explanation) where you can test various chunk sizes to gain some intuition; in particular, it's worth examining where the document is split using various split sizes or strategies and whether semantically related content is unnaturally split.

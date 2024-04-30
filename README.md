# thesis
Reading and Understanding Annual Reports Using Large Language Models LLM and Retrieval-Augmented Generation.


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

### experiments board
[Experiments Board](https://whimsical.com/thesis-experiments-UDsNTrQfqfqMduUfbus1d8)
[LangChain Smith projects](https://smith.langchain.com/o/7a22f395-21ae-54fe-a44d-3212a54e04ee/projects?paginationState=%7B%22pageIndex%22%3A0%2C%22pageSize%22%3A10%7D&chartedColumn=latency_p50)

### datasets
* modified [edgar-crawler](https://github.com/nlpaueb/edgar-crawler) code to download and extract reports from the [FINANCEBENCH](https://arxiv.org/pdf/2311.11944.pdf) 150 questions dataset. 

### questions
* prepared list of [35 questions](questions/questions_ver2.txt) that are most commonly used in analyzing corporate reports. These questions will be used to test the system

### models / frameworks / databases
1. [TheBloke/Llama-2-7B-Chat-GPTQ](https://huggingface.co/TheBloke/Llama-2-7B-Chat-GPTQ)
2. [GPTQ paper](https://arxiv.org/pdf/2210.17323)
3. [ChromaDB](https://github.com/chroma-core/chroma)
4. [LangChain Retrieval](https://python.langchain.com/docs/modules/data_connection/)
5. [BAAI/bge-small-en-v1.5](https://huggingface.co/BAAI/bge-small-en-v1.5)
6. [Embeddings leaderboard](https://huggingface.co/spaces/mteb/leaderboard)

### evaluation
1. Human evaluation
2. [Ragas](https://docs.ragas.io/en/latest/index.html)
3. [An Overview on RAG Evaluation](https://weaviate.io/blog/rag-evaluation)
4. [ARES: An Automated Evaluation Framework for Retrieval-Augmented Generation Systems](https://arxiv.org/pdf/2311.09476.pdf)
5. [Evaluating RAG: A journey through metrics](https://www.elastic.co/search-labs/blog/articles/evaluating-rag-metrics)
6. [Best Practices for LLM Evaluation of RAG Applications](https://www.databricks.com/blog/LLM-auto-eval-best-practices-RAG)
7. PatronusAI Enterprise Scenarios [leaderboard](https://huggingface.co/spaces/PatronusAI/enterprise_scenarios_leaderboard)


### additional literature
* [Kay x Cybersyn x LangChain](https://python.langchain.com/docs/integrations/retrievers/sec_filings?ref=blog.langchain.dev). API retriver of SEC filings (can be used for evaluation)
* [Anyscale. Numbers every LLM Developer should know](https://www.anyscale.com/blog/num-every-llm-developer-should-know)
* [Anyscale. Building RAG-based LLM Applications for Production (Part 1)](https://www.anyscale.com/blog/a-comprehensive-guide-for-building-rag-based-llm-applications-part-1)
* [Anyscale. Using LoRa for fine-tuning Llama 2](https://www.anyscale.com/blog/fine-tuning-llms-lora-or-full-parameter-an-in-depth-analysis-with-llama-2?ref=hackernoon.com)
* [Why You (Probably) Don’t Need to Fine-tune an LLM](https://www.tidepool.so/2023/08/17/why-you-probably-dont-need-to-fine-tune-an-llm/?ref=hackernoon.com)


### remarks
* Models like The MosaicML MPT-7B [model](https://www.mosaicml.com/blog/mpt-7b) or [Llama2 7B](https://ai.meta.com/llama/) are too large to run on Google Colab free account even though they are the smallest in their respective families. With a free colab account, 12Gb RAM memory is available. Estimation of the RAM required for 7B parameters model: model parameters 28 Gb, model overhead 3-6 Gb, I/O buffers 1-2 Gb, OS/Framework overhead 2-4 Gb, In total - 34-40 Gb.
* [llama.cpp](https://github.com/ggerganov/llama.cpp) is a plain C/C++ implementation of LLaMA model using 4-bit integer quantization. [TheBloke/Llama-2-13B-chat-GGUF](https://huggingface.co/TheBloke/Llama-2-13B-chat-GGUF) model with 13B parameters requires 11.73 Gb maximum
* Quantized Llama 2 model. The recommendation is to use a 4-bit quantized model, on the largest parameter size you can run on your gpu (a rough estimate would be 1b parameters = 1gb vram).
* The model size. The industry standard is 32bit per parameter, since we are talking about 13B let me give an example using that. 13B x 32bit = 13,000,000,000 parameter × 32 bit ÷ 8 bits per byte ÷1,024 bytes per kilobyte ÷ 1,024 kilobytes per megabyte ÷1,024 megabytes per gigabyte ≈ 48.43 gigabytes. Meaning in 16bit format the size is half that = 48.42... / 2 (half the bits) ≈ 24.21 gigabytes, meaning in 8bit it becomes half ≈ 12.1 gigabytes and finally in 4bit format ≈ 6 gigabytes.
* The second piece of information you need to know is how you get a model loaded, the most effective and efficient way is to use VRAM since GPUs are very fast with floating point operations and matrix mathematics which means to get best results (fastest inference) you have to load it all to VRAM, now you can see why we need the quantized (smaller versions). For a 13B parameter model in 32bit format you need a little bit more than 2 x 4090 which is super expensive to get as a home setup because it will still need power and so on, while the quality of output at 4bit quantization is nearly 95% of original model, which if compared to the saving you get in model size saving is a very profitable deal.
* https://oobabooga.github.io/blog/posts/perplexities/ - a link comparing and explaining the effect of quantization on model perplexity and comparison between each level
* The comprehensive [study](https://github.com/Tongji-KGLLM/RAG-Survey) of RAG systems
* FAISS supports searching only from RAM, as disk databases are orders of magnitude slower, even with SSDs.
* The [RAG-Token Model](https://huggingface.co/facebook/rag-token-nq) of the the [paper](https://arxiv.org/pdf/2005.11401.pdf) is a uncased model, which means that capital letters are simply converted to lower-case letters. The complete lecagy index requires over 75 GB of RAM.
* There are apps [LangChain](https://langchain-text-splitter.streamlit.app/) and [Chunkviz](https://chunkviz.up.railway.app/#explanation) where you can test various chunk sizes to gain some intuition; in particular, it's worth examining where the document is split using various split sizes or strategies and whether semantically related content is unnaturally split.

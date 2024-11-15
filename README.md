# thesis
Reading and Understanding Annual Reports Using Large Language Models LLM and Retrieval-Augmented Generation.

The primary research questions:
- How can open-source utilities (libraries and models) be effectively combined with information retrieval to enhance the question-answering and understanding of financial reports?
- What are the results of the RAG pipeline with using open-source utilities on real-life finance domain specific questions?

Methodology:
- A comprehensive review of existing research and theoretical foundation on embeddings, LLMs, vectore storage, RAG systems, and their applications. 
- Using open-source LLMs and frameworks to develop a RAG system that can process and analyze financial reports. The system will be designed to run locally (without using any API calls), ensuring cost-effectiveness.
- Conducting experiments to assess the quality of the system's responses to real financial queries. This includes testing the system on questions of varying complexity and specificity, as well as manual evaluation of its accuracy.


### experiments board
[Experiments Board](https://whimsical.com/thesis-experiments-UDsNTrQfqfqMduUfbus1d8)
[LangChain Smith projects](https://smith.langchain.com/o/7a22f395-21ae-54fe-a44d-3212a54e04ee/projects?paginationState=%7B%22pageIndex%22%3A0%2C%22pageSize%22%3A10%7D&chartedColumn=latency_p50)

### datasets
* modified [edgar-crawler](https://github.com/nlpaueb/edgar-crawler) code to download and extract reports from the [FINANCEBENCH](https://arxiv.org/pdf/2311.11944.pdf) 150 questions dataset. 

### questions
* prepared list of [35 questions](questions/questions_ver2.txt) that are most commonly used in analyzing corporate reports. These questions will be used to test the system
* 150 questions from [FINANCEBENCH](https://arxiv.org/pdf/2311.11944.pdf)

### models / frameworks / databases
1. [microsoft/Phi-3-mini-4k-instruct](https://huggingface.co/microsoft/Phi-3-mini-4k-instruct)
2. [ChromaDB](https://github.com/chroma-core/chroma)
3. [LangChain](https://python.langchain.com/docs/introduction/)
4. [BAAI/bge-small-en-v1.5](https://huggingface.co/BAAI/bge-small-en-v1.5)
5. [FlashRank](https://github.com/PrithivirajDamodaran/FlashRank)
6. [FlagEmbedding Reranker](https://github.com/FlagOpen/FlagEmbedding/tree/master/FlagEmbedding/llm_reranker)

### evaluation
1. Manual evaluation


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

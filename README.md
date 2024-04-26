# Langchain Pandas Dataframe Agent using Local Model

## Approach 1 - Using Custom Langchain Pandas DataFrame Agent for Local LLMs

> NOTE: The notebook was run using Google Colab A100 (40GB). The `meta-llama/Llama-2-13b-hf` model requires ~36GB GPU memory with 4-bit quantization.

### Installation

```
!pip install -qU transformers==4.31.0 accelerate==0.21.0 einops==0.6.1 langchain==0.0.240 xformers==0.0.20 bitsandbytes==0.41.0

```

### Tasks Accomplished

- [x] Using Local LLM with Langchain Pandas DataFrame Agent
   
- [x] 4-bit quantization for Llama-2-70b-chat-hf
   
- [x] `custom_create_pandas_dataframe_agent` to use local LLMs with Langchain


### To do

- [ ] Parse output to JSON instead of text.
   
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;- **Challenge**: Including a `SUFFIX` specifying the output formatting currently breaks the `Thought – Action – Action Input - Observation` cycle, making it unable to call the Python AREPL to execute commands. 

> NOTE: In the Llama 2 paper they mentioned that it was difficult to keep Llama 2 chat models following instructions over multiple interactions.
> One way they found that improves this is by inserting a reminder of the instructions to each user query. 

- [ ] Running complex queries leads to Out of Memory (OOM) error on Colab’s A100 (40GB) GPU after a few steps, even after using 4-bit quantization.

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;- **Potential Solution**: Serving the local model as an API using [vLLM](https://github.com/vllm-project/vllm) (for higher throughput), [DeepSpeed](https://www.deepspeed.ai/) (ZeRO-2 or ZeRO-3) and/or [Ray Serve](https://docs.ray.io/en/latest/serve/index.html) (over multiple GPUs) would allow GPU memory optimization and higher throughput (lower inference time).

- [ ] Model Response Time
   
&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;- **Challenge**: Since there’s not much optimization possible without serving the model, the inference time is on the higher side (~1 minute/query).

&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;- **Potential Solution**: Serving the local model with vLLM + DeepSpeed and/or Ray and then computing average inference times for a subset (~100-200 queries) to provide accurate throughput (~x tokens/second).

- [ ] Evaluating Agent/Pipeline Performance


## Approach 2 - Using RAG Pipeline using CSV Loader, VectorDB, and RetrievalQA Chain with Local Model

> Work in Progress


## Approach 3 - Using Knowledge Graphs to improve the accuracy of the RAG pipeline with Local model
> Work in Progress

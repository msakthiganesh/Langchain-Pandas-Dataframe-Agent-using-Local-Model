# Langchain Pandas Dataframe Agent using Local Model

> NOTE: The notebook was run using Google Colab A100 (40GB). The `meta-llama/Llama-2-13b-hf` model requires ~36GB with 4-bit quantization.

### Installation

```
!pip install -qU transformers==4.31.0 accelerate==0.21.0 einops==0.6.1 langchain==0.0.240 xformers==0.0.20 bitsandbytes==0.41.0

```

### Things to Improve

1.	Parse output to JSON instead of text.
Issue Faced – Including a `SUFFIX` specifying the output formatting currently breaks the `Thought – Action – Action Input - Observation` cycle, making it unable to call the Python AREPL to execute commands. 

2.	Running complex queries leads to Out of Memory (OOM) error on Colab’s A100 (40GB) GPU after a few steps, even after using 4-bit quantization. Serving the local model as an API using [vLLM](https://github.com/vllm-project/vllm) (for higher throughput), [DeepSpeed](https://www.deepspeed.ai/) (ZeRO-2 or ZeRO-3) and/or [Ray Serve](https://docs.ray.io/en/latest/serve/index.html) (over multiple GPUs) would allow GPU memory optimization.

3.	Model Response Time – Since there’s not much optimization possible without serving the model, the inference time is on the higher side (~1 minute/query) .

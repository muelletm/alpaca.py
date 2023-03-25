# Alpaca.py

A python client based on [alpaca.cpp](https://github.com/antimatter15/alpaca.cpp).

The most important change W.R.T the original code is that context is not maintained between calls. That is there is not state so by default it doesn't behave like a chat bot. That said it's easy to add that simply by keeping track of all user and system utterances.

## Build

Build cpp binary:

```shell
cd cpp
mkdir -p build
make
cd ..
```

Set up python environment:

```shell
conda create -n alpaca python=3.8
pip install -r requirements.txt 
conda activate alpaca
```

## Try it out

Command line:

```shell
python demo_cli.py --alpaca-cli-path cpp/build/alpaca --model-path $MODEL_DIR/ggml-alpaca-7b-q4.bin 
```

Web Demo (Streamlit):

```shell
export ALPACA_CLI_PATH="$PWD/cpp/build/alpaca"
export ALPACA_MODEL_PATH="$MODEL_DIR/ggml-alpaca-7b-q4.bin"
python demo_cli.py --alpaca-cli-path cpp/build/alpaca --model-path $MODEL_DIR/ggml-alpaca-7b-q4.bin 
```

```python
from alpaca import Alpaca

alpaca = Alpaca(alpaca_cli_path, model_path)
try:
    output = alpaca.run_simple("Are alpacas afraid of snakes?")["output"]
finally:
    alpaca.stop()
```

## Credit

This is a fork of [alpaca.cpp](https://github.com/antimatter15/alpaca.cpp), which itself gives the following credit:
> This combines [Facebook's LLaMA](https://github.com/facebookresearch/llama), [Stanford Alpaca](https://crfm.stanford.edu/2023/03/13/alpaca.html), [alpaca-lora](https://github.com/tloen/alpaca-lora) and [corresponding weights](https://huggingface.co/tloen/alpaca-lora-7b/tree/main) by Eric Wang (which uses [Jason Phang's implementation of LLaMA](https://github.com/huggingface/transformers/pull/21955) on top of Hugging Face Transformers), and [llama.cpp](https://github.com/ggerganov/llama.cpp) by Georgi Gerganov. The chat implementation is based on Matvey Soloviev's [Interactive Mode](https://github.com/ggerganov/llama.cpp/pull/61) for llama.cpp. Inspired by [Simon Willison's](https://til.simonwillison.net/llms/llama-7b-m2) getting started guide for LLaMA. [Andy Matuschak](https://twitter.com/andy_matuschak/status/1636769182066053120)'s thread on adapting this to 13B, using fine tuning weights by [Sam Witteveen](https://huggingface.co/samwit/alpaca13B-lora). 
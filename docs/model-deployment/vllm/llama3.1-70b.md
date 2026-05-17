# Llama-3.1-70B on vLLM

## 模型简介

Llama 3.1 是 Meta 推出的开源大语言模型，70B 版本支持 128K 上下文、8 种语言，适合多语言问答、代码生成等场景。

## 模型列表

| 模型权重 | 量化方式 | 推荐硬件 | 卡数 | 部署方式 | 启动命令 |
| -------- | -------- | -------- | ---- | -------- | -------- |
| [LLM-Research/Meta-Llama-3.1-70B-Instruct](https://www.modelscope.cn/models/LLM-Research/Meta-Llama-3.1-70B-Instruct) | BF16 | BW1100 | 2 | IFB | [**`>_`**](#meta-llama-31-70b-instruct-ifb-bw1100-2x) |

## 启动命令

### Meta-Llama-3.1-70B-Instruct IFB BW1100 2x

```bash
export VLLM_USE_MODELSCOPE=1

vllm serve LLM-Research/Meta-Llama-3.1-70B-Instruct \
    --trust-remote-code \
    --dtype bfloat16 \
    -tp 2 \
    --max-model-len 32768 \
    --gpu-memory-utilization 0.90 \
    --disable-log-requests \
    --enable-prefix-caching \
    --kv-cache-dtype fp8_e4m3
```

## API 调用

### IFB

```python
from openai import OpenAI

client = OpenAI(base_url="http://localhost:8000/v1", api_key="not-needed")

response = client.chat.completions.create(
    model="LLM-Research/Meta-Llama-3.1-70B-Instruct",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "What is the capital of France?"},
    ],
    max_tokens=2048,
)
print(response.choices[0].message.content)
```

```bash
curl http://localhost:8000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "LLM-Research/Meta-Llama-3.1-70B-Instruct",
    "messages": [
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "What is the capital of France?"}
    ],
    "max_tokens": 128
  }'
```

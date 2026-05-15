# DeepSeek-R1-Distill-Llama-70B on vLLM

## 模型简介

DeepSeek-R1-Distill-Llama-70B 基于 Llama3.3-70B 蒸馏，适合高质量推理与复杂问答任务。

## 模型列表

| 模型 | 参数量 | 上下文 | 量化方式 | vLLM 版本 | 推荐硬件 |
|------|--------|--------|---------|-----------|---------|
| DeepSeek-R1-Distill-Llama-70B | 70B | 128K | BF16 | 0.1.8 | 4x BW1000 64GB TP / 2x BW1100 144GB TP |

## 启动命令

```bash
export VLLM_HCU_USE_FLASH_ATTN=1
export VLLM_HCU_USE_FLASH_ATTN_UNIFIED=1
export VLLM_HCU_USE_CUSTOM_TOPK_TOPP_SAMPLER=1

vllm serve deepseek-ai/DeepSeek-R1-Distill-Llama-70B \
    -tp 4 \
    --dtype bfloat16 \
    --trust-remote-code \
    --disable-cascade-attn \
    --max-num-batched-tokens 10240
```

## API 调用

```python
from openai import OpenAI

client = OpenAI(base_url="http://localhost:8000/v1", api_key="not-needed")

response = client.chat.completions.create(
    model="deepseek-ai/DeepSeek-R1-Distill-Llama-70B",
    messages=[
        {"role": "system", "content": "你是一个专业的推理助手。"},
        {"role": "user", "content": "给出一个分布式缓存一致性方案。"},
    ],
    max_tokens=1024,
    temperature=0.6,
)
print(response.choices[0].message.content)
```

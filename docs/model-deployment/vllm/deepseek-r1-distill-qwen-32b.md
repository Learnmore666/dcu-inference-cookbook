# DeepSeek-R1-Distill-Qwen-32B on vLLM

## 模型简介

DeepSeek-R1-Distill-Qwen-32B 基于 Qwen2.5-32B 蒸馏，适合复杂推理与代码生成场景。

## 模型列表

| 模型 | 参数量 | 上下文 | 量化方式 | 推荐硬件 |
|------|--------|--------|---------|---------|
| DeepSeek-R1-Distill-Qwen-32B | 32B | 128K | BF16 | 2x BW1000 64GB TP / 1x BW1100 144GB |

## 启动命令

```bash
export VLLM_HCU_USE_FLASH_ATTN=1
export VLLM_HCU_USE_FLASH_ATTN_UNIFIED=1
export VLLM_HCU_USE_CUSTOM_TOPK_TOPP_SAMPLER=1

vllm serve deepseek-ai/DeepSeek-R1-Distill-Qwen-32B \
    -tp 2 \
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
    model="deepseek-ai/DeepSeek-R1-Distill-Qwen-32B",
    messages=[
        {"role": "system", "content": "你是一个专业的推理助手。"},
        {"role": "user", "content": "请解释一下 A* 搜索算法的时间复杂度。"},
    ],
    max_tokens=1024,
    temperature=0.6,
)
print(response.choices[0].message.content)
```

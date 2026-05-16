# DeepSeek-R1-Distill-Llama-70B on SGLang

## 模型简介

DeepSeek-R1-Distill-Llama-70B 基于 Llama3.3-70B 蒸馏，适合高质量推理与复杂问答任务，可在 DCU 上通过 SGLang 进行 BF16 推理部署。

## 模型列表

| 模型 | 参数量 | 上下文 | 量化方式 | 推荐硬件 |
|------|--------|--------|---------|---------|
| DeepSeek-R1-Distill-Llama-70B | 70B | 128K | BF16 | 4x BW1000 64GB TP / 2x BW1100 144GB TP |

## 启动命令

```bash
export SGLANG_ENABLE_SPEC_V2=1
export USE_DCU_CUSTOM_ALLREDUCE=1
export SGLANG_USE_LIGHTOP=1
export SGLANG_USE_FUSED_TOPK_SOFTMAX=1
export SGLANG_KV_LAYOUT_DCU_FA=1

python -m sglang.launch_server \
    --model-path deepseek-ai/DeepSeek-R1-Distill-Llama-70B \
    --tp-size 4 \
    --trust-remote-code \
    --dtype bfloat16 \
    --port 30000 \
    --attention-backend fa3 \
    --mem-fraction-static 0.90 \
    --disable-radix-cache \
    --chunked-prefill-size -1
```

## API 调用

```python
from openai import OpenAI

client = OpenAI(base_url="http://localhost:30000/v1", api_key="not-needed")

response = client.chat.completions.create(
    model="deepseek-ai/DeepSeek-R1-Distill-Llama-70B",
    messages=[
        {"role": "system", "content": "你是一个专业的推理助手。"},
        {"role": "user", "content": "给出一个分布式缓存一致性方案。"},
    ],
    max_tokens=1024,
)
print(response.choices[0].message.content)
```

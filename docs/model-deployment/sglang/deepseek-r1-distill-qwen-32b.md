# DeepSeek-R1-Distill-Qwen-32B on SGLang

## 模型简介

DeepSeek-R1-Distill-Qwen-32B 基于 Qwen2.5-32B 蒸馏，可在 DCU 上通过 SGLang 进行 BF16 推理部署。

## 模型列表

| 模型 | 参数量 | 上下文 | 量化方式 | 推荐硬件 |
|------|--------|--------|---------|---------|
| DeepSeek-R1-Distill-Qwen-32B | 32B | 128K | BF16 | 2x BW1000 64GB TP / 1x BW1100 144GB |

## 启动命令

```bash
export SGLANG_ENABLE_SPEC_V2=1
export USE_DCU_CUSTOM_ALLREDUCE=1
export SGLANG_USE_LIGHTOP=1
export SGLANG_USE_FUSED_TOPK_SOFTMAX=1
export SGLANG_USE_CAUSAL_CONV1D=1
export SGLANG_KV_LAYOUT_DCU_FA=1

python -m sglang.launch_server \
    --model-path deepseek-ai/DeepSeek-R1-Distill-Qwen-32B \
    --tp-size 2 \
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
    model="deepseek-ai/DeepSeek-R1-Distill-Qwen-32B",
    messages=[
        {"role": "system", "content": "你是一个专业的推理助手。"},
        {"role": "user", "content": "请写一个并发限流器的设计思路。"},
    ],
    max_tokens=1024,
)
print(response.choices[0].message.content)
```

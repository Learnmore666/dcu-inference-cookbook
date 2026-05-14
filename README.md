<div align="center">

![DCU Inference Cookbook Logo](./assets/logo.svg)

</div>


## 📖 简介

本仓库整理了在 DCU 硬件上部署、调优和运行 AI 模型的经验与最佳实践，涵盖：

- **大语言模型 (LLM)** — 文本生成、对话、代码补全等
- **全模态模型 (Omni)** — 文本+图像+音频统一理解与生成
- **多模态模型 (VLM)** — 视觉语言模型、图像生成、语音识别等
- **环境搭建** — DTK 工具链、驱动安装、Python 环境配置
- **模型部署** — 推理服务、分布式部署、多卡方案
- **性能优化** — 显存优化、算子调优、量化、KV Cache 策略
- **框架适配** — vLLM (含 Omni)、SGLang、Transformers、ComfyUI 等
- **故障排查** — 常见问题、错误码、FAQ
- **性能基准** — 各模型在 DCU 上的实测数据

## 📋 模型列表

<table>
  <tr>
    <td align="center"><b>厂商</b></td>
    <td><b>模型</b></td>
    <td><b>框架</b></td>
    <td align="center"><b>K100_AI</b></td>
    <td align="center"><b>BW1000</b></td>
    <td align="center"><b>BW1100</b></td>
  </tr>
  <tbody>
    <tr>
      <td rowspan="16" align="center"><img src="https://github.com/QwenLM.png?size=64" height="40"/><br/>Alibaba</td>
      <td rowspan="2">Qwen2.5-VL</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Qwen3</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/vllm/qwen3.md">✅</a></td>
      <td align="center"><a href="docs/model-deployment/vllm/qwen3.md">✅</a></td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/sglang/qwen3.md">✅</a></td>
      <td align="center"><a href="docs/model-deployment/sglang/qwen3.md">✅</a></td>
    </tr>
    <tr>
      <td rowspan="2">Qwen3-Coder</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Qwen3-Coder-Next</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Qwen3-Next</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Qwen3-VL</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/vllm/qwen3-vl.md">✅</a></td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Qwen3.5</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/vllm/qwen3.5.md">✅</a></td>
      <td align="center"><a href="docs/model-deployment/vllm/qwen3.5.md">✅</a></td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/sglang/qwen3.5.md">✅</a></td>
      <td align="center"><a href="docs/model-deployment/sglang/qwen3.5.md">✅</a></td>
    </tr>
    <tr>
      <td rowspan="2">Qwen3.6</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="16" align="center"><img src="https://github.com/deepseek-ai.png?size=64" height="40"/><br/>DeepSeek</td>
      <td rowspan="2">DeepSeek-Math-V2</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">DeepSeek-OCR</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">DeepSeek-OCR-2</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">DeepSeek-R1</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/sglang/deepseek-r1.md">✅</a></td>
    </tr>
    <tr>
      <td rowspan="2">DeepSeek-V3</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/vllm/deepseek-v3.md">✅</a></td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">DeepSeek-V3.1</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">DeepSeek-V3.2</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/vllm/deepseek-v3.2.md">✅</a></td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/sglang/deepseek-v3.2.md">✅</a></td>
    </tr>
    <tr>
      <td rowspan="2">DeepSeek-V4</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="6" align="center"><img src="https://github.com/meta-llama.png?size=64" height="40"/><br/>Meta</td>
      <td rowspan="2">Llama-3.1</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Llama-3.3-70B</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Llama 4</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="20" align="center"><img src="https://github.com/THUDM.png?size=64" height="40"/><br/>Zhipu AI</td>
      <td rowspan="2">GLM-4.5</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">GLM-4.5V</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">GLM-4.6</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">GLM-4.6V</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">GLM-4.7</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">GLM-4.7-Flash</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">GLM-5</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/vllm/glm-5.md">✅</a></td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/sglang/glm-5.md">✅</a></td>
    </tr>
    <tr>
      <td rowspan="2">GLM-5.1</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">GLM Glyph</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">GLM-OCR</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2" align="center"><img src="https://github.com/google.png?size=64" height="40"/><br/>Google</td>
      <td rowspan="2">Gemma 4</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2" align="center"><img src="https://github.com/openai.png?size=64" height="40"/><br/>OpenAI</td>
      <td rowspan="2">GPT-OSS</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="8" align="center"><img src="https://github.com/MoonshotAI.png?size=64" height="40"/><br/>Moonshot AI</td>
      <td rowspan="2">Kimi-K2</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/vllm/kimi-k2.md">✅</a></td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/sglang/kimi-k2.md">✅</a></td>
    </tr>
    <tr>
      <td rowspan="2">Kimi-K2.5</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/vllm/kimi-k2.5.md">✅</a></td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/sglang/kimi-k2.5.md">✅</a></td>
    </tr>
    <tr>
      <td rowspan="2">Kimi-K2.6</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Kimi-Linear</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="6" align="center"><img src="https://github.com/MiniMax-AI.png?size=64" height="40"/><br/>MiniMax</td>
      <td rowspan="2">MiniMax-M2</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">MiniMax-M2.5</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/vllm/minimax-2.x.md">✅</a></td>
      <td align="center"><a href="docs/model-deployment/vllm/minimax-2.x.md">✅</a></td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/sglang/minimax-m2.5.md">✅</a></td>
      <td align="center"><a href="docs/model-deployment/sglang/minimax-m2.5.md">✅</a></td>
    </tr>
    <tr>
      <td rowspan="2">MiniMax-M2.7</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="6" align="center"><img src="https://github.com/NVIDIA.png?size=64" height="40"/><br/>NVIDIA</td>
      <td rowspan="2">Nemotron3-Nano</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Nemotron3-Nano-Omni</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Nemotron3-Super</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="4" align="center"><img src="https://github.com/PaddlePaddle.png?size=64" height="40"/><br/>Baidu</td>
      <td rowspan="2">Ernie4.5</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Ernie4.5-VL</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="4" align="center"><img src="https://github.com/stepfun-ai.png?size=64" height="40"/><br/>StepFun</td>
      <td rowspan="2">Step3-VL-10B</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Step-3.5</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="8" align="center"><img src="https://github.com/InclusionAI.png?size=64" height="40"/><br/>InclusionAI</td>
      <td rowspan="2">LLaDA 2.1</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Ling-2.5-1T</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Ling-2.6</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Ring-2.5-1T</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="4" align="center"><img src="https://github.com/InternLM.png?size=64" height="40"/><br/>InternLM</td>
      <td rowspan="2">Intern-S1</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Intern-S2-Preview</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2" align="center"><img src="https://github.com/OpenGVLab.png?size=64" height="40"/><br/>InternVL</td>
      <td rowspan="2">InternVL3.5</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2" align="center"><img src="https://github.com/OpenBMB.png?size=64" height="40"/><br/>OpenBMB</td>
      <td rowspan="2">MiniCPM-V 4.6</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2" align="center"><img src="https://github.com/jina-ai.png?size=64" height="40"/><br/>Jina AI</td>
      <td rowspan="2">Jina-reranker-m0</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="8" align="center"><img src="https://github.com/mistralai.png?size=64" height="40"/><br/>Mistral AI</td>
      <td rowspan="2">Devstral 2</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Ministral-3</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Mistral Medium 3.5</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2">Mistral Small 4</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="4" align="center"><img src="https://github.com/XiaoMi.png?size=64" height="40"/><br/>Xiaomi</td>
      <td rowspan="2">MiMo-V2-Flash</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center"><a href="docs/model-deployment/sglang/mimo-v2-flash.md">✅</a></td>
    </tr>
    <tr>
      <td rowspan="2">MiMo-V2.5</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td rowspan="2" align="center"><img src="https://github.com/flashlabs-ai.png?size=64" height="40"/><br/>FlashLabs</td>
      <td rowspan="2">Chroma-1.0</td>
      <td>vLLM</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
    <tr>
      <td>SGLang</td>
      <td align="center">-</td>
      <td align="center">-</td>
      <td align="center">-</td>
    </tr>
  </tbody>
</table>

## 🤝 贡献

欢迎提交 Issue 和 PR！详见 [CONTRIBUTING.md](CONTRIBUTING.md)。

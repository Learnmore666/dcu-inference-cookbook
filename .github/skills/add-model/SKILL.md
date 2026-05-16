---
name: add-model
description: Guide for adding a new model deployment doc to dcu-inference-cookbook. Use this when asked to add a new model or create a new model deployment page.
---

# 新增模型部署文档规范

## 模型列表表格格式

模型部署文档的 `## 模型列表` 章节必须包含以下列，且顺序固定：

| 模型权重 | 量化方式 | 推荐硬件 | 卡数 | 部署方式 | 启动命令 |
| -------- | -------- | -------- | ---- | -------- | -------- |

### 各列说明

- **模型权重**：ModelScope 上 hygon 量化的 channelwise 模型名称，带链接。格式：
  `[hygon/<MODEL-NAME>](https://www.modelscope.cn/models/hygon/<MODEL-NAME>)`
  例如：`[hygon/GLM-5-Channel-INT4-w4a8](https://www.modelscope.cn/models/hygon/GLM-5-Channel-INT4-w4a8)`
  同一模型的多个量化行，后续行的模型权重列留空。

- **量化方式**：使用标准格式，例如：`INT4 W4A8`、`INT8 W8A8`、`FP8 W8A8`、`BF16`。

- **推荐硬件**：只使用以下官方产品名称（不带 GB 规格前缀外的其他字样）：
  - `K100_AI`
  - `BW1000 64GB`（简写 `BW1000`）
  - `BW1100 144GB`（简写 `BW1100`）

- **卡数**：整数，表示所需 DCU 数量。

- **部署方式**：`IFB`（单机推理）或 `PD`（预填充-解码分离）。

- **启动命令**：带 `>_` 图标的锚点链接，跳转到文档内对应的启动命令章节。格式：
  `[`>_` <QUANT> <MODE>](#<anchor>)`
  例如：`[`>_` W4A8 IFB](#glm-5-w4a8)`

## 启动命令章节格式

每个量化方式对应一个 `###` 子章节，章节锚点需与模型列表中的链接一致。

```markdown
## 启动命令

### <MODEL>-<QUANT>

#### IFB【tp<N>】【<hardware>】

```bash
# 环境变量
export ...

# 启动命令
sglang serve <modelscope_model_id> \
  --tp <N> \
  --trust-remote-code \
  ...
```

#### PD【prefill tp<N>】【decode tp<N>】【<hardware>】
...
```

## 模型变量

- **模型 ID**：使用 ModelScope 上的完整路径，例如 `hygon/GLM-5-Channel-INT4-w4a8`
- **启动命令**：使用 `sglang serve`（不用 `python -m sglang.launch_server`）
- **必须加**：`--trust-remote-code`
- **不要加**：`--host 0.0.0.0`（本地部署无需）、`--dist-init-addr`（单节点无需）
- **端口**：SGLang 默认 `30000`，vLLM 默认 `8000`，不在文档中显式指定除非有特殊原因

## 示例（SGLang GLM-5）

```markdown
## 模型列表

| 模型权重 | 量化方式 | 推荐硬件 | 卡数 | 部署方式 | 启动命令 |
| -------- | -------- | -------- | ---- | -------- | -------- |
| [hygon/GLM-5-Channel-INT4-w4a8](https://www.modelscope.cn/models/hygon/GLM-5-Channel-INT4-w4a8) | INT4 W4A8 | BW1000 |  8 | IFB | [`>_` W4A8 IFB](#glm-5-w4a8) |
|                                                                                                   | INT4 W4A8 | BW1000 | 32 | PD  | [`>_` W4A8 PD](#glm-5-w4a8)  |
| [hygon/GLM-5-Channel-INT8-w8a8](https://www.modelscope.cn/models/hygon/GLM-5-Channel-INT8-w8a8) | INT8 W8A8 | BW1100 |  8 | IFB | [`>_` W8A8 IFB](#glm-5-w8a8) |
|                                                                                                   | INT8 W8A8 | BW1100 | 24 | PD  | [`>_` W8A8 PD](#glm-5-w8a8)  |
| [hygon/GLM-5-Channel-FP8-w8a8](https://www.modelscope.cn/models/hygon/GLM-5-Channel-FP8-w8a8)   |  FP8 W8A8 | BW1100 |  8 | IFB | [`>_` FP8 IFB](#glm-5-fp8)   |
|                                                                                                   |  FP8 W8A8 | BW1100 | 24 | PD  | [`>_` FP8 PD](#glm-5-fp8)    |
```

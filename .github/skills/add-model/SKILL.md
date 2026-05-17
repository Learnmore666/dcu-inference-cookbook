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
  同一模型的多个行，后续行的模型权重列留空（用空格对齐）。

- **量化方式**：使用标准格式，例如：`INT4 W4A8`、`INT8 W8A8`、`FP8 W8A8`、`BF16`。

- **推荐硬件**：只使用以下官方产品名称（不带 GB 规格前缀外的其他字样）：
  - `K100_AI`
  - `BW1000 64GB`（简写 `BW1000`）
  - `BW1100 144GB`（简写 `BW1100`）

- **卡数**：整数，表示所需 DCU 数量。

- **部署方式**：
  - `IFB`：单机批量推理
  - `xPyD`：PD 分离，例如 `2P2D`（2 个 prefill 节点 + 2 个 decode 节点）、`1P2D`

- **启动命令**：加粗的 `` >_ `` 图标作为锚点链接，跳转到文档内对应的启动命令章节。格式：
  `[**\`>_\`**](#<anchor>)`
  例如：`[**\`>_\`**](#glm-5-channel-int4-w4a8-ifb-bw1000-8x)`

  **锚点生成规则**（GitHub Markdown）：章节标题全部小写，空格转 `-`，非字母数字非 `-` 字符直接删除（`/` 不转换为 `-`，直接删除）。

## 启动命令章节格式

**每一个表格行对应一个 `###` 章节**，章节标题格式固定为：

```
### <MODEL> <MODE> <HW> <Nx>
```

- `<MODEL>`：模型权重名（不含 `hygon/` 前缀，因为 `/` 会破坏锚点生成）
- `<MODE>`：`IFB` 或 `xPyD`（如 `2P2D`、`1P2D`）
- `<HW>`：推荐硬件简写（如 `BW1000`、`BW1100`）
- `<Nx>`：总卡数加 `x`（如 `8x`、`32x`、`24x`）

例如：
- `### GLM-5-Channel-INT4-w4a8 IFB BW1000 8x` → anchor `#glm-5-channel-int4-w4a8-ifb-bw1000-8x`
- `### GLM-5-Channel-INT4-w4a8 2P2D BW1000 32x` → anchor `#glm-5-channel-int4-w4a8-2p2d-bw1000-32x`

### IFB 章节结构

IFB 章节只有一个 bash 代码块，无需子标题：

```markdown
### GLM-5-Channel-INT4-w4a8 IFB BW1000 8x

```bash
export ...

sglang serve \
  --model-path hygon/GLM-5-Channel-INT4-w4a8 \
  --trust-remote-code \
  --tp-size 8 \
  ...
```
```

### PD 分离章节结构

PD 分离章节开头加一行 IB 网卡配置说明，然后用 `####` 划分各节点：

```markdown
### GLM-5-Channel-INT4-w4a8 2P2D BW1000 32x

网卡配置参考：[IB 网卡](../../troubleshooting/common-issues.md#ib网卡)。

#### P node 0

```bash
export ...

sglang serve \
  --model-path hygon/GLM-5-Channel-INT4-w4a8 \
  --trust-remote-code \
  --host "$(ip route get 1.1.1.1 | awk '/src/{print $7}')" \
  --port 30000 \
  --dist-init-addr "$(ip route get 1.1.1.1 | awk '/src/{print $7}'):5000" \
  --nnodes <P节点数> \
  --node-rank 0 \
  --tp-size <tp> \
  --disaggregation-mode prefill \
  ...
```

#### P node 1

说明：`--dist-init-addr` 填写当前分组 node0 的 IP，下面示例使用 `10.x.x.x`。

```bash
...（同 P node 0，node-rank 改为 1，dist-init-addr 改为固定 IP）
```

#### D node 0

```bash
...（decode 节点，disaggregation-mode decode）
```

#### D node 1

说明：`--dist-init-addr` 填写当前分组 D node0 的 IP，下面示例使用 `10.x.x.x`。

```bash
...（同 D node 0，node-rank 改为 1，dist-init-addr 改为固定 IP）
```

#### Router

```bash
python3 -m sglang_router.launch_router \
  --pd-disaggregation \
  --prefill http://<P_node0_ip>:30000 \
  --decode http://<D_node0_ip>:30000 \
  --policy cache_aware \
  --port 30005
```
```

## 模型相关说明

- **模型 ID**：使用 ModelScope 上的完整路径，例如 `hygon/GLM-5-Channel-INT4-w4a8`
- **启动命令**：使用 `sglang serve`（不用 `python -m sglang.launch_server`）
- **必须加**：`--trust-remote-code`
- **`--host`**：PD 分离模式必须指定，绑定节点对外的 IP；IFB 不需要。推荐用 `$(ip route get 1.1.1.1 | awk '/src/{print $7}')` 自动获取
- **`--dist-init-addr`**：多节点必须指定。格式 `<IP>:5000`。node 0 用自身 IP，其余节点填 node 0 的 IP
- **`--served-model-name`**：PD 分离时所有 P/D 节点必须设置相同的值；API 调用的 `model` 字段须与此一致
- **端口**：SGLang 默认 `30000`，vLLM 默认 `8000`。Router 默认 `30000`，与 P node 0 同机时需换端口（推荐 `30005`）；不在文档中显式指定端口除非有特殊原因

## API 调用章节格式

`## API 调用` 章节分两个子节：

```markdown
## API 调用

### IFB

```python
from openai import OpenAI
client = OpenAI(base_url="http://localhost:30000/v1", api_key="not-needed")
response = client.chat.completions.create(
    model="hygon/GLM-5-Channel-INT4-w4a8",  # 替换为实际使用的模型名
    messages=[...],
    max_tokens=2048,
)
```

```bash
curl http://localhost:30000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"model": "hygon/GLM-5-Channel-INT4-w4a8", "messages": [...], "max_tokens": 128}'
```

### PD 分离

PD 分离模式下，客户端请求发送到 SGLang Router，而非直接发送到 P/D 节点。Router 默认端口为 `30000`，
若与 P node 0 部署在同一机器上需指定其他端口（示例中为 `30005`）。

```python
client = OpenAI(base_url="http://<router_ip>:30005/v1", api_key="not-needed")
```

```bash
curl http://<router_ip>:30005/v1/chat/completions ...
```
```

## 示例（SGLang GLM-5）

```markdown
## 模型列表

| 模型权重 | 量化方式 | 推荐硬件 | 卡数 | 部署方式 | 启动命令 |
| -------- | -------- | -------- | ---- | -------- | -------- |
| [hygon/GLM-5-Channel-INT4-w4a8](https://www.modelscope.cn/models/hygon/GLM-5-Channel-INT4-w4a8) | INT4 W4A8 | BW1000 |  8 | IFB  | [**`>_`**](#glm-5-channel-int4-w4a8-ifb-bw1000-8x)   |
|                                                                                                 | INT4 W4A8 | BW1000 | 32 | 2P2D | [**`>_`**](#glm-5-channel-int4-w4a8-2p2d-bw1000-32x) |
| [hygon/GLM-5-Channel-INT8-w8a8](https://www.modelscope.cn/models/hygon/GLM-5-Channel-INT8-w8a8) | INT8 W8A8 | BW1100 |  8 | IFB  | [**`>_`**](#glm-5-channel-int8-w8a8-ifb-bw1100-8x)   |
|                                                                                                 | INT8 W8A8 | BW1100 | 24 | 1P2D | [**`>_`**](#glm-5-channel-int8-w8a8-1p2d-bw1100-24x) |
| [hygon/GLM-5-Channel-FP8-w8a8](https://www.modelscope.cn/models/hygon/GLM-5-Channel-FP8-w8a8)   |  FP8 W8A8 | BW1100 |  8 | IFB  | [**`>_`**](#glm-5-channel-fp8-w8a8-ifb-bw1100-8x)    |
|                                                                                                 |  FP8 W8A8 | BW1100 | 24 | 1P2D | [**`>_`**](#glm-5-channel-fp8-w8a8-1p2d-bw1100-24x)  |
```

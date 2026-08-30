# hf-cloud-lab

**适用**：Grok编程助理 / 编程 Bot  
**目的**：把 Hugging Face 开源模型拉到 Grok Bot 云电脑本地跑，做小样本实验。HF 当文件仓，默认不走付费 Inference API。  
**工作区**：`/workspace/hf-lab`  
**状态**：规则与门槛已定；云电脑实操还没当面跑通。第一次 setup 后按失败点改本文件，不要猜步骤。

密钥、token、验证码不准写进本文件、日志或 git。

---

## 硬规则

1. 先探测机器，再下载。
2. 只用 HF **Read** token。
3. 默认单模型 ≤ 8GB。留 4GB 内存 + 15GB 磁盘。
4. 14B+ / 70B / SDXL / 微调：拒绝。
5. 没有实验 brief，只允许 setup / pull / smoke。
6. 客户聊天、报价、店照不上传 Hub，不贴进 Issues / Spaces。
7. 付费 Inference、gated 协议硬硬点硬认、删模型：停，交给辉哥。

云电脑社区基线（非官方）：约 8 vCPU / 16GB 内存 / 128GB 盘，通常没独享 GPU。四人共用一台机，拆 Bot 不是隔离。

---

## 适合 / 不适合

|适合|不适合|
|---|---|
|YOLO / OCR / 小分类 / embedding|70B 对话当免费 API|
|Qwen 0.5B–4B，或 7B–8B GGUF Q4 烟测|出图、视频生成、全量微调|
|店里 10–30 张真照小样本|前台实时报价|

第一波优先：YOLOv8n/s、`microsoft/trocr-small-printed`、`BAAI/bge-small-zh-v1.5`、Qwen 0.5B–4B Instruct。

许可先看 MIT / Apache-2.0 / BSD。CC-BY-NC、Llama 社区许可只标「仅测试」。

---

## setup

```bash
mkdir -p /workspace/hf-lab/{models,cache,data,runs,reports,bin}
python3 -m pip install -U huggingface_hub safetensors
# 探测 CPU/内存/磁盘/GPU，写 reports/machine.json
# 检查环境变量 HF_TOKEN，有/无 只报状态，不打印 token
```

没有 token：停。让辉哥去 https://huggingface.co/settings/tokens 建 **Read**，在云电脑写入环境变量，不要贴进对话长期保存。

---

## pull

```bash
python3 - <<'PY'
import os
from huggingface_hub import HfApi, snapshot_download
repo = os.environ["HF_REPO"]          # 例 Qwen/Qwen2.5-0.5B-Instruct
cap_gb = float(os.environ.get("HF_CAP_GB", "8"))
api = HfApi(token=os.environ.get("HF_TOKEN"))
info = api.repo_info(repo, repo_type="model", files_metadata=True)
size = sum((s.size or 0) for s in (info.siblings or [])) / 1024**3
if size > cap_gb:
    raise SystemExit(f"{repo} {size:.2f}GB over cap {cap_gb}")
print("size_gb", round(size, 3))
snapshot_download(repo_id=repo, local_dir=f"/workspace/hf-lab/models/{repo.replace('/', '__')}", token=os.environ.get("HF_TOKEN"))
PY
```

gated / 401 / 403：停。让辉哥在浏览器打开模型页接受协议，再重试。

---

## smoke

- 检测 / OCR：`data/` 里 1 张图
- LLM：中英各 1 句，max_new_tokens=64
- 超 60 秒：标「只能批量实验，不能实时」
- 写 `runs/smoke-<slug>/summary.md`

---

## experiment

辉哥要补 brief，缺项就问，不要自衡：

- 目标（一句）
- 任务：detect / ocr / classify / embed / llm-smoke
- 样本路径与数量
- 通过线
- 时间预算（默认 30 分）
- allow_paid_hf_inference: no

报告必有：模型 id + 许可、硬件快照、数字、3 个失败例、keep / drop / needs-GPU、下一句只要辉哥说什么。

产出只落 `/workspace/hf-lab` 和 2T `Agent文件`。不要写 Mini 系统盘。

---

## 给编程 Bot 的启动句

你现在按 `skills/hf-cloud-lab.md` 做 setup。探测机器、检查 HF_TOKEN 有没有、建 `/workspace/hf-lab`。不下 8GB 以上模型，不拉 14B/70B，不微调，不打印 token。用中文回：机器配置、token 有无、路径、下一句我说什么。不要自行展开实验。

之后可直接说：
- `拉 Qwen/Qwen2.5-0.5B-Instruct 做 smoke`
- `拉一个最小检测模型，先不要动店里照片`
- `用 /workspace/hf-lab/data/brake 做实验，brief 我补`

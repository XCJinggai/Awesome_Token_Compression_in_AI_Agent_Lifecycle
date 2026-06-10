# Paper Table 维护规范

## 日期规则

- **日期以 arXiv 第一个版本（v1）的提交时间为准**
- 有些论文会发多个版本（v1, v2, ...），不要用最新版本的时间
- 格式：`YYYY`（年份）
- 如果论文未发布到 arXiv，以最早公开发布时间为准

## 排序规则

- **各子分类表格内，按 arXiv 第一版（v1）发布时间降序排列**，越新的越靠上
- arXiv ID 格式：`YYMM.NNNNN`，前四位 YYMM 代表年月
- **先按年月降序**：2603（2026年3月）> 2602（2026年2月）> 2510（2025年10月）
- **同一年月内**再按后面的序号降序：2602.23235 > 2602.18846 > 2602.04804
- ⚠️ 不是纯字符串排序！2603.01143 比 2602.23235 新，因为 3月 > 2月

---

## 分类体系

本仓库基于以下 **智能体为中心的分类体系**：

### 一级分类（Category）

| Badge | 含义 |
|---|---|
| `[![Category](https://img.shields.io/badge/Perception-cyan)]()` | 感知压缩：作用于输入侧感知 token（文本/图像/视频/音频） |
| `[![Category](https://img.shields.io/badge/Semantic-yellow)]()` | 语义压缩：作用于智能体执行过程中积累的工作流上下文 token |

### 二级分类（Modality / Context）

**感知压缩子类（紫色 purple）：**
- `Text` — 文本 token 压缩
- `Image` — 图像 token 压缩
- `Video` — 视频 token 压缩
- `Audio` — 音频 token 压缩

**语义压缩子类：**
- `Observation`（橙色 orange）— 环境观察/工具反馈的 token 压缩
- `Retrieval`（青色 teal）— 检索增强生成中证据的 token 压缩
- `Memory`（紫罗兰色 blueviolet）— 长期记忆系统的 token 压缩

### 方法范式（Method，浅灰 lightgrey）

| 方法 | 说明 |
|---|---|
| `Selection` | 基于显著性/冗余度/多样性/任务相关性保留有信息量的 token |
| `Aggregation` | 将冗余或相关 token 合并为紧凑的代表性表示 |
| `Resampling` | 将原始 token 映射为一组新构建的紧凑表示（如软 token、查询 token） |
| `Transformation` | 通过结构性操作（卷积、池化、像素重排等）降低 token 数量 |
| `Tokenizer` | 在 tokenizer/codec 设计阶段即进行压缩（主要用于音频） |

---

## Tag 规则

### 来源 Badge（放在标题链接前）

- 已发表：`[![PDF](https://img.shields.io/badge/会议名-年份-blue)](链接)`
  - 例如：`[![PDF](https://img.shields.io/badge/CVPR-2025-blue)]()`、`[![PDF](https://img.shields.io/badge/NeurIPS-2024-blue)]()`
  - 会议名中的空格用下划线替代：`Findings_of_ACL`、`ICLR`、`EMNLP`
- 仅 arXiv：`[![arXiv](https://img.shields.io/badge/arXiv-年份-red)](arXiv链接)`
- ⚠️ **标注会议必须反复确认！** 只有明确公开录用信息的才能标会议 badge，否则一律标 arXiv。不要给别人"手动中稿"

### Category Badge（cyan/yellow）

```markdown
[![Category](https://img.shields.io/badge/Perception-cyan)]()
[![Category](https://img.shields.io/badge/Semantic-yellow)]()
```

### Modality Badge（purple/orange/teal/blueviolet）

```markdown
# 感知压缩子类（purple）
[![Modality](https://img.shields.io/badge/Text-purple)]()
[![Modality](https://img.shields.io/badge/Image-purple)]()
[![Modality](https://img.shields.io/badge/Video-purple)]()
[![Modality](https://img.shields.io/badge/Audio-purple)]()

# 语义压缩子类
[![Modality](https://img.shields.io/badge/Observation-orange)]()
[![Modality](https://img.shields.io/badge/Retrieval-teal)]()
[![Modality](https://img.shields.io/badge/Memory-blueviolet)]()
```

### Method Badge（lightgrey）

```markdown
[![Method](https://img.shields.io/badge/Selection-lightgrey)]()
[![Method](https://img.shields.io/badge/Aggregation-lightgrey)]()
[![Method](https://img.shields.io/badge/Resampling-lightgrey)]()
[![Method](https://img.shields.io/badge/Transformation-lightgrey)]()
[![Method](https://img.shields.io/badge/Tokenizer-lightgrey)]()
```

---

## 表格行格式

```markdown
| [![arXiv](https://img.shields.io/badge/arXiv-2025-red)](arXiv链接)<br>[论文标题](arXiv链接)<br>作者 | 2025 | [arXiv](arXiv链接) | [![Category](https://img.shields.io/badge/Perception-cyan)]() [![Modality](https://img.shields.io/badge/Image-purple)]() | [![Method](https://img.shields.io/badge/Selection-lightgrey)]() |
```

- `Title & Authors` 列：来源 badge + 换行 + 标题链接 + 换行 + 作者
- `Year` 列：四位年份
- `Links` 列：arXiv 链接 / Paper 链接；无链接填 `-`
- `Category & Modality` 列：Category badge + Modality badge
- `Method` 列：Method badge；不确定填 `-`

### 作者格式

- 作者 ≤ 2 人：`Zhang and Li`
- 作者 > 2 人：第一作者 + `et al.`（如 `Zhang et al.`）

---

## 如何添加新论文

1. 确定论文属于哪个子分类（感知/语义 × 模态/上下文类型 × 方法范式）
2. 找到对应的子表格，按日期降序插入新行
3. 确认 arXiv ID、作者名、年份信息
4. 如有 GitHub 仓库，可在 Links 列额外添加 `[GitHub](链接)`
5. 提交 Pull Request

---

## 其他

- 没有链接的论文 Links 列填 `-`
- 没有方法标签的论文 Method 列填 `-`
- GitHub Stars badge 可选：`[![Star](https://img.shields.io/github/stars/org/repo.svg?style=social&label=Star)](repo链接)`

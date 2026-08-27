# tracing-research-lineages

> 面向 Codex 的学术论文研究谱系分析 Skill。

英文版本：[README.en.md](README.en.md)

## 功能介绍

`tracing-research-lineages` 用于分析一篇学术论文的研究问题、核心主张、实验验证和研究发展脉络。它把论文视为一个“承载主张的研究证据单元”，而不是孤立的引用节点，帮助用户回答以下问题：

| 能力 | 说明 |
| --- | --- |
| 论文解析 | 提取研究问题、核心主张、方法和实验设置 |
| 主张—实验映射 | 将主要主张与数据、模型、基线、指标和结果对应起来 |
| 研究方向收窄 | 用“对象 + 机制/现象 + 目的”定义可检索的窄方向，并列出同义词和排除项 |
| 谱系检索 | 结合概念检索、后向引用和前向引用寻找潜在前驱与后续工作 |
| 核心/邻近工作筛选 | 区分真正构成研究主线的论文与仅有主题相似的论文 |
| 时间线重建 | 按最早可验证的公开日期排序，合并预印本、会议版、期刊版和修订版 |
| 创新比较 | 对每篇核心论文说明继承基础、既有限制、新增贡献和关系类型 |
| 不确定性报告 | 区分直接证据、分析推断和证据不足，避免无依据地声称覆盖完整 |

## 分析流程

1. 根据可获得的全文、摘要和元数据判定证据等级：`A`、`B` 或 `C`。
2. 提取目标论文的研究问题、核心主张及其对应的实验验证。
3. 建立窄方向抽象，明确研究对象、机制/现象、目的、同义词和排除项。
4. 先按概念检索候选论文，再通过后向引用和前向引用扩展候选集。
5. 筛选核心谱系论文，将宽泛、相似、综述、基准或应用型工作放入邻近工作。
6. 按最早可验证的公开日期重建时间线，并单独记录正式发表信息。
7. 比较每个谱系节点相对于前序工作的继承基础、限制和新增量。
8. 输出带有证据等级、引用、分析推断、搜索截止时间和局限性的结构化报告。

## 输出结构

最终报告按以下九个部分组织，章节名称与 `references/output-template.md` 保持一致：

1. `Paper Metadata`
2. `One-Sentence Synthesis`
3. `Research Problem and Core Claims`
4. `Claim-Experiment Validation Matrix`
5. `Narrow Direction`
6. `Search Scope`
7. `Core Timeline`
8. `Adjacent Work`
9. `Development Lineage`

## 使用方式

安装后，在 Codex 中使用 Skill 名称调用：

```text
$tracing-research-lineages
```

推荐的请求格式：

```text
Use $tracing-research-lineages to analyze this paper and trace its research lineage.

Paper: <paper title, URL, uploaded file, or identifier>
Focus: <optional research direction, method, dataset, or claim>
Cutoff: <optional search cutoff date>
```

也可以直接说明希望分析的论文、研究方向或比较范围。若提供论文全文、可靠元数据和可访问的引用信息，谱系判断通常会更稳健。

## 部署指南

本项目是 Codex Skill，不是独立运行的 Web 服务。仓库没有 Node.js、Python、数据库、端口或 Docker 运行时要求；部署的含义是把 Skill 目录放到 Codex 可发现的 Skill 路径中。

### 方式一：本地安装到 Codex（推荐）

#### PowerShell

在仓库根目录执行：

```powershell
$skillRoot = if ($env:CODEX_HOME) {
  Join-Path $env:CODEX_HOME 'skills'
} else {
  Join-Path $env:USERPROFILE '.codex\skills'
}
$targetDir = Join-Path $skillRoot 'tracing-research-lineages'

New-Item -ItemType Directory -Force -Path $targetDir | Out-Null
Copy-Item -Path .\SKILL.md, .\README.md, .\README.en.md, .\agents, .\references `
  -Destination $targetDir -Recurse -Force
```

#### macOS / Linux

在仓库根目录执行：

```bash
skill_root="${CODEX_HOME:-$HOME/.codex}/skills"
target_dir="$skill_root/tracing-research-lineages"

mkdir -p "$target_dir"
cp SKILL.md README.md README.en.md "$target_dir/"
cp -R agents references "$target_dir/"
```

安装后重启 Codex 或新建会话，使 Skill 重新被发现。可以用下面的命令检查关键文件是否存在：

```powershell
Test-Path (Join-Path $targetDir 'SKILL.md')
Test-Path (Join-Path $targetDir 'references\research-protocol.md')
Test-Path (Join-Path $targetDir 'references\output-template.md')
```

macOS / Linux 可以使用：

```bash
test -f "$target_dir/SKILL.md"
test -f "$target_dir/references/research-protocol.md"
test -f "$target_dir/references/output-template.md"
```

然后在 Codex 中使用 `$tracing-research-lineages` 调用。

#### 更新本地安装

拉取或切换到新版本后，在仓库根目录重新执行对应平台的复制命令即可。更新时请保留以下结构，尤其不要遗漏 `references` 目录：

```text
tracing-research-lineages/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── research-protocol.md
    └── output-template.md
```

### 方式二：上传到 OpenAI Skills API（可选）

如果需要将 Skill 作为 API Skill 资源管理，可以将 Skill 文件打包为 ZIP，再通过 Skills API 上传。官方接口支持上传 Skill 目录或单个 ZIP 文件，详见 [Create a new skill](https://developers.openai.com/api/reference/python/resources/skills/methods/create)。

打包示例：

```powershell
Compress-Archive -Path SKILL.md, agents, references `
  -DestinationPath tracing-research-lineages.zip -Force
```

使用 Python SDK 上传：

```python
from openai import OpenAI

client = OpenAI()

with open("tracing-research-lineages.zip", "rb") as bundle:
    skill = client.skills.create(files=bundle)

print(skill.id)
```

该方式需要配置 `OPENAI_API_KEY` 并安装对应版本的 OpenAI Python SDK；对本地 Codex 使用者而言不是必需步骤。

## 项目结构

```text
tracing-research-lineages/
├── SKILL.md                         # Skill 主说明与分析流程
├── agents/
│   └── openai.yaml                  # Codex UI 展示信息与默认调用提示
├── references/
│   ├── research-protocol.md         # 证据、检索、筛选和时间线协议
│   └── output-template.md           # 结构化报告模板
├── README.md                        # 中文说明
└── README.en.md                     # English documentation
```

## 证据与使用限制

- 优先使用论文全文和已核验的元数据；只有摘要或二手来源时，会降低结论强度并显式说明。
- 研究谱系不是简单的相似论文列表。只有在原始记录中看到引用、明确动机、复用设置或延续说明时，才使用 `direct` 或 `continuation` 等强关系标签。
- 时间线以最早可验证的公开版本为排序依据，正式发表信息单独列出；存在日期冲突时应显式标注。
- “没有找到前驱”不等于“没有前驱”。搜索结果受全文可访问性、检索来源、查询词和截止日期限制。
- 当无法完成外部检索或引用链分析时，报告应明确说明降级模式和覆盖边界。

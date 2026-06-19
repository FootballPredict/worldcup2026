# 2026世界杯预测助手（Agent Skill）

一个纯提示词驱动的 [Agent Skill](https://www.anthropic.com/news/skills)，用于预测和解答2026年FIFA世界杯相关问题。无需代码：通过因素清单推理、提问时实时联网查询当前球队评分，以简洁美观、诚实的概率格式回答。

`SKILL.md` 是入口；`references/` 下的文件按需加载。

## 能问什么
- 「预测美国vs澳大利亚」/ 「西班牙vs巴西比分预测」
- 「谁会赢得2026世界杯？」/ 「摩洛哥能走多远？」
- 「墨西哥能出小组赛吗？」
- 「2026世界杯在哪里举办？」（主办方、赛制、日期、场地、名额）

## 安装

Skill 就是本仓库根目录（`SKILL.md` 在根部）。安装即把它放入你的工具能发现 skill 的目录。按你使用的工具选择对应步骤。

### Codex CLI
Skill 从 `$CODEX_HOME/skills` 自动发现（默认 `~/.codex/skills`）。

```bash
# 克隆仓库后，将整个目录作为 skill 文件夹复制进去
git clone https://github.com/FootballPredict/worldcup2026.git worldcup-2026-predictor
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R worldcup-2026-predictor "${CODEX_HOME:-$HOME/.codex}/skills/"
```

启动 Codex 后用 `$worldcup-2026-predictor` 触发，或直接提世界杯相关问题让它自动识别。

### Claude Code
Claude Code 从 `~/.claude/skills`（用户级）或 `.claude/skills`（项目级）发现 skill。

```bash
git clone https://github.com/FootballPredict/worldcup2026.git worldcup-2026-predictor
mkdir -p ~/.claude/skills
cp -R worldcup-2026-predictor ~/.claude/skills/
```

重启 Claude Code（或重新加载项目），skill 出现在 `/skills` 列表中。

### Claude.ai 及 Anthropic API（zip上传）
接受 zip 上传的工具（Claude.ai Skills UI、Agent Skills API）要求 `SKILL.md` 在压缩包根部。

```bash
git clone https://github.com/FootballPredict/worldcup2026.git
cd worldcup2026
zip -r worldcup-2026-predictor.zip . -x '*.git*' -x '*.DS_Store'
```

在工具的「添加skill」/「上传skill」流程中上传 `worldcup-2026-predictor.zip`。

### 其他兼容 Agent Skills 的工具
本 skill 遵循标准布局（`SKILL.md` 在根目录 + 可选 `references/`）。通用安装步骤：

1. 获取仓库：克隆或下载整个仓库目录。
2. 将该目录复制到工具的 skills 目录中。
3. 重新加载工具使其重新扫描 skills。
4. 确认 skill 出现（通常在 `/skills` 或 skills 列表），按名称触发。

无需构建、无依赖、无需网络密钥即可安装。Skill 仅在运行时需要网络，用于获取最新球队评分。

## 更新
```bash
cd worldcup-2026-predictor && git pull
cp -R . "${CODEX_HOME:-$HOME/.codex}/skills/worldcup-2026-predictor/"  # 按工具调整目标路径
```

## 卸载
从工具的 skills 目录中删除对应文件夹：
```bash
rm -rf "${CODEX_HOME:-$HOME/.codex}/skills/worldcup-2026-predictor"
```

## 文件结构
```text
（仓库根目录）
├── SKILL.md                    入口：触发条件 + 推理工作流
├── LICENSE                     MIT 开源协议
├── agents/openai.yaml          UI元数据（显示名称、默认提示词）
└── references/
    ├── 分析框架.md             因素清单、结果锚点、比分启发式
    ├── 实力评分指引.md         如何实时搜索当前球队评分并映射档位
    ├── 回复风格.md             单场/整届/资讯三类回答模板
    └── 赛事资讯2026.md         已确认的2026赛制、主办方、日期、场地、名额
```

## 开源协议
MIT，详见 [LICENSE](LICENSE)。

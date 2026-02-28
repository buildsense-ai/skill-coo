# skill-coo

COO（首席运营官）Skill — 团队信息中枢。让信息流动、决策不卡住。

不是秘书，不是看板工具。是一个有判断力的信息中枢：汇聚信息、路由问题、追踪进展、推动决策。

可挂载到任何支持 SKILL.md 协议的 agent 框架（小八、Claude Code 等）。

## 核心能力

- **align** — 收集信息，更新团队对齐状态，交叉比对发现断档
- **report** — 生成带判断的状态报告（不是清单）
- **propose** — 记录超出 COO 权限的待决策提案
- **route** — 发现问题，判断该谁管，推过去并附上判断
- **patrol** — 主动巡检 GitHub / agent logs / stale 状态

## 信息来源

1. **GitHub** — commits、PR、issues（通过 `gh` CLI）
2. **本地 Agent Logs** — agent 工作日志（路径配置在 sources.json）
3. **人类对话** — 随时说一句，COO 提取并持久化

## 安装

```bash
cd your-agent-project/skills
git clone https://github.com/buildsense-ai/skill-coo.git coo
```

初始化数据文件：

```bash
cd coo
for f in *.example.json; do cp "$f" "data/${f%.example.json}.json"; done
mkdir -p data
```

## 目录结构

```
├── SKILL.md                  # Skill 定义（核心 prompt）
├── *.example.json            # 数据模板
└── data/                     # 运行时数据（git ignored）
    ├── alignment.json        # 团队对齐状态
    ├── members.json          # 成员档案
    ├── proposals.json        # 待决策提案池
    ├── sources.json          # 信息源配置
    └── inbox.json            # 待处理事项队列
```

## 依赖

- bash + 文件读写能力
- `gh` CLI（GitHub 巡检用，可选）

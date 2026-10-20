# AWS Well-Architected Assessment Skill

一个用于辅助评估 AWS 环境的 Agent Skill。它依据 [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html) 的六大支柱，指导 Agent 发现资源、执行检查、整理风险并给出改进建议。

> 本仓库提供的是 **Skill 指令和 Markdown 检查规则**，不是可独立运行的扫描器。实际评估需要支持 Skill 的 Agent、有效的 AWS 凭证，以及相应的只读 API 权限。

## 功能

- 按运营卓越、安全性、可靠性、性能效率、成本优化和可持续性六大支柱组织评估。
- 提供 25 份 AWS 服务检查规则，覆盖 EC2、S3、RDS、IAM、Lambda、EKS、VPC、CloudFront、WAF 等服务。
- 按高风险、中风险和改进机会对发现进行分级，并映射到相关支柱。
- 生成资源概览、服务检查结果、支柱分析和整改建议。
- 支持指定服务、支柱和 AWS Region；可选择性地辅助整理 AWS Well-Architected Tool 的填写内容。

## 目录结构

```text
aws-well-architected-assessment/
├── SKILL.md                       # Skill 入口与评估工作流
├── references/
│   ├── pillar-*.md                # 六大支柱的评估参考
│   ├── severity-matrix.md         # 严重程度与评分规则
│   └── service-checks/
│       └── *-checks.md            # 各 AWS 服务的检查项
└── README.md
```

## 安装

将整个目录放到支持 Skill 的 Agent （codex,claude code, kiro etc..）的技能目录中。以 Codex 的本地技能目录为例：

```bash
git clone <本仓库的 GitHub 地址>
cp -R aws-well-architected-assessment ~/.codex/skills/
```

安装后，确认 `~/.codex/skills/aws-well-architected-assessment/SKILL.md` 存在，并重新启动或刷新 Agent 会话。若使用其他 Agent，请按该产品的 Skill 安装方式放置目录。

## 前置条件

1. 配置可访问目标 AWS 账户的凭证，并确认目标 Region。
2. 为评估身份授予所选服务的 `List*`、`Describe*`、`Get*` 等必要只读权限。具体权限取决于评估范围；权限不足的检查应标记为“未评估”，而不是“通过”。
3. 在正式评估前，确认要扫描的账户、Region、服务和支柱。跨 Region 评估会产生更多 API 调用。

## 使用示例

在已加载此 Skill 的 Agent 中输入：

```text
请使用 aws-well-architected-assessment 评估当前 AWS 账户在
ap-southeast-1 的安全性和可靠性，先展示资源发现结果，再执行检查。
请区分“通过”“发现问题”和“因权限不足而未评估”的项目。
```

也可以要求完整评估：

```text
请按六大支柱评估当前账户中发现的服务，输出按严重程度排序的发现、
对应资源、证据、整改建议和各支柱评分。不要修改任何 AWS 资源。
```

Skill 的工作流依次为：确定范围 → 发现资源 → 加载服务检查规则 → 映射六大支柱 → 生成报告 → 提供整改建议。评分方法见 [`references/severity-matrix.md`](references/severity-matrix.md)。

## 安全与局限

- 设计目标是**只读评估**；不会自动修改 AWS 资源，也不会自动执行整改。
- 结果取决于扫描范围、IAM 权限及检查时的环境状态，不应把未发现的问题视为不存在。
- 风险等级和建议需要结合业务场景人工复核；本 Skill 不等同于 AWS 官方 Well-Architected Review 或合规认证。
- 不要将 AWS 凭证、账户资源清单或包含敏感信息的评估报告提交到公开仓库。

## 参考资料

- [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html)
- [service-screener-v2](https://github.com/aws-samples/service-screener-v2)（评估思路参考）

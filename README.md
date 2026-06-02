# tender-search

知了标讯全网招中标数据查询与分析 Skill。把本仓库安装到支持 Skill 的 AI 编程助手后，助手可以按自然语言调用知了标讯 API，完成招标/中标公告检索、企业招投标画像、竞争对手分析、潜在供应商推荐、市场统计、品牌价格趋势等任务。

## 适用场景

- 查询招标公告、中标公告、采购意向、合同公告等标讯数据
- 搜索临期或即将到期的周期性项目，挖掘续约商机
- 分析某公司的历史中标、采购项目、主营业务和合作客户
- 查找竞争对手、潜在投标供应商、Top 采购单位、Top 中标单位
- 按行业、地区、月份、季度、品牌等维度做招投标市场分析
- 查询品牌型号的历史中标单价和价格趋势

## 能力概览

本 Skill 内置 16 个知了标讯数据工具的调用说明：

| 分类 | 能力 |
| --- | --- |
| 标讯搜索 | 常规搜索、高级组合搜索、公告详情、临期项目 |
| 企业分析 | 公司搜索、公司画像、主营业务、合作客户/供应商、联系人、竞争对手、潜在供应商 |
| 市场分析 | Top 采购单位、Top 中标单位、Top 品牌、多维统计、价格趋势 |

详细参数见 `references/` 目录：

- `references/api-search.md`：标讯搜索类接口
- `references/api-company.md`：企业分析类接口
- `references/api-market.md`：市场分析类接口
- `references/auto-register.md`：首次使用自动注册流程

## 安装

将本仓库放到你的 AI 助手 Skill 目录中即可。

### Claude Code

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/liu-jiapeng/tender-search.git ~/.claude/skills/tender-search
```

### Codex

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/liu-jiapeng/tender-search.git ~/.codex/skills/tender-search
```

如果你的客户端使用其他 Skill 目录，请将仓库克隆到对应目录，并确保目录内包含 `SKILL.md`。

## API Key 配置

Skill 会按以下优先级读取 API Key：

1. 环境变量 `ZLBX_API_KEY`
2. 本地配置文件 `~/.zlbx/config.json` 中的 `api_key`
3. 如果以上都没有配置，Skill 会自动注册设备账号并写入 `~/.zlbx/config.json`

手动配置示例：

```bash
export ZLBX_API_KEY="zlbx_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

或写入本地配置：

```json
{
  "api_key": "zlbx_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

首次自动注册的新设备账号会获得免费调用额度。额度用完后，助手会根据 Key 来源提示对应的登录或充值方式。

## 使用示例

安装后直接向助手提问即可。只要问题涉及招投标、采购、中标、供应商、竞争对手、市场分析等场景，助手会自动使用本 Skill。

```text
帮我查一下广东最近一个月关于服务器采购的招标项目
```

```text
分析科大讯飞近两年的中标业务方向和主要客户
```

```text
找一下智慧城市项目里最常见的中标供应商和采购单位
```

```text
查询联想 ThinkSystem SR650 在服务器项目里的历史中标价格
```

```text
帮我找北京 90 天内到期的物业管理项目
```

```text
分析华为和中兴在哪些项目里共同投标，竞争集中在哪些地区和产品
```

## 查询技巧

- 查某个采购单位发布的项目时，说清楚“采购方/招标方”，Skill 会使用采购单位匹配。
- 查某个供应商的中标情况时，说清楚“中标方/供应商”，Skill 会使用中标单位匹配。
- 需要更精确的结果时，可补充地区、时间范围、金额范围、公告阶段、排除词。
- 做市场分析时，可指定统计维度，例如“按月”“按省份”“按品牌”“同比/环比”。
- 搜索具体产品时，可把品牌、型号、品类分开描述，便于后续价格和品牌分析。

## 隐私说明

自动注册仅在用户未配置 `ZLBX_API_KEY` 且本地没有 `~/.zlbx/config.json` 时触发。注册时会采集设备基础特征用于生成设备账号，其中 MAC 地址会先做 SHA256 哈希，不会上传明文 MAC。

API Key 默认保存在本机 `~/.zlbx/config.json`。请勿把该文件提交到 GitHub。

## 目录结构

```text
tender-search/
├── SKILL.md
├── README.md
└── references/
    ├── api-search.md
    ├── api-company.md
    ├── api-market.md
    └── auto-register.md
```

## 常见问题

### 为什么助手没有使用这个 Skill？

确认仓库已放到客户端识别的 Skill 目录，并重启或刷新客户端。不同客户端的 Skill 加载目录可能不同，请以你的客户端文档为准。

### 没有 API Key 能用吗？

可以。未检测到环境变量和本地配置时，Skill 会自动注册设备账号并使用免费额度。

### 如何更换 API Key？

优先推荐设置环境变量 `ZLBX_API_KEY`。也可以修改 `~/.zlbx/config.json` 中的 `api_key` 字段。

### 查询结果不够精准怎么办？

补充匹配角色和筛选条件，例如“作为采购方”“作为中标方”“只看广东”“排除维保/耗材”“只看 2025 年以来”“金额 100 万以上”。

## License

本项目授权方式以仓库中的 `LICENSE` 文件为准。如仓库暂未提供 `LICENSE`，请联系维护者确认使用范围。

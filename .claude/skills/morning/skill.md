---
name: morning
description: 生成晨间简报，收集 AI/政务/巨头动态，输出结构化报告。Use when user says "/morning", "/brief", "早报", "晨报", or asks for daily news briefing.
---

# Morning Skill

生成晨间简报，聚合多源 RSS 信息，输出结构化的每日动态报告。

## When to Use

- 用户说 "/morning", "/brief", "早报", "晨报"
- 需要获取最新的 AI/政务/技术动态
- 生成每日信息摘要

## Output

```
10_Daily/YYYY/
└── YYYY-MM-DD_brief.md

60_Resources/Newsletters/YYYY-MM/
└── YYYY-MM-DD-digest.md  (cache)
```

## Fetch Strategy

| Category | Priority Order | Limit |
|----------|---------------|-------|
| AI & Agent | P0 > P1 > P2 | TOP 10 |
| GovTech / 政务 | - | TOP 3 |
| Big Tech | P1 > P2 | TOP 5 |
| 互联网资讯 | P1 > P2 | TOP 5 |
| 奇思妙想 | P2 | TOP 3 |
| 技术团队与安全 | P1 | TOP 4 |
| 产品与架构 | P2 | TOP 2 |

Time Window: 仅抓取发布时间在过去 24 小时内的内容。

## RSS Sources

### AI Sources

#### P0 (Core)
| Name | URL |
|------|-----|
| OpenAI | https://openai.com/blog/rss |
| Anthropic | https://www.anthropic.com/rss |
| TLDR AI | https://bullrich.dev/tldr-rss/ai.rss |

#### P1 (Important)
| Name | URL |
|------|-----|
| The Rundown AI | https://rss.beehiiv.com/feeds/2R3C6Bt5wj.xml |
| Google AI | https://ai.googleblog.com/feeds/posts/default |
| Microsoft AI | https://blogs.microsoft.com/ai/feed/ |

#### P2 (Extended)
| Name | URL | Enabled |
|------|-----|---------|
| Meta AI | https://about.meta.com/rss/meta-ai/ | true |
| Apple AI | https://machinelearning.apple.com/rss | true |
| AI Weekly | https://aiweekly.co/rss.xml | true |
| Import AI | https://jack-clark.net/rss/ | false |
| Algorithm | https://www.technologyreview.com/feed/ | false |

### GovTech Sources

| Name | URL |
|------|-----|
| 国务院 | https://www.gov.cn/rss/gov.xml |
| 国家政策法规 | https://www.gov.cn/rss/gov.xml |

### BigTech Sources

#### P1
| Name | URL |
|------|-----|
| GitHub | https://github.com/github/roadmap/issues.atom |
| AWS News | https://aws.amazon.com/new/feeds/current.xml |
| Google Cloud | https://cloud.google.com/blog/rss |

#### P2
| Name | URL |
|------|-----|
| Azure | https://azure.microsoft.com/updates/feed/ |
| Meta Engineering | https://engineering.fb.com/?format=RSS |
| Netflix Tech | https://netflixtechblog.com/feed |

### 互联网资讯 Sources（前端科技/电子硬件/手机应用）

| Name | URL |
|------|-----|
| 36kr | https://rss.aishort.top/?type=36kr |
| 虎嗅网 | https://rss.aishort.top/?type=huxiu |
| 艾瑞网 | https://rss.aishort.top/?type=iresearch |
| 爱范儿 | https://rss.aishort.top/?type=AppSolution |
| 效率火箭 | https://rss.aishort.top/?type=xlrocket |

### 奇思妙想 Sources

| Name | URL |
|------|-----|
| 果壳网 | https://rss.aishort.top/?type=guokr |
| 少数派 | https://rss.aishort.top/?type=sspai |
| 知乎想法热榜 | https://rss.aishort.top/?type=zhihu |

### 技术团队与安全 Sources

| Name | URL |
|------|-----|
| 美团技术团队 | https://tech.meituan.com/feed |
| 掘金专栏-字节跳动技术团队 | https://rsshub.app/juejin/posts/1838039172387262 |
| 有赞技术团队 | https://tech.youzan.com/rss/ |
| 360 核心安全技术博客 | https://blogs.360.net/rss.html |

### 产品与架构 Sources

| Name | URL |
|------|-----|
| 人人都是产品经理 | https://plink.anyfeeder.com/weixin/woshipm |
| 架构师之路 | https://plink.anyfeeder.com/weixin/gh_10a6b96351a9 |

## Report Sections

1. **AI & Agent** (Top 10)
2. **GovTech / 政务服务** (Top 3)
3. **Big Tech Moves** (Top 5)
4. **互联网资讯** (Top 5)
5. **奇思妙想** (Top 3)
6. **技术团队与安全** (Top 4)
7. **产品与架构** (Top 2)
8. **Opportunities** (最多 5 条)
9. **Watchlist**

## Output Format

每条动态必须包含：
- **结论**: 一句话总结
- **影响**: 对业务/技术的影响
- **行动建议**: 建议采取的行动
- **原文链接**: 必须使用 Markdown 格式 `[标题](https://...)`

## Constraints

- 输出必须是结论 + 影响 + 行动建议 + 原文链接
- 原文链接缺失的条目不进入正式输出
- AI 取 TOP 10，GovTech 取 TOP 3，BigTech 取 TOP 5
- 互联网资讯取 TOP 5，奇思妙想取 TOP 3
- 技术团队与安全取 TOP 4，产品与架构取 TOP 2
- 仅纳入过去 24 小时内发布的内容
- 抓取后必须按 URL 去重；同 URL 仅保留一条
- **禁止创建任务**
- **禁止修改状态**
- 机会点建议先进入 Inbox

## Cache

缓存文件存储在 `60_Resources/Newsletters/YYYY-MM/YYYY-MM-DD-digest.md`，避免重复抓取。

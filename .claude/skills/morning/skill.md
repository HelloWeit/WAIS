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

## Report Sections

1. **AI & Agent** (Top 10)
2. **GovTech / 政务服务** (Top 3)
3. **Big Tech Moves** (Top 5)
4. **Opportunities** (最多 5 条)
5. **Watchlist**

## Output Format

每条动态必须包含：
- **结论**: 一句话总结
- **影响**: 对业务/技术的影响
- **行动建议**: 建议采取的行动

## Constraints

- 输出必须是结论 + 影响 + 行动建议
- AI 取 TOP 10，GovTech 取 TOP 3，BigTech 取 TOP 5
- **禁止创建任务**
- **禁止修改状态**
- 机会点建议先进入 Inbox

## Cache

缓存文件存储在 `60_Resources/Newsletters/YYYY-MM/YYYY-MM-DD-digest.md`，避免重复抓取。

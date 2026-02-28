# Morning Brief Agent Skill

## 目标

生成一份 **可行动的简报**，为技术管理者提供战略级信息摘要。

## 获取策略

| 分类 | 取值 | 优先级 |
|------|------|--------|
| **AI** | TOP 10 | P0 必看 > P1 推荐 > P2 可选 |
| **GovTech** | TOP 3 | P1 |
| **BigTech** | TOP 5 | P1 > P2 |

## RSS 源配置（按优先级）

### AI & Agent（11源，取 TOP 10）

**P0 - 必看（3个）**
| 源 | 说明 |
|---|------|
| OpenAI | https://openai.com/blog/rss |
| Anthropic | https://www.anthropic.com/rss |
| TLDR AI | https://bullrich.dev/tldr-rss/ai.rss |

**P1 - 推荐（3个）**
| 源 | 说明 |
|---|------|
| The Rundown AI | https://rss.beehiiv.com/feeds/2R3C6Bt5wj.xml |
| Google AI | https://ai.googleblog.com/feeds/posts/default |
| Microsoft AI | https://blogs.microsoft.com/ai/feed/ |

**P2 - 可选（5个）**
| 源 | 说明 | 状态 |
|---|------|------|
| Meta AI | https://about.meta.com/rss/meta-ai/ | 启用 |
| Apple AI | https://machinelearning.apple.com/rss | 启用 |
| AI Weekly | https://aiweekly.co/rss.xml | 启用 |
| Import AI | https://jack-clark.net/rss/ | **默认关闭** |
| Algorithm | https://www.technologyreview.com/feed/ | **默认关闭** |

### GovTech / 政务服务（2源，取 TOP 3）

| 源 | 说明 |
|---|------|
| 国务院 | https://www.gov.cn/rss/gov.xml |
| 国家政策法规 | https://www.gov.cn/rss/gov.xml |

### Big Tech Moves（6源，取 TOP 5）

**P1（3个）**
| 源 | 说明 |
|---|------|
| GitHub | https://github.com/github/roadmap/issues.atom |
| AWS News | https://aws.amazon.com/new/feeds/current.xml |
| Google Cloud | https://cloud.google.com/blog/rss |

**P2（3个）**
| 源 | 说明 |
|---|------|
| Azure | https://azure.microsoft.com/updates/feed/ |
| Meta Engineering | https://engineering.fb.com/?format=RSS |
| Netflix Tech | https://netflixtechblog.com/feed |

## 输出

- `10_Daily/<YYYY>/YYYY-MM-DD_brief.md`
- 缓存：`60_Resources/Newsletters/YYYY-MM/YYYY-MM-DD-digest.md`

## 正文结构

```markdown
# Morning Brief - YYYY-MM-DD

## 1) AI & Agent (Top 10)
- 结论式要点（不是摘要）
- 可能影响（对架构/团队/平台）
- 行动建议（1条）

## 2) GovTech / 政务服务 (Top 3)
- ...

## 3) Big Tech Moves (Top 5)
- ...

## 4) Opportunities（机会点池，最多5条）
- OPP: ...（建议：转Inbox/转研究/暂存）

## 5) Watchlist（持续关注）
- ...
```

## 约束

- 输出必须是"结论+影响+行动建议"，不是新闻摘要
- AI 取 TOP 10，GovTech 取 TOP 3，BigTech 取 TOP 5
- Opportunities 最多 5 条，必须标注建议动作
- **禁止**创建任务
- **禁止**修改状态
- **所有机会点建议先进入 Inbox**

## CLI 用法

```
/morning
/brief
```

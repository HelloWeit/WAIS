# Morning Brief Agent Skill

## 目标

生成一份 **可行动的简报**，为技术管理者提供战略级信息摘要。

## 获取策略

| 分类 | 取值 | 优先级 |
|------|------|--------|
| **AI** | TOP 10 | P0 必看 > P1 推荐 > P2 可选 |
| **GovTech** | TOP 3 | P1 |
| **BigTech** | TOP 5 | P1 > P2 |
| **互联网资讯** | TOP 5 | P1 > P2 |
| **奇思妙想** | TOP 3 | P2 |
| **技术团队与安全** | TOP 4 | P1 |
| **产品与架构** | TOP 2 | P2 |

时间窗口：仅抓取过去 24 小时内发布的内容。

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

### 互联网资讯（5源，取 TOP 5）

| 源 | 说明 |
|---|------|
| 36kr | https://rss.aishort.top/?type=36kr |
| 虎嗅网 | https://rss.aishort.top/?type=huxiu |
| 艾瑞网 | https://rss.aishort.top/?type=iresearch |
| 爱范儿 | https://rss.aishort.top/?type=AppSolution |
| 效率火箭 | https://rss.aishort.top/?type=xlrocket |

### 奇思妙想（3源，取 TOP 3）

| 源 | 说明 |
|---|------|
| 果壳网 | https://rss.aishort.top/?type=guokr |
| 少数派 | https://rss.aishort.top/?type=sspai |
| 知乎想法热榜 | https://rss.aishort.top/?type=zhihu |

### 技术团队与安全（4源，取 TOP 4）

| 源 | 说明 |
|---|------|
| 美团技术团队 | https://tech.meituan.com/feed |
| 掘金专栏-字节跳动技术团队 | https://rsshub.app/juejin/posts/1838039172387262 |
| 有赞技术团队 | https://tech.youzan.com/rss/ |
| 360 核心安全技术博客 | https://blogs.360.net/rss.html |

### 产品与架构（2源，取 TOP 2）

| 源 | 说明 |
|---|------|
| 人人都是产品经理 | https://plink.anyfeeder.com/weixin/woshipm |
| 架构师之路 | https://plink.anyfeeder.com/weixin/gh_10a6b96351a9 |

## 输出

- `10_Daily/<YYYY>/YYYY-MM-DD_brief.md`
- 缓存：`60_Resources/Newsletters/YYYY-MM/YYYY-MM-DD-digest.md`

缓存文件为必选输出，必须在 `/morning` 结束时落盘。

## 正文结构

```markdown
# Morning Brief - YYYY-MM-DD

## 1) AI & Agent (Top 10)
- 结论式要点（不是摘要）
- 可能影响（对架构/团队/平台）
- 行动建议（1条）
- 原文链接（可点击，格式：`[标题](https://...)`）

## 2) GovTech / 政务服务 (Top 3)
- ...

## 3) Big Tech Moves (Top 5)
- ...

## 4) 互联网资讯 (Top 5)
- ...

## 5) 奇思妙想 (Top 3)
- ...

## 6) 技术团队与安全 (Top 4)
- ...

## 7) 产品与架构 (Top 2)
- ...

## 8) Opportunities（机会点池，最多5条）
- OPP: ...（建议：转Inbox/转研究/暂存）

## 9) Watchlist（持续关注）
- ...
```

## 约束

- 输出必须是"结论+影响+行动建议+原文链接"，不是新闻摘要
- 原文链接必须为 Markdown 链接；缺失链接的条目不进入正式输出
- AI 取 TOP 10，GovTech 取 TOP 3，BigTech 取 TOP 5
- 互联网资讯取 TOP 5，奇思妙想取 TOP 3
- 技术团队与安全取 TOP 4，产品与架构取 TOP 2
- 仅纳入过去 24 小时内发布的内容
- 抓取后按 URL 去重；同 URL 仅保留一条，避免重复摘要
- 必须创建/写入 `60_Resources/Newsletters/YYYY-MM/YYYY-MM-DD-digest.md`
- Opportunities 最多 5 条，必须标注建议动作
- **禁止**创建任务
- **禁止**修改状态
- **所有机会点建议先进入 Inbox**

## CLI 用法

```
/morning
/brief
```

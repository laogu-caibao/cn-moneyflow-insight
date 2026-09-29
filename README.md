# 资金流向解读

`laogu-moneyflow`

资金流向解读 skill：汇总北向资金、融资融券、龙虎榜、ETF 份额变化，输出中文资金行为解读。

## 一键安装

仓库地址（点击复制）：

`https://github.com/laogu-caibao/laogu-moneyflow`

**方式一：克隆**

```bash
git clone https://github.com/laogu-caibao/laogu-moneyflow.git
```

**方式二：下载 ZIP**

https://github.com/laogu-caibao/laogu-moneyflow/archive/refs/heads/main.zip

**导入使用**

- Claude Code / Muse：把仓库中的 `SKILL.md` 放到 `~/.claude/skills/laogu-moneyflow/` 下即可调用。
- 豆包智能体 / Workbuddy 等：按各平台的 skill 上传流程导入 `SKILL.md`。
- 一次装好全部 16 个：用 [laogu-mcp](https://github.com/laogu-caibao/laogu-mcp)，`uvx laogu-mcp` 一键安装。
## 文件结构

- `SKILL.md` — 主流程（平台中立）
- `references/sources.md` — 数据源与接口说明

## 解读维度

- 方向与强度：净流入/流出规模相对历史分位
- 资金性质：北向（外资偏好）/融资（杠杆情绪）/机构席位（中长线）/游资（短炒）
- 量价关系：资金与价格是否背离
- 板块轮动：资金在行业间的切换方向

## 说明

- 数据注明交易日期；盘中数据标注"盘中快照"
- 只描述资金行为与逻辑，不做买卖推荐

---
## 出品

**老谷拆财报** —— 以数据为刃，剖市场真相

- 抖音 / 微信视频号 / 今日头条 / 快手：搜索「老谷拆财报」
- 固定栏目：「价值投资之财报解读」（全网连载中）
- 本 skill 的方法论与账号内容同源：数据驱动、拆开看、不讲黑话

### 扫码关注

| 微信视频号 | 抖音 |
|---|---|
| ![视频号二维码](docs/qrcode-shipinhao.jpg) | ![抖音二维码](docs/qrcode-douyin.png) |
| 扫一扫，关注视频号 | 抖音号：gubaobao22 |

> 作者声明：个人观点，仅供参考，不构成投资建议。


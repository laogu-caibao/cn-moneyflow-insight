# 数据源（2026-09-29 实测修订，API 优先）

## 北向资金

**机制性说明**：2024年5月11日起沪深交易所调整沪深港通披露机制，北向不再披露实时成交额和日度净买入，改为收盘后披露成交总额及前十大成交证券。**任何"北向净流入/净买入"数字都不再存在**，老接口（如 `push2his.eastmoney.com/api/qt/kamt/get`）返回全零是预期行为，不是故障。

- 可用口径：北向成交总额及占两市成交额比、沪深股通前十大成交股（收盘后披露）
- 来源：东方财富北向资金栏目/同花顺快讯（搜索 `北向资金 成交额` + 日期），注明来源
- 个股级外资动向替代：龙虎榜"深沪股通专用席位"净买入（见下）

## 融资融券（T+1 披露，默认取 T-1 交易日数据）

东财 datacenter 个股级接口（2026-09-29 实测可用）：
```
https://datacenter-web.eastmoney.com/api/data/v1/get?reportName=RPTA_WEB_RZRQ_GGMX&columns=DATE,SCODE,RZYE,RZMRE,RZCHE,RQYE,RQMCL,RQCHL,RZRQYE&source=WEB&client=WEB
```
- 关键字段：`DATE`（日期）、`SCODE`（代码）、`RZYE`（融资余额）、`RZMRE`（融资买入额）、`RZCHE`（融资偿还额）、`RQYE`（融券余额）
- 融资净买入口径：`RZMRE − RZCHE`（当日融资买入额减偿还额）；或用融资余额环比，**必须注明所用口径**
- 按个股查：加 `filter=(SCODE%3D%22600519%22)`——须用 URL 编码的双引号（`%22`），单引号（含编码后）实测报 9501 参数预处理错误
- 注意：这是**个股级**明细；全市场两融余额汇总用交易所每日披露（搜索 `两融余额` + 日期，取上交所/深交所数据）
- 备选：`https://data.eastmoney.com/rzrq/`（JS 重度渲染，需浏览器环境）

## 龙虎榜（2026-09-29 实测可用）

```
https://datacenter-web.eastmoney.com/api/data/v1/get?reportName=RPT_DAILYBILLBOARD_DETAILSNEW&source=WEB&client=WEB&filter=(TRADE_DATE='2026-09-28')
```
- 关键字段：`BILLBOARD_NET_AMT`（净买额）、`BILLBOARD_BUY_AMT`（买入额）、`BILLBOARD_SELL_AMT`（卖出额）、`EXPLAIN`（AI 席位标签，如"1家机构买入""2家机构卖出""深沪股通专用席位净买入"）
- 粒度说明：公共接口**不返回营业部席位明细**，只能到 EXPLAIN 标签级；真正的席位明细需看页面或第三方库。skill 中"机构席位 vs 游资席位方向"按标签级陈述，不编造具体营业部
- 备选：`https://data.eastmoney.com/stock/lhb.html`（JS 重度渲染，需浏览器环境）；兜底搜索 `龙虎榜` + 日期

## ETF 份额（收盘后/T+1）

- 优先：行情接口基金份额字段做 T-1 对比（如东财 push2 `f102` 基金份额；注意 push2 部分环境不稳定）
- 默认锚点（每次用同一批，保证前后可比）：沪深300ETF（510300）、科创50ETF（588000）、中证500ETF、中证A500ETF
- 备选：上交所/深交所官网 ETF 份额每日披露
- 兜底：搜索 `ETF追踪 昨日ETF净申购` + 日期（东财有每日"ETF追踪"系列，Choice 数据，是最稳定的每日口径）；仍取不到则按缺口行规范标注

## 兜底规则

接口失效时一律用网页搜索补足并注明来源，补不到的标注"待确认"，不编造数字。页面型数据源（data.eastmoney.com 各栏目页）均为 JS 重度渲染，无浏览器自动化时不作为主力路径。

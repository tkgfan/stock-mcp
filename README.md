# 股票MCP | A股、港股、美股数据与量化回测

**Stock MCP — Financial Data, Python Backtesting & Research Emails**

[English](README.en.md) · [官网与 Key 管理](https://zhiweigo.com/) · [魔搭 ModelScope](https://modelscope.cn/mcp/servers/gaomufans/zw-financial-data) · [连接配置示例](mcp-config.example.json)

**股票MCP（Stock MCP）** 将股票数据查询、财务分析、条件选股、云端 Python 量化回测和邮件发送接入 AI 助手。覆盖 **A股、港股、美股及指数**，历史金融数据覆盖 **1990 年至今**，并提供 **A股 60 分钟 K 线数据**。

不同市场、证券、指标及 K 线频率的实际起始日期和更新进度以查询结果为准。1990 年是整体数据覆盖的起点，不代表每只证券或每种频率都从该年开始。

本仓库提供 zhiweigo.com 托管股票 MCP 服务的接入文档和配置示例。服务通过远程 Streamable HTTP 使用，无需本地部署数据库或计算环境。

## 股票 MCP 能做什么

| 能力 | 说明 |
| --- | --- |
| 股票数据与行情查询 | 查询公司资料、交易日历、历史行情、财务报表、财务指标及指数数据 |
| A股 60 分钟 K 线 | 支持日内走势分析，查询前先确认可用证券、日期和字段 |
| 条件选股与财务研究 | 使用只读 SQL 筛选股票，比较盈利、成长、现金流和负债指标 |
| Python 量化回测 | 在云端隔离沙箱中运行分析、策略回测，生成图表和报告 |
| 网页搜索与读取 | 搜索新闻及公开资料，将网页正文提取为 Markdown |
| 研究报告与邮件发送 | 生成研究摘要或 HTML 报告，通过 send_email 发送至当前账号绑定的邮箱 |
| 文件与用量管理 | 获取当前 Key 工作区的结果文件，查询积分余额，管理工具权限和有效期 |

## 快速接入股票MCP

1. 打开 [zhiweigo.com](https://zhiweigo.com/) 并注册或登录。
2. 打开 **个人中心 → MCP → 创建 Key**，勾选需要的工具。
3. 在支持远程 MCP 的客户端中添加以下连接。
4. 连接后获取工具列表，再让 AI 助手执行股票研究任务。

| 配置项 | 值 |
| --- | --- |
| 显示名称 | 股票MCP / Stock MCP |
| 传输方式 | Streamable HTTP |
| MCP 服务地址 | https://api.zhiweigo.com/mcp |
| 请求头名称 | Authorization |
| 请求头值 | Bearer YOUR_MCP_KEY |

将 YOUR_MCP_KEY 替换为自己的完整 Key；Bearer 与 Key 之间保留一个空格。每位用户使用自己的 Key，请勿把真实 Key 提交到公开仓库、Issue 或截图中。

### JSON 配置示例

type 字段及配置文件位置以所用客户端版本为准。以下示例适用于接受 streamable_http 类型和 headers 字段的客户端；也可以在客户端界面手动填写地址和请求头。


```json
{
  "mcpServers": {
    "stock-mcp": {
      "type": "streamable_http",
      "url": "https://api.zhiweigo.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_MCP_KEY"
      }
    }
  }
}
```

客户端需支持 **Streamable HTTP 和自定义请求头**；部分客户端版本可能需要插件或桥接。此服务使用个人 MCP Key 鉴权。

## 可以直接尝试的股票分析任务

### A股条件选股

> 先确认可用数据的最新日期与字段，筛选最近三个完整财年净利润均为正的 A 股公司，按最近一年 ROE 排序，列出筛选条件和数据日期。

### 股票财务对比

> 对比三家同行公司的营收增长、利润率、经营现金流和负债水平，生成对比表与图表，并注明币种、单位和报告期。

### A股 60 分钟 K 线分析

> 查询我指定的 A 股股票最近一个月可用的 60 分钟 K 线，先确认数据覆盖日期和字段，再分析成交量与价格走势，列出数据缺口。

### Python 策略回测

> 查询一只股票的历史日线，用 Python 测试双均线策略，与买入持有比较。说明数据区间、除权除息处理和交易成本，输出收益曲线、最大回撤与交易次数。

### 将研究结果发送到邮箱

> 查询并分析我指定公司的财务与历史股价，补充相关公开新闻，将研究摘要整理为 HTML 邮件，发送到我在官网账号绑定的邮箱。

## MCP 工具清单

| 工具 | 用途 |
| --- | --- |
| stock_data | 在金融分析库执行只读 SQL，查询表结构、股票行情、财务及指数数据 |
| web_search | 搜索新闻和网页 |
| web_reader | 抓取网页正文并转换为 Markdown |
| sandbox_exec | 在隔离 Python 沙箱中执行分析、回测与文件生成命令 |
| sandbox_keepalive | 为运行中的长命令续租，或停止执行 |
| sandbox_files | 列出或读取当前 Key 工作区文件 |
| send_email | 向当前账号绑定邮箱发送 HTML 邮件 |
| current_time | 获取当前日期、时间及时区 |
| credit_balance | 查询当前 Key 的可用积分 |

实际可调用工具以当前 Key 的授权及服务可用状态为准。邮件支持自定义标题和 HTML 正文，单封邮件上限 3 MB，收件邮箱由当前账号绑定信息确定。

## 数据范围、计费与使用说明

- **数据来源与更新**：金融数据由 zhiweigo.com 提供，按采集任务更新。不同市场、证券与指标的覆盖范围可能不同，分析前请确认字段、时间范围及数据新鲜度。
- **回测口径**：区分报告期和公告日，明确复权、分红与交易成本，避免把未来才公布的信息用于历史决策。
- **积分计费**：调用前可通过 credit_balance 查询余额。股票数据查询、网页搜索、网页读取、邮件发送等按相应工具规则计费；沙箱按规格和运行时间计费。具体费用和记录以官网及工具说明为准。
- **沙箱与文件**：沙箱在命令执行时启动，结束后关闭；长命令需在租约到期前续租。需要保留的文件写入 /workspace，通过 sandbox_files 获取，工作区路径不是公开下载链接。
- **研究用途**：本服务提供数据查询与分析工具，研究及回测结果用于辅助判断，不构成投资建议。

## 常见问题

### 这是免费股票数据接口吗？

服务使用积分计费。公开接入文档不代表工具调用免费，当前价格和可用积分以官网及工具说明为准。

### 为什么连接后没有看到沙箱或邮件工具？

工具列表取决于当前 Key 的权限。请在官网检查相应工具权限，重新连接并获取列表。魔搭连接检测使用的测试 Key 只开放基础工具，不包含沙箱与邮件，因此魔搭展示的检测工具列表可能少于这里的完整能力清单。

### 是否需要部署服务端？

使用托管服务只需要 MCP 客户端、服务地址和个人 Key。本仓库提供接入文档与配置示例，服务端由 zhiweigo.com 运行。

### 1990 年至今是否包含每只股票的 60 分钟 K 线？

不同数据集覆盖时间不同。股票上市日期、市场、指标和频率都会影响起始日期，请先查询实际可用区间。

## 项目与目录收录信息

- **中文名称**：股票MCP（股票 MCP / 金融数据 MCP）
- **English name**: Stock MCP — Financial Data & Backtesting
- **服务提供方**：zhiweigo.com
- **官网**：https://zhiweigo.com/
- **MCP endpoint**：https://api.zhiweigo.com/mcp
- **Transport**：Streamable HTTP
- **Authentication**：个人 MCP Key，Authorization: Bearer YOUR_MCP_KEY
- **英文文档**：[README.en.md](README.en.md)
- **原始发布页**：[ModelScope 股票 MCP](https://modelscope.cn/mcp/servers/gaomufans/zw-financial-data)

Stock MCP provides China A-share, Hong Kong and US stock data, financial statements, index data, 60-minute A-share candlesticks, cloud Python backtesting, web research and research email delivery through the Model Context Protocol.

# Stock MCP | Stock Market Data, Financial Analysis & Backtesting

[简体中文](README.md) · [Website & API Keys](https://zhiweigo.com/) · [ModelScope](https://modelscope.cn/mcp/servers/gaomufans/zw-financial-data)

Stock MCP (股票MCP / 股票 MCP) connects AI assistants to hosted financial data, cloud Python analysis and research email delivery. This repository contains connection documentation and configuration examples for the hosted service operated by zhiweigo.com.

**Historical data spans 1990 to the present, including 60-minute candlestick data for China A-shares.** Use it for long-term market research and intraday analysis. Actual start dates and update progress vary by market, security, metric and bar frequency; confirm coverage in query results.

Connect financial data, cloud computing and email delivery to your preferred AI assistant.

Financial Data MCP supports stock research, financial analysis and quantitative strategy validation. It provides data for China A-shares, Hong Kong and US stocks, and indices, connecting web search, webpage reading, Python analysis, backtesting, report generation and email delivery.

Website and API key management: https://zhiweigo.com/

## Capabilities

- Financial data queries: retrieve company profiles, trading calendars, historical prices, financial statements, financial metrics and index data for stock screening, fundamental comparisons and historical statistics.
- Cloud Python analysis and backtesting: run code in an isolated sandbox to analyze data, evaluate strategies, and generate charts and reports without setting up a local database or computing environment.
- Web search and reading: search news and public sources, extract webpage content as Markdown, and combine it with structured financial data.
- Research emails: use send_email to send research summaries, conclusions or HTML report content to the email address linked to the current account. Custom subjects and HTML bodies are supported, with a 3 MB limit per email. The recipient is determined by the account's linked email address.
- Result files: list or read charts, datasets and reports generated in the current key's workspace.
- Usage management: check available credits and manage each key's tool permissions, expiration and credit source on the website.

## Quick start

1. Register or sign in at https://zhiweigo.com/.
2. Open Personal Center > MCP > Create Key and select the tools you need.
3. Add a remote MCP connection in your client using Streamable HTTP and https://api.zhiweigo.com/mcp. Set the Authorization header to Bearer followed by one space and your complete MCP key.
4. Connect, retrieve the tool list and try the examples below.

Connection details:
- Server identifier: zw-financial-data
- Transport: Streamable HTTP
- Endpoint: https://api.zhiweigo.com/mcp
- Authentication header: Authorization: Bearer YOUR_MCP_KEY

Clients must support remote MCP over Streamable HTTP and custom request headers. Some clients require a plugin or bridge, depending on the version. Each user supplies their own key.

### Example client configuration

Replace YOUR_MCP_KEY with your own key. Keep a space after Bearer. Never publish your real key in a repository, issue or screenshot. Client configuration formats vary; this example is for clients that accept the streamable_http type and headers field.

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

See [mcp-config.example.json](mcp-config.example.json).

## Example prompts

### Stock screening
Confirm the latest available data date and fields. Find China A-share companies with positive net profit in each of the last three complete fiscal years. Rank them by the latest annual ROE and show the screening criteria and data dates.

### Fundamental research
Compare revenue growth, profit margins, operating cash flow and debt levels for three companies in the same industry. Generate comparison tables and charts, specifying currencies, units and reporting periods.

### A-share 60-minute candlesticks
Query the available 60-minute bars for a China A-share stock over the last month. Confirm coverage and fields first, analyze volume and price movements, and identify missing intervals.

### Strategy backtesting
Retrieve a stock's historical daily prices. Use Python to backtest a dual moving-average strategy against buy-and-hold. State the data period, corporate-action adjustments and transaction costs, and report the equity curve, maximum drawdown and number of trades.

### Email research results
Analyze the financial statements and historical prices of a company I specify, add relevant public news, and send an HTML research summary to the email address linked to my account.

## Tools

- stock_data: execute read-only SQL in the financial analytics database to inspect schemas and query prices and financial data.
- web_search: search news and webpages.
- web_reader: fetch webpage content and convert it to Markdown.
- sandbox_exec: run analysis, backtesting and file-generation commands in an isolated Python sandbox.
- sandbox_keepalive: renew the lease for a running long command or stop execution.
- sandbox_files: list or read files in the current key's workspace.
- send_email: send an HTML email to the current account's linked email address.
- current_time: retrieve the current date, time and time zone.
- credit_balance: check the current key's available credits.

Available tools depend on the permissions granted to the current key and service availability.

## Data and usage notes

Financial data is provided by zhiweigo.com and refreshed through collection jobs. Coverage varies by market, security and metric. Before analysis, confirm fields, time ranges and data freshness. Historical backtests should distinguish reporting periods from publication dates and explicitly state price adjustments, dividends and transaction costs.

The service uses zw credits. Check your balance with credit_balance before making calls. Stock queries, web search, webpage reading, email delivery and other tools follow their respective pricing rules. Sandbox charges depend on resources and runtime. Refer to the website and tool descriptions for current fees and usage records.

The sandbox starts when a command runs and closes after execution. Renew long-running commands before their lease expires. Save files you want to retain under /workspace and retrieve them using sandbox_files. Workspace paths are not public download links.

This service provides data and analysis tools. Research and backtest results support decision-making and do not constitute investment advice.

## Tool permissions and directory listings

The test key used for ModelScope connection checks only enables basic tools and excludes sandbox and email permissions. Its detected tool list may therefore be shorter than the complete list above. To use sandbox backtesting, file access or email delivery, enable the corresponding permissions on your own key, then reconnect and retrieve the tool list. You can connect directly through the public endpoint above using a compatible remote MCP client.

Original ModelScope listing: https://modelscope.cn/mcp/servers/gaomufans/zw-financial-data

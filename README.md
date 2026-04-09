# Claude Code Market Research Skill

[![npm version](https://img.shields.io/npm/v/@lh-ai/claude-code-market-research.svg)](https://www.npmjs.com/package/@lh-ai/claude-code-market-research)

AI-powered market research skill for Claude Code. Generate comprehensive market research reports with a single request.

## Features

- **One-Command Research** - Just describe what you want to research
- **AI Personas** - Generates 1-10 target user profiles
- **Social Media Insights** - Simulates user voices from Xiaohongshu, Weibo, Douyin
- **Deep Interviews** - AI simulates interviews with each persona
- **Structured Reports** - Outputs professional Markdown reports

## Installation

```bash
npm install -g @lh-ai/claude-code-market-research
```

## Setup

### 1. Get API Key

1. Visit [ResearchMind Platform](https://platform.researchmind.ai)
2. Register/Login
3. Click 🔑 in sidebar to get your API Key

### 2. Configure Environment

Add to your `~/.claude/settings.json`:

```json
{
  "enabledPlugins": {
    "@lh-ai/claude-code-market-research": true
  },
  "env": {
    "MARKET_RESEARCH_API_KEY": "your_api_key_here"
  }
}
```

Or set environment variable:

```bash
export MARKET_RESEARCH_API_KEY="your_api_key_here"
```

## Usage

Just tell Claude what you want to research:

```
用户: 帮我研究年轻女性对国产美妆品牌的态度

Claude: 我来帮你进行市场研究...

[2-5 minutes later]

## 年轻女性对国产美妆品牌态度研究报告

### 一、执行摘要
本次研究发现...
```

## Examples

| User Request | Report Focus |
|--------------|--------------|
| "研究年轻女性对国产美妆的消费态度" | Brand perception, purchase factors |
| "分析大学生对新能源汽车的购买意愿" | Purchase consideration, barriers |
| "研究白领咖啡消费习惯" | Consumption patterns, brand preference |

## Report Structure

Generated reports include:

1. **Executive Summary** - Key findings (200 words)
2. **Research Method** - Qualitative approach used
3. **User Persona Analysis** - 5 detailed user profiles
4. **Key Findings** - Main insights and conclusions
5. **Market Insights** - Competitive landscape
6. **Opportunities & Recommendations** - Actionable suggestions
7. **Appendix** - Full interview transcripts

## Credits

- Each research costs **10 credits**
- Failed research automatically refunds credits
- Super admins have unlimited credits

## Requirements

- Claude Code CLI
- Valid API Key from ResearchMind Platform
- Internet connection

## License

MIT

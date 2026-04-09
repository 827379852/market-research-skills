# Market Research

TRIGGER when:
- 用户请求进行市场研究、市场调研、市场分析
- 用户想要研究消费者态度、消费习惯、购买意愿
- 用户提到"用户画像"、"用户洞察"、"消费者研究"
- 用户请求竞品分析、行业分析
- 用户说"帮我研究"、"做一个调研"、"分析一下市场"
- 用户提到定性研究、用户访谈、焦点小组

DO NOT TRIGGER when:
- 用户只是询问一般性问题（不是研究需求）
- 用户在进行代码开发或调试
- 用户在处理文件格式转换（如 PDF、Excel）
- 用户明确要求使用其他工具

## 功能

一键生成完整的市场研究报告，包括：

1. **研究设计** - AI 自动设计研究框架和访谈提纲
2. **用户人设** - 生成 1-10 个目标用户画像
3. **社媒侦察** - 模拟小红书、微博、抖音的用户声音
4. **深度访谈** - AI 模拟每个用户进行深度访谈
5. **研究报告** - 生成结构化的 Markdown 报告

## 使用方法

当用户触发此 skill 时，执行以下步骤：

### 步骤 1: 确认研究需求

向用户确认研究需求：
```
我来帮你进行市场研究。请确认以下信息：

研究需求: [用户的研究需求]
人设数量: 5 (可调整 1-10)

是否开始研究？
```

### 步骤 2: 执行研究

用户确认后，执行 Python 脚本：

```bash
pip install requests 2>/dev/null || echo "requests already installed"

python -c "
import sys
import time
import requests

# API 配置
API_BASE = 'http://localhost:8000/api/v1/research-flow'  # 本地开发
# API_BASE = 'https://your-domain.com/api/v1/research-flow'  # 生产环境

# 从环境变量获取 API Key，或使用默认值
API_KEY = '$MARKET_RESEARCH_API_KEY'

if not API_KEY:
    print('错误: 请设置环境变量 MARKET_RESEARCH_API_KEY')
    sys.exit(1)

# 提交任务
print('提交研究任务...')
resp = requests.post(
    f'{API_BASE}/auto-research/submit',
    headers={'Content-Type': 'application/json', 'X-API-Key': API_KEY},
    json={
        'user_request': '''用户的研究需求''',
        'persona_count': 5,
        'platforms': ['小红书', '微博', '抖音']
    }
)
result = resp.json()

if result.get('code') != 0:
    print(f'提交失败: {result.get(\"message\")}')
    sys.exit(1)

task_id = result['data']['task_id']
print(f'任务已提交: {task_id}')

# 轮询状态
print('等待研究完成...')
waited = 0
while waited < 600:
    resp = requests.get(
        f'{API_BASE}/auto-research/status/{task_id}',
        headers={'X-API-Key': API_KEY}
    )
    data = resp.json()['data']
    status = data['status']

    if status == 'completed':
        print('\\n' + '='*60)
        print(data['report'])
        break
    elif status == 'failed':
        print(f'任务失败: {data.get(\"error\")}')
        sys.exit(1)

    time.sleep(5)
    waited += 5
"
```

### 步骤 3: 输出报告

研究报告包含以下结构：

```markdown
## 一、执行摘要
研究核心发现（200字）

## 二、研究方法
采用的定性研究方法

## 三、用户画像分析
5 个典型用户画像（年龄、职业、消费习惯、痛点）

## 四、核心发现
关键洞察和结论（3-5 点）

## 五、竞品与市场洞察
市场环境和竞品分析

## 六、机会与建议
可执行的商业建议（3-5 条）

## 七、附录
完整访谈记录
```

## 配置

### 获取 API Key

1. 访问平台注册账号
2. 在侧边栏点击 🔑 获取 API Key
3. 设置环境变量：

```bash
export MARKET_RESEARCH_API_KEY="your_api_key_here"
```

### 积分消耗

- 每次研究消耗 10 积分
- 研究失败自动返还
- 超级管理员无限制

## 示例对话

**用户:** 帮我研究一下年轻女性对国产美妆品牌的态度

**Claude:** 我来帮你进行市场研究。请确认：

研究需求: 研究年轻女性对国产美妆品牌的态度
人设数量: 5

是否开始研究？

**用户:** 开始

**Claude:** [执行研究脚本，等待 2-5 分钟]

研究报告已完成：

## 年轻女性对国产美妆品牌态度研究报告

### 一、执行摘要
本次研究发现年轻女性对国产美妆品牌的认知度持续提升...
[完整报告内容]

## 注意事项

- 研究过程约需 2-5 分钟，请耐心等待
- 更详细的研究需求会得到更精准的报告
- 可调整人设数量（1-10）控制研究深度
- 报告以 Markdown 格式输出，可复制保存

<center style="font-weight:bold; font-size:33px;">AI 对冲基金</center>

本项目是一个AI驱动对冲基金的概念验证。项目目标是探索利用AI进行交易决策的可能性。本项目仅用于教育目的，不涉及真实交易或投资。

该系统由多个协同工作的智能体组成：

1. 本杰明·格雷厄姆智能体 - 价值投资之父，只买入具有安全边际的隐藏瑰宝
2. 比尔·阿克曼智能体 - 积极型投资者，采取大胆立场并推动变革
3. 凯西·伍德智能体 - 成长型投资女王，坚信创新和颠覆的力量
4. 查理·芒格智能体 - 巴菲特搭档，只以合理价格收购优质企业
5. 斯坦利·德鲁肯米勒智能体 - 宏观交易传奇，寻找具有爆发性增长潜力的不对称机会
6. 沃伦·巴菲特智能体 - 奥马哈先知，以合理价格寻求优质公司
7. 估值智能体 - 计算股票内在价值并生成交易信号
8. 情绪智能体 - 分析市场情绪并生成交易信号
9. 基本面智能体 - 分析基本面数据并生成交易信号
10. 技术面智能体 - 分析技术指标并生成交易信号
11. 风险经理 - 计算风险指标并设置仓位限制
12. 组合经理 - 做出最终交易决策并生成订单

<img width="1020" alt="Screenshot 2025-03-08 at 4 45 22 PM" src="https://github.com/user-attachments/assets/d8ab891e-a083-4fed-b514-ccc9322a3e57" />
>

注意：本系统仅模拟交易决策，不进行真实交易。

[![Twitter Follow](https://img.shields.io/twitter/follow/virattt?style=social)](https://twitter.com/virattt)

## 1. 免责声明

本项目仅用于教育及研究目的。

- 不适用于真实交易或投资
- 不提供任何保证或承诺
- 过往表现不代表未来结果
- 作者不承担任何财务损失责任
- 投资决策请咨询专业财务顾问

使用本软件即表示您同意仅将其用于学习目的。


## 2. 项目结构
项目结构
```bash
ai-hedge-fund/
├── src/
│   ├── agents/                   # 智能体定义
│   │   ├── bill_ackman.py        # 比尔·阿克曼智能体
│   │   ├── fundamentals.py       # 基本面分析智能体
│   │   ├── portfolio_manager.py  # 组合管理智能体
│   │   ├── risk_manager.py       # 风险管理智能体
│   │   ├── sentiment.py          # 市场情绪分析智能体
│   │   ├── technicals.py         # 技术面分析智能体
│   │   ├── valuation.py          # 估值分析智能体
│   │   ├── warren_buffett.py     # 巴菲特智能体
│   ├── tools/                    # 工具集
│   │   ├── api.py                # API工具
│   ├── backtester.py             # 回测工具
│   ├── main.py                   # 主程序入口
├── pyproject.toml
├── ...
```

## 3. 使用说明
### 3.1 安装
  
1. 克隆仓库：

    ```bash
    git clone https://github.com/virattt/ai-hedge-fund.git
    cd ai-hedge-fund
    ```

2. 安装Poetry（如未安装）：
    ```bash
    curl -sSL https://install.python-poetry.org | python3 -
    ```

3. 安装依赖：
    ```bash
    poetry install
    ```

4. 设置环境变量：
    ```bash
    # 创建.env文件存储API密钥
    cp .env.example .env
    ```

5. 配置API密钥：
    ```bash
    # OpenAI服务密钥（用于运行gpt-4o、gpt-4o-mini等模型）
    # 从https://platform.openai.com/获取密钥
    OPENAI_API_KEY=your-openai-api-key

    # Groq服务密钥（用于运行deepseek、llama3等模型）
    # 从https://groq.com/获取密钥
    GROQ_API_KEY=your-groq-api-key

    # 金融数据服务密钥
    # 从https://financialdatasets.ai/获取密钥
    FINANCIAL_DATASETS_API_KEY=your-financial-datasets-api-key
    ```

<b>重要提示</b>：必须至少设置OPENAI_API_KEY、GROQ_API_KEY、ANTHROPIC_API_KEY或DEEPSEEK_API_KEY中的一项。如需使用所有LLM服务，需配置全部密钥。

AAPL、GOOGL、MSFT、NVDA和TSLA的金融数据可免费获取，无需API密钥。

其他股票代码需要配置.env文件中的FINANCIAL_DATASETS_API_KEY。  

### 3.2 使用

运行对冲基金
```bash
poetry run python src/main.py --ticker AAPL,MSFT,NVDA
```

示例输出：​
<img width="992" alt="Screenshot 2025-01-06 at 5 50 17 PM" src="https://github.com/user-attachments/assets/e8ca04bf-9989-4a7d-a8b4-34e04666663b" />


可通过--show-reasoning参数显示各智能体的决策依据：

```bash
poetry run python src/main.py --ticker AAPL,MSFT,NVDA --show-reasoning
```

可选指定时间范围进行决策：

```bash
poetry run python src/main.py --ticker AAPL,MSFT,NVDA --start-date 2024-01-01 --end-date 2024-03-01 
```
运行回测系统
```bash
poetry run python src/backtester.py --ticker AAPL,MSFT,NVDA
```
示例输出：​
<img width="941" alt="Screenshot 2025-01-06 at 5 47 52 PM" src="https://github.com/user-attachments/assets/00e794ea-8628-44e6-9a84-8f8a31ad3b47" />


可选指定时间范围进行回测：

```bash
poetry run python src/backtester.py --ticker AAPL,MSFT,NVDA --start-date 2024-01-01 --end-date 2024-03-01
```

## 4. 贡献指南
1. Fork本仓库
2. 创建功能分支
3. 提交修改
4. 推送分支
5. 创建Pull Request

重要提示：请保持PR小而专注，便于审核合并。


## 5. 功能请求
如有功能建议，请提交issue并添加enhancement标签。

## 6. 许可协议
本项目采用MIT许可协议，详见LICENSE文件。

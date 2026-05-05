# LHPT - Cryptocurrency Quantitative Trading Platform

加密货币量化交易平台，支持可视化回溯历史数据，验证策略效果。

## 功能特点

- **多交易所支持**: 通过 CCXT 统一接口支持 Binance、OKX 等 100+ 交易所
- **历史数据缓存**: SQLite 本地缓存，下载后秒级加载
- **一键下载**: 支持批量下载主流币种历史数据
- **内置策略**: MA 交叉、RSI、网格交易、定投策略
- **自定义策略**: 支持 Python 脚本自定义策略
- **专业图表**: TradingView Lightweight Charts K 线图
- **回放模拟**: K线逐根播放，手动交易练习
- **回测报告**: 收益率、最大回撤、夏普比率、胜率等指标

## 技术栈

- **前端**: Next.js 14 + React 18 + TypeScript + Tailwind CSS
- **图表**: TradingView Lightweight Charts
- **后端**: Python 3.11 + FastAPI
- **数据处理**: pandas, numpy, CCXT
- **存储**: SQLite



## 快速开始


### 2. 配置环境变量



### 3. 启动服务



### 4. 访问界面

打开浏览器访问 http://localhost:3000

### 5. 下载历史数据（加速加载）

首次使用建议下载历史数据到本地缓存：

- **前端界面**: 点击侧边栏的"一键下载全部热门币种"
- **API 调用**: 
  ```bash
  # 下载 BTC 1年数据
  curl -X POST "http://localhost:8000/api/data/cache/download?symbols=BTC/USDT&days=365"
  
  # 下载主流币种 30天数据
  curl -X POST "http://localhost:8000/api/data/cache/download-all?days=30"
  ```

数据缓存后，加载速度从数秒降至毫秒级。

## 内置策略

### 1. MA Cross (均线交叉)
- 参数: `fast_period`, `slow_period`
- 逻辑: 快慢均线交叉时产生信号

### 2. RSI (相对强弱指数)
- 参数: `period`, `oversold`, `overbought`
- 逻辑: RSI 低于超卖线买入，高于超买线卖出

### 3. Grid (网格交易)
- 参数: `grid_levels`, `grid_spacing`
- 逻辑: 在价格区间内设置网格，自动交易

### 4. DCA (定投策略)
- 参数: `buy_interval`, `buy_amount`, `take_profit`
- 逻辑: 定期买入，达到目标收益后卖出

## 自定义策略

在 `strategies/` 目录下创建 Python 文件:

```python
import pandas as pd

def generate_signals(df: pd.DataFrame, params: dict) -> pd.DataFrame:
    signals = pd.DataFrame(index=df.index)
    
    # 你的策略逻辑
    signals['buy'] = ...  # 布尔值，True 表示买入
    signals['sell'] = ... # 布尔值，True 表示卖出
    
    return signals
```






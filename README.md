# Breakout Strategy Crypto Trading Bot

## Overview

This Python-based crypto trading bot implements a breakout strategy to trade the uBTCUSD pair on the Phemex exchange. The bot analyzes 15-minute candlestick data over the last three days (289 periods) to determine support and resistance levels. It then places limit orders on breakout retests.

## Features

- **Automated trading:** Places buy and sell orders based on breakout signals.

- **Support & Resistance Calculation:** Determines key levels from historical data.

- **Re-test Mechanism:** Confirms breakouts before executing trades.

- **Position Management:** Avoids over-trading when already in a position.

- **PnL Tracking & Sleeping on Close:** Manages risk and prevents excessive order submissions.

- **Failsafe Handling:** Automatically retries on internet connection issues.

## Strategy Explanation

1. **Data Collection:**

- Fetches the last 3 days of 15-minute candlestick data (289 periods).

- Identifies support (lowest close price) and resistance (highest close price).

2. **Breakout Detection:**

- If the bid price breaks above resistance → BUY order placed just above resistance.

- If the bid price breaks below support → SELL order placed just below support.

3. **Trade Execution:**

- The bot cancels all previous orders before placing new ones.

- Uses create_limit_buy_order and create_limit_sell_order with PostOnly parameters.

- Sleeps for 2 minutes after submitting an order.

4. **Risk Management:**

- Position size (pos_size) is limited to prevent overexposure.

- Targets +9% gain and max loss of -8%.

## Requirements
**Install Dependencies**
   ```bash
   pip install ccxt pandas numpy schedule
   ```
**API Key Setup**

1. Create a **dontshare_config.py** file and add your API keys:
   ```bash
   xP_hmv_KEY = "your_api_key"
   xP_hmv_SECRET = "your_api_secret"
   ```
2. **Ensure the file is not shared** to protect your credentials.

## How to Run the Bot
   ```bash
   python breakout_bot.py
   ```
The bot will run continuously, checking for breakout opportunities every 28 seconds.
## Configuration Parameters
```bash

| Parameter      | Description                  | Default Value |
| -------------- | ---------------------------- | ------------- |
| symbol         | Trading pair                 | uBTCUSD       |
| pos_size       | Position size                | 30            |
| target         | Profit target (%)            | 9             |
| max_loss       | Max acceptable loss (%)      | -8            |
| pause_time     | Time between trades (mins)   | 10            |
| vol_repeat     | Volume check repeats         | 11            |
| vol_time       | Volume check interval (secs) | 5             |
```
## Future Improvements
- Implement stop-loss orders for better risk management.
- Improve breakout confirmation using moving averages.
- Add more trading pairs for diversification.
## Disclaimer
This bot is for educational purposes only. Trading involves risk, and past performance is not indicative of future results. Use at your own discretion.

* **Code is currently in writing and will be pushed as soon as the bot is done**

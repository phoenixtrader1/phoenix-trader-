# Phoenix Trader

[![Python](https://img.shields.io/badge/python-3.11-blue.svg)](https://www.python.org/)  
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)  

**Phoenix Trader** is a modular, professional Solana trading bot designed for smart, automated trading. It supports:

- Automated token scanning via Dexscreener and public APIs
- Rule-based or ML-ready AI scoring for entry decisions
- Async trading loop for 24/7 operation
- PAPER mode for safe testing
- LIVE mode for real Solana trading with Jupiter swaps
- Real-time PnL tracking and position management
- Telegram bot control for remote management

---

## 🔄 How It Works

Phoenix Trader is designed as a **fully automated Solana trading bot** with a modular architecture:

1. **Token Scanning**  
   - Scans Solana DEXs (via Dexscreener and public APIs) to find new tokens.  
   - Filters based on liquidity, 5-minute volume, age, and other safety parameters.

2. **Feature Extraction & Scoring**  
   - Converts token data into features (price, liquidity, volume, symbol length, etc.).  
   - Rule-based or ML-ready scorer evaluates features and assigns a score.  
   - Tokens below the score threshold are ignored.

3. **Entry Logic**  
   - Tokens passing scoring filters and risk limits are considered for purchase.  
   - Position size is a fraction of total capital (`MAX_POSITION_PCT`).  
   - Executes in **PAPER mode** (simulation) or **LIVE mode** (real Jupiter swap).

4. **Exit Logic**  
   - Monitors positions continuously.  
   - Positions are closed automatically based on **stop-loss** or **take-profit thresholds**.  

5. **Position & PnL Tracking**  
   - Tracks entry price, current price, and size of each position.  
   - Calculates real-time PnL for reporting and risk management.

6. **Async Loop & Telegram Control**  
   - Runs asynchronously: scanning, evaluating, trading in a continuous loop.  
   - Telegram bot allows remote **start**, **stop**, and **status** commands.

7. **Risk Management**  
   - Limits number of open positions (`MAX_POSITIONS`) and trade size.  
   - Filters tokens based on liquidity, volume, and scoring.  
   - Stop-loss and take-profit prevent large losses and secure gains.

---

## 📊 Strategy

Phoenix Trader uses a **rule-based, score-driven strategy**:

### Entry Strategy
- Token score must exceed `MIN_SCORE`.  
- Token liquidity > `MIN_LIQUIDITY`.  
- Token age < `MAX_TOKEN_AGE` (minutes).  
- Max open positions (`MAX_POSITIONS`) not exceeded.  
- Position size = `TOTAL_SOL * MAX_POSITION_PCT`.

### Exit Strategy
- Take-profit threshold: `TAKE_PROFIT` (e.g., 80% gain).  
- Stop-loss threshold: `STOP_LOSS` (e.g., -20% loss).  
- PnL = `(current_price - entry_price) / entry_price`.  

### Modes
- **PAPER**: simulated trades, prints logs instead of executing.  
- **LIVE**: executes real trades via Jupiter swap, tokens swapped back to SOL on exit.

---

## 🛠 Installation

1. Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/phoenix-trader.git
cd phoenix-trader

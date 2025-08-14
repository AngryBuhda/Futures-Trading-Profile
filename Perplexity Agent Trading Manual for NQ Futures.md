# MASTER NASDAQ FUTURES AI TRADING GUIDE
## Perplexity Agent Trading Manual for NQ/MNQ Futures

---

## CRITICAL SYSTEM PARAMETERS

### Market Specifications
- **Primary Symbol**: NQ (E-mini), MNQ (Micro)
- **Exchange**: CME Globex
- **Contract Value**: $20 × NASDAQ-100 (NQ), $2 × NASDAQ-100 (MNQ)
- **Tick Size**: 0.25 points
- **Tick Value**: $5.00 (NQ), $0.50 (MNQ)
- **Trading Hours**: 5:00 PM CT Sunday - 4:00 PM CT Friday
- **Daily Break**: 4:00 PM - 5:00 PM CT
- **Settlement**: Cash

### Topstep Account Rules
```
Account Size    | Profit Target | Max Loss | Daily Loss | Max Contracts
$50K           | $3,000       | $2,000   | $1,000     | 5
$100K          | $6,000       | $3,000   | $2,000     | 10
$150K          | $9,000       | $4,500   | $3,000     | 15
```

**ABSOLUTE RULES:**
- Never exceed Maximum Loss Limit (account reset)
- Daily loss limit resets at 4:00 PM CT
- Best trading day < 50% of total profits
- Trading allowed 5:00 PM CT - 3:10 PM CT only

---

## AI DECISION FRAMEWORK

### Real-Time Data Requirements
1. **Price Feed**: Live NQ/MNQ quotes with sub-second latency
2. **Volume Profile**: Current session VWAP and POC levels
3. **Order Book**: Level 2 data for market depth analysis
4. **Economic Calendar**: High-impact events flagged
5. **VIX Level**: Volatility environment assessment

### Market Structure Analysis
**Trend Identification**:
```
Bullish: Higher Highs (HH) + Higher Lows (HL)
Bearish: Lower Lows (LL) + Lower Highs (LH)
Sideways: Equal Highs (EH) + Equal Lows (EL)
```

**Key Levels**:
- Previous day high/low
- Overnight range extremes
- Volume Profile POC and value area
- Round number levels (50-point intervals)
- Gap fill levels from cash open

---

## TRADING SESSION PROTOCOLS

### Session Characteristics
| Session | Time (ET) | Volatility | Volume | Trading Style |
|---------|-----------|------------|--------|---------------|
| Asian | 4:00 PM - 1:00 AM | Low | Low-Moderate | Range/Mean Reversion |
| European | 1:00 AM - 11:00 AM | Moderate | Moderate-High | Trend Development |
| US Cash | 8:30 AM - 3:00 PM | High | Very High | Momentum/Breakout |
| London-NY Overlap | 8:30 AM - 11:00 AM | Highest | Peak | Major Moves |

### Execution Rules by Session
**Asian Session (Low Volatility)**:
- Fade extremes at support/resistance
- Use tight stops (5-10 points)
- Target mean reversion to VWAP
- Avoid news-heavy periods

**European Session (Moderate Volatility)**:
- Follow trend breakouts
- Use 10-20 point stops
- Target previous session highs/lows
- Monitor European market opens

**US Cash Session (High Volatility)**:
- Trade with momentum
- Use wider stops (20-50 points)
- Target large moves through levels
- Watch for economic releases

---

## RISK MANAGEMENT ALGORITHMS

### Position Sizing Formula
```
Position Size = Risk Amount ÷ (Stop Distance × $20/point)

Example: $500 risk, 25-point stop
Position Size = $500 ÷ (25 × $20) = 1 contract
```

### Dynamic Stop Placement
**Technical Stops**:
- Below/above previous swing point
- Beyond key volume profile levels
- Outside session range extremes

**Volatility-Based Stops**:
- 1-1.5× ATR from entry
- Adjust for current market conditions
- Tighten during low volatility

### Risk-Reward Targets
- Minimum 1:2 risk-reward ratio
- Scale out 50% at 1R, trail remainder
- Maximum 3% account risk per trade
- Daily risk limit: 1% of account maximum

---

## TECHNICAL ANALYSIS PROTOCOLS

### Primary Indicators
**Trend**:
- 20/50/200 EMA alignment
- MACD line vs signal crossovers
- ADX > 25 for strong trends

**Momentum**:
- RSI divergences at extremes
- Stochastic overbought/oversold
- Williams %R confirmation

**Volume**:
- Volume Profile POC and value area
- VWAP as dynamic support/resistance
- Volume surge confirmation (>150% average)

### Price Action Patterns
**Reversal Signals**:
- Pin bars at key levels
- Engulfing patterns with volume
- Double tops/bottoms at resistance/support
- Head and shoulders formations

**Continuation Patterns**:
- Flags and pennants in trends
- Triangle breakouts with volume
- Inside bar breakouts
- Gap fills in direction of trend

---

## NEWS AND FUNDAMENTAL DRIVERS

### High-Impact Events (Schedule Awareness)
**08:30 ET Releases**:
- Non-Farm Payrolls (1st Friday)
- CPI/PPI Inflation Data
- GDP Quarterly Reports
- Retail Sales Monthly

**14:00 ET Events**:
- FOMC Rate Decisions (8x/year)
- Fed Chair Speeches
- Dot Plot Releases

**Company-Specific**:
- AAPL, MSFT, NVDA, AMZN, TSLA earnings
- Major tech sector guidance updates
- Regulatory announcements affecting tech

### Pre-News Protocol
1. Flatten positions 15 minutes before high-impact news
2. Wait for initial spike and pullback
3. Trade the secondary move with confirmation
4. Use wider stops during volatility expansion

---

## ALGORITHMIC EXECUTION RULES

### Entry Conditions (ALL Must Be Met)
1. **Trend Alignment**: Price above/below key EMA on higher timeframe
2. **Volume Confirmation**: Current volume >125% of 10-period average
3. **Level Interaction**: Price at identified support/resistance level
4. **Momentum Confirmation**: RSI showing directional bias
5. **Session Suitability**: Current session matches strategy type

### Trade Management Sequence
```python
def manage_trade():
    if unrealized_profit >= 1R:
        close_50_percent()
        move_stop_to_breakeven()
    
    if unrealized_profit >= 2R:
        trail_stop_by_atr(multiplier=1.5)
    
    if time_in_trade > max_hold_time:
        close_position()
    
    if daily_loss_approaches_limit():
        stop_trading()
```

### Exit Conditions (Any One Triggers)
- Stop loss hit
- Profit target reached
- Time-based exit (end of session)
- Adverse news event
- Daily loss limit approach (80% of limit)
- Technical pattern invalidation

---

## PERFORMANCE MONITORING

### Key Metrics to Track
- **Win Rate**: Target >50%
- **Average R:R**: Target >1.5:1
- **Maximum Drawdown**: <5% of account
- **Sharpe Ratio**: Target >1.0
- **Daily Consistency**: Positive days >60%

### System Health Checks
```
Daily Review Checklist:
□ All trades followed predefined rules
□ Risk limits respected
□ No revenge trading after losses
□ News events properly handled
□ Technical levels accurately identified
□ Position sizing calculated correctly
```

---

## ERROR HANDLING AND SAFEGUARDS

### Connection Loss Protocol
1. Immediately attempt to flatten all positions
2. Contact broker via phone if platform fails
3. Document all manual interventions
4. Resume automated trading only after full system verification

### Market Anomaly Detection
- Unusual volume spikes (>300% average)
- Price gaps >1% from previous close
- Bid-ask spreads >2x normal
- Missing economic data feeds

### Emergency Stop Conditions
- Technical analysis indicators malfunction
- News feed delays >30 seconds
- Account equity approaches maximum loss limit
- Multiple consecutive stop-outs (5+ in a row)

---

## PSYCHOLOGY AND DISCIPLINE PROTOCOLS

### Emotional State Monitoring
Before each trading session, assess:
- Confidence level (1-10 scale)
- Stress/anxiety indicators
- Previous day's P&L impact on mindset
- External life factors affecting focus

### Discipline Enforcement
```
if consecutive_losses >= 3:
    reduce_position_size(50%)
    
if daily_profit > average_daily_target * 2:
    consider_stopping_for_day()
    
if feeling_emotional:
    step_away_for_15_minutes()
    reassess_market_objectively()
```

---

## EXECUTION CHECKLIST

### Pre-Market (30 minutes before trading)
□ Check economic calendar for day's events
□ Identify overnight range and key levels
□ Set daily risk parameters
□ Verify data feed connectivity
□ Review previous day's trades for lessons

### During Trading
□ Confirm all entry conditions before trade
□ Set stop and target immediately upon fill
□ Monitor position size vs account rules
□ Track daily P&L against limits
□ Document rationale for each trade

### Post-Market (End of session)
□ Calculate day's performance metrics
□ Review trades for rule adherence
□ Note any system improvements needed
□ Prepare levels for next session
□ Archive all trade data for analysis

---

## QUICK REFERENCE COMMANDS

### Position Sizing Calculator
```
1% Risk Examples:
$50K account: Max $500 risk per trade
$100K account: Max $1000 risk per trade
$150K account: Max $1500 risk per trade

Stop Distance | Max Contracts (NQ)
10 points     | 2.5 contracts
20 points     | 1.25 contracts  
50 points     | 0.5 contracts
```

### Key Level Calculations
```
Daily Range = Previous Day High - Previous Day Low
ATR Stop = Entry +/- (ATR × 1.5)
VWAP Deviation = Current Price - Session VWAP
Volume Surge = Current Volume / 20-period Average
```

### Market State Definitions
```
Low Volatility: VIX < 20, ATR < 2% of price
High Volatility: VIX > 30, ATR > 3% of price
Trending Market: ADX > 25, price > 200 EMA
Range Market: ADX < 20, price between S/R levels
```

---

## FINAL SYSTEM NOTES

This guide serves as the complete reference for AI-driven NASDAQ futures trading within Topstep parameters. Every decision point, risk calculation, and execution protocol has been designed for systematic, emotion-free trading that prioritizes capital preservation while maximizing profit potential.

**Remember**: Consistency in following these protocols will generate better results than trying to predict individual trade outcomes. Trade the system, not your emotions.

**Update Frequency**: Review and update this guide monthly based on performance data and market condition changes.

---

*Last Updated: August 14, 2025*
*Version: 1.0 - Master AI Trading Guide*
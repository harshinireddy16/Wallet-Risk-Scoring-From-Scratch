# Wallet-Risk-Scoring-From-Scratch
## 🧾 Explanation: Risk Scoring Methodology

### 🛠️ Data Collection Method
We used the [Covalent API](https://www.covalenthq.com/docs/api/) to fetch Compound V2/V3 transaction data for 100 wallet addresses. For each wallet, we pulled up to 1000 recent transactions and filtered for `compound.finance` activity.

### 📊 Feature Selection Rationale
To build a risk profile, we extracted the following features per wallet:
- `num_tx`: Total number of transactions (indicates activity)
- `total_gas`: Cumulative gas used (more gas = more genuine use)
- `num_compound_interactions`: Count of direct interactions with Compound
- `num_failed_tx`: Failed transactions (used as a negative risk indicator)

These features were chosen for their relevance in identifying active, reliable DeFi participants versus dormant or risky wallets.

### ⚖️ Scoring Method
- We normalized all features using **MinMaxScaler**.
- Applied custom weights to each feature:
  - Positive: Activity, gas, protocol interaction
  - Negative: Failed transactions
- The final score was scaled between **0 and 1000** where:
  - **1000 = Low Risk**
  - **0 = High Risk**

### ✅ Risk Indicator Justification
- High failed transactions → suspicious or poorly managed wallets
- More Compound use → familiarity with protocol = less risky
- High activity and gas use → genuine, frequent usage
  
The final output is stored in the file:  
**`wallet_scores.csv`**


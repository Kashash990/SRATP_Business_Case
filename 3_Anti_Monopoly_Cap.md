# 3. Anti-Monopoly & Takeover Cap Validation Blueprint

To comply with Saudi regulatory guidelines and protect property tranches from hostile takeovers, the platform enforces a strict threshold restriction at the smart-contract state layer.

## 1. The Validation Flowchart
* **Investor Initiates Purchase Command** → **Check Current Balance + Proposed Purchase Amount** → **Is Total Value > 20% of Asset?**
  * **YES:** Transaction Rejected & Error Thrown
  * **NO:** Transaction Cleared & Tokens Minted

## 2. The Verification Code Architecture
Before executing a primary subscription or confirming a secondary market buy order, the transaction passes through an automated conditional check:

```solidity
function validatePurchase(address investor, uint256 tokenAmountToBuy) public view returns (bool) {
    uint256 currentBalance = balanceOf(investor);
    uint256 totalProposedBalance = currentBalance + tokenAmountToBuy;
    uint256 maxAllowedBalance = (totalSupply() * 20) / 100; // Calculates the 20% maximum cap

    // Enforcement Conditional Block
    require(totalProposedBalance <= maxAllowedBalance, "EXCEEDS_20_PERCENT_ANTI_MONOPOLY_MAXIMUM_CAP");
    return true;
}
```

## 3. Edge-Case System Controls
* **Secondary Market Synchronization:** This check is hardcoded directly into the core `_transfer()` logic of the property token. If an investor tries to buy up fractional tokens from other users on the secondary bulletin board, the contract intercepts and blocks the trade the moment their total holding crosses 20%.
* **Affiliate Cluster Flagging:** To prevent sophisticated actors from bypassing the system by creating multiple individual accounts under a single corporate umbrella, our frontend platform cross-references underlying Beneficial Ownership (UBO) records during the API verification phase. It groups corporate affiliates into a single risk cluster, applying the 20% restriction to their collective holdings.


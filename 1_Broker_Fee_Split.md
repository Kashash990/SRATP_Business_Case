# 1. Smart-Contract Architecture Specification: Automated Broker Fee-Split Logic

This technical specification details the programmatic fee architecture for automated commission payouts directly to traditional real estate brokers who bring assets or capital pools to the SRATP platform.

## 1. Core Logic & Variables
The contract dynamically intercepts incoming investor capital during primary issuance subscription cycles. Instead of routing the full transaction fee to the platform's operating balance and manually paying commissions later, the protocol distributes the funds programmatically at the block level.

* **TotalRaisedAmount:** Total capital cleared through the property tranche (e.g., SAR 1,000,000).
* **PrimarySaleFeeRate:** Locked at **2.5%** (`0.025`).
* **BrokerShareRate:** Locked at **0.5%** (`0.005`).
* **PlatformNetShareRate:** Remainder **2.0%** (`0.020`).

## 2. Programmatic Execution Rule
Upon execution of the `finalizeTranche()` transaction (triggered once the property pool hits 100% funding), the contract runs the following distribution flow:

```solidity
// Mathematical Allocation Check
uint256 totalFee = (TotalRaisedAmount * PrimarySaleFeeRate) / 10000; // 2.5% Total Cut
uint256 brokerCut = (TotalRaisedAmount * BrokerShareRate) / 10000;   // 0.5% Broker Allocation
uint256 platformCut = totalFee - brokerCut;                         // 2.0% Net SRATP Allocation

// Automated On-Chain Transfer Executions
payable(PropertySellerAddress).transfer(TotalRaisedAmount - totalFee);
payable(PlatformOpsAddress).transfer(platformCut);
payable(RegisteredBrokerAddress).transfer(brokerCut);
```

## 3. Operational Safe Controls
* **Zero-Address Enforcement:** If a property has no broker affiliate assigned (`RegisteredBrokerAddress == address(0)`), the contract automatically overrides the split logic. It routes the entire **2.5% fee** straight to the `PlatformOpsAddress` to prevent funds from being permanently lost.
* **Immutable Fee Caps:** The contract hardcodes the `PrimarySaleFeeRate` as a constant (`constant public`), ensuring no external factor or technical adjustment can alter the transaction distribution logic post-deployment.

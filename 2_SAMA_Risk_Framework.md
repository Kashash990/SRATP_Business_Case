# 2. SAMA Sandbox Risk Management Framework: Virtual IBAN Asset Isolation Flows

This document details the operational architecture used to fulfill SAMA and CMA requirements ensuring that the SRATP platform does not hold, store, or clear client money directly.

## 1. The Operational Workflow
* **Step 1:** Every investor onboarding onto the SRATP platform triggers an automated API call to our partner commercial bank via Banking-as-a-Service (BaaS) API integrators.
* **Step 2:** The banking API instantly spins up a unique, dedicated **Virtual IBAN** tied explicitly to that investor's national identity number (*Nafath/CR*), mapped under a master **SRATP Client Escrow Account**.
* **Step 3:** The investor initiates an external bank transfer (*SARIE*) directly to their unique virtual IBAN. The physical cash lands inside the secure vault of the regulated partner bank—**never touching SRATP’s corporate balance sheet**.
* **Step 4:** The bank sends an automated confirmation webhook to the SRATP ledger. The platform validates the deposit and programmatically mints the matching fractional real estate tokens to the investor's secure wallet.

## 2. Systemic Risk Mitigations
* **Bankruptcy Remoteness:** Because all asset purchase funds reside in an external escrow account managed by a licensed commercial bank, if SRATP faces corporate insolvency, user capital remains safe, isolated, and accessible for direct claims.
* **Zero Commingling Policy:** The platform keeps its operating accounts (for corporate expenses, payroll, and developer listing fees) completely detached from the client transaction escrow architecture.

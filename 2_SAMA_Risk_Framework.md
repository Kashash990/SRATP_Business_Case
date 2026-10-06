Step 3: In-Order Regulatory Deliverable 2
SAMA Sandbox Risk Management Framework: Virtual IBAN Asset Isolation Flows
Regulators (SAMA and CMA) require strict operational assurance that your platform does not hold, store, or clear client money directly. This document maps out how you mitigate custody risks by using Banking-as-a-Service (BaaS) and API-driven virtual IBAN escrow loops.
1. The Operational Workflow
[ Investor Account ] ──► [ Unique Virtual IBAN ] ──► [ Licensed Escrow Bank Pool ]
                                                                  │
                                 [ Automated Webhook Confirmation ]
                                                                  │
                                                                  ▼
                                                      [ SRATP Token Minting ]
• Step 1: Every investor onboarding onto the SRATP platform triggers an automated API call to our partner commercial bank (e.g., Al Rajhi or SNB via APIs from providers like Lean/Tarabut).
• Step 2: The banking API instantly spins up a unique, dedicated Virtual IBAN tied explicitly to that investor's national identity number (Nafath/CR), mapped under a master SRATP Client Escrow Account.
• Step 3: The investor initiates an external bank transfer (SARIE) directly to their unique virtual IBAN. The physical cash lands inside the secure vault of the regulated partner bank—never touching SRATP’s corporate balance sheet.
• Step 4: The bank sends an automated confirmation webhook to the SRATP ledger. The platform validates the deposit and programmatically mints the matching fractional real estate tokens to the investor's secure wallet.
2. Systemic Risk Mitigations
• Bankruptcy Remoteness: Because all asset purchase funds reside in an external escrow account managed by a licensed commercial bank, if SRATP faces corporate insolvency, user capital remains safe, isolated, and accessible for direct claims.
• Zero Commingling Policy: The system maintains strict operational walls. Platform operating funds (such as asset listing fees or corporate payroll) are kept in a separate, isolated corporate account, making it impossible to commingle operational expenses with client transaction pools.


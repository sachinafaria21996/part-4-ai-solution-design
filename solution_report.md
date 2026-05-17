# Task 1: Choose a Business Domain

- Domain: Finance

# Task 2: Define the Business Problem

## What problem is being solved?

- Detecting suspicious and potentially fraudulent financial transactions accurately and in real-time.

## Who are the users or stakeholders? 

- Fraud Analysts, Risk Management Teams, and Bank Customers.

## What is the current manual or traditional process? 

- The current process relies on static, rule-based systems (e.g., flagging any transaction over Rs 50,000 or from a high-risk country) followed by manual investigation by fraud analysts.

## What are the limitations of the current process? 

- Rule-based systems are rigid and easily bypassed by sophisticated fraudsters. 
- They also generate an overwhelming number of false positives. 
- Based on the given business KPI sample, this leads to high manual_processing_hours (often exceeding 500 hours a month) and high average_resolution_time_hours (30-40+ hours), delaying legitimate transactions.

# Task 3: Identify the AI Task Type

- AI Task Type: Anomaly detection / Classification

- Why this AI task type is suitable: 

    - Classification is ideal because we have historical transaction records that can be labeled as "fraud" or "legitimate." 
    - Anomaly detection complements this by identifying outliers—new, unseen patterns of fraudulent activity that deviate from a customer's normal baseline behavior.

# Task 4: Data Requirement Plan

- Type of data needed: Historical transaction data and customer profiles.

- Structured or unstructured data: Highly structured tabular data.

- Input features: Transaction amount, time of day, geolocation, merchant category code, device IP address, and time since the last transaction.

- Target variable or labels: Is_Fraud (Binary: 1 for Suspicious/Fraud, 0 for Legitimate).

- Data collection method: Continuously ingested from the bank's payment processing gateways, CRM systems, and relational databases.

- Data quality risks: 

    - Class Imbalance: Fraudulent transactions make up a tiny fraction of total transactions, which can bias the model toward predicting "legitimate."

    - Delayed Labels: It can take weeks for a customer to report a chargeback, meaning recent data may have incorrect labels.

# Task 5: Model Recommendation

- Recommended Model: Feed-forward neural network or Autoencoder.

- Why it is appropriate: 

    - A Feed-forward neural network is highly capable of learning complex, non-linear interactions between dozens of structured features (e.g., how the combination of "merchant type," "time of day," and "location" correlates to fraud). 

    - Alternatively, an Autoencoder (unsupervised) is excellent for anomaly detection, learning what a "normal" transaction looks like and flagging transactions that fail to fit that learned pattern.

# Task 6: Evaluation Plan

- Technical metrics: 
    - Recall (ensuring we catch as much fraud as possible)
    - Precision (ensuring we don't flag too many legitimate transactions).

- Business metrics: 

    - Connecting to our KPI dataset, the success of the model will be measured by a reduction in manual_processing_hours and average_resolution_time_hours. 

    - We also expect the error_rate_percent of investigations to drop while the customer_satisfaction_score increases due to fewer blocked cards.

- Possible failure cases: 
    - Sudden, legitimate shifts in customer behavior (e.g., mass holiday travel or a major shopping event like Black Friday) triggering a spike in false alarms.

- Human review or validation process:
    - The AI will act as a filter system.
    - High-confidence fraud predictions will auto-block the transaction, while medium-confidence "borderline" cases will be routed to a human fraud analyst for final review.

# Task 7: Responsible AI Considerations

- False Positives / Impact on Users: 

    - The most significant risk is blocking legitimate users from making essential purchases (e.g., paying for emergency medical care or groceries), which damages trust.

- Bias in Data: 

    - The model might inadvertently learn to disproportionately flag transactions in specific geographic regions, lower-income neighborhoods, or specific demographics based on historical biases in the training data.

- Over-reliance on AI: 

    - Human analysts might develop "automation bias," blindly trusting the AI's fraud flags without independently investigating the context of the transaction.

- Need for Human Oversight:

    - Customers must have a clear, immediate escalation path (like an instant SMS verification link) to confirm their identity and unblock their accounts if the AI makes a mistake.

# Task 8: Final Solution Summary

## AI Solution Summary: 

- Suspicious Transaction Detection Problem:

    - Existing rule-based fraud detection systems generate too many false positives, overwhelming analysts, inflating manual processing hours, and delaying legitimate customer transactions.

- Proposed AI Solution:
    - Implement an Anomaly Detection and Classification system to score the risk of transactions in real-time, automating blocks for high-risk activity and routing medium-risk cases to humans.

- Required Data: 
    - Millions of structured historical transaction records containing features like amount, location, merchant category, and device IP, labeled with previous fraud outcomes.

- Model Recommendation: 
    - A Feed-forward Neural Network for supervised classification of known fraud patterns, supplemented by an Autoencoder to detect novel anomalies.

- Expected Business Impact: 
    - A drastic reduction in manual_processing_hours (targeting a drop from ~500 hrs/month to <200 hrs/month) and average_resolution_time_hours for fraud cases, alongside an overall boost in investigation efficiency and customer satisfaction.

- Risks and Mitigation Plan: 

    - Risk: Model falsely flags legitimate users, causing frustration.

    - Mitigation: Implement real-time SMS/Email validation allowing users to instantly override a block by verifying the purchase. Continuously audit model outcomes across different geographic regions to prevent localized bias.
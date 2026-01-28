# Chapter 3 – Hard Scenario-Based MCQs  
## Managing Risks of Generative AI in Software Testing

Each question includes:
- ✅ Correct answer  
- 📘 Explanation  
- 📌 Syllabus section reference from Chapter 3 of the ISTQB CT-GenAI syllabus

---

### Q1  
An LLM generates convincing but incorrect test cases that assume invalid acceptance criteria. Testers discover this after execution. Which risk type does this BEST represent?

A. Data privacy risk  
B. Hallucination  
C. Environmental impact  
D. Algorithmic audit failure  

**✅ Answer: B**  
📘 *Explanation:* Hallucinations are when an LLM produces factually incorrect or irrelevant outputs for the given task, such as fictitious or invalid test cases.  
📌 *Section Reference:* 3.1 Hallucinations, Reasoning Errors and Biases – Hallucinations :contentReference[oaicite:1]{index=1}

---

### Q2  
A tester notices that an LLM incorrectly prioritizes test cases due to misinterpreting cause-and-effect dependencies in requirements. What risk category does this illustrate?

A. Regulatory non-compliance  
B. Data breach  
C. Reasoning error  
D. Non-deterministic emissions  

**✅ Answer: C**  
📘 *Explanation:* Reasoning errors occur when LLMs misinterpret logical structures like conditional logic or cause-effect relationships.  
📌 *Section Reference:* 3.1 Hallucinations, Reasoning Errors and Biases – Reasoning errors :contentReference[oaicite:2]{index=2}

---

### Q3  
During analysis of AI-generated test scripts, outputs disproportionately focus on specific UI locales due to the training data skew. What risk is this?

A. Energy consumption risk  
B. Bias  
C. Hallucination  
D. Data privacy breach  

**✅ Answer: B**  
📘 *Explanation:* Bias in LLMs originates from skewed training data patterns, leading to outputs that favour certain information or assumptions.  
📌 *Section Reference:* 3.1 Hallucinations, Reasoning Errors and Biases – Biases :contentReference[oaicite:3]{index=3}

---

### Q4  
An organization uses ChatOps to generate test data and accidentally includes production customer PII in prompts. Which risk category is MOST relevant?

A. Regulatory standards risk  
B. Data privacy and security risk  
C. Hallucination risk  
D. Energy consumption risk  

**✅ Answer: B**  
📘 *Explanation:* Handling sensitive information in GenAI prompts and outputs creates data privacy and security risks such as unauthorized exposure of PII.  
📌 *Section Reference:* 3.2 Data Privacy and Security Risks of Generative AI in Software Testing :contentReference[oaicite:4]{index=4}

---

### Q5  
Which mitigation strategy directly reduces unauthorized access to sensitive data in LLM outputs?

A. Using larger models  
B. Token-level masking and access controls  
C. Increasing prompt length  
D. Disabling human review  

**✅ Answer: B**  
📘 *Explanation:* Masking, access controls, and secure data handling limit exposure of sensitive data and improve privacy/security in GenAI use.  
📌 *Section Reference:* 3.2 Data Privacy and Security Risks – Mitigation strategies :contentReference[oaicite:5]{index=5}

---

### Q6  
A test team finds that identical prompts produce different LLM-generated expected results across runs. What underlying characteristic of LLMs should testers consider?

A. Hallucination certainty  
B. Data privacy controls  
C. Non-determinism  
D. Bias amplification  

**✅ Answer: C**  
📘 *Explanation:* The non-deterministic nature of LLMs can produce varying outputs for the same input, complicating reproducibility.  
📌 *Section Reference:* 3.1 Hallucinations, Reasoning Errors and Biases – Non-deterministic behavior :contentReference[oaicite:6]{index=6}

---

### Q7  
A GenAI system used for test reporting generates detailed analytics but consumes disproportionate compute with each query. Which risk dimension does this reflect?

A. Energy consumption and environmental impact  
B. Hallucination intensity  
C. Security vulnerability  
D. Regulatory reporting risk  

**✅ Answer: A**  
📘 *Explanation:* High compute use and its resultant energy consumption contribute to environmental impact concerns for Generative AI.  
📌 *Section Reference:* 3.3 Energy Consumption and Environmental Impact of Generative AI in Software Testing :contentReference[oaicite:7]{index=7}

---

### Q8  
Which is a test organization’s obligation regarding AI outputs when operating under international data protection regulations?

A. Masking irrelevant fields  
B. Logging every token generated  
C. Ensuring outputs never include any data  
D. Auditing data flows for compliance  

**✅ Answer: D**  
📘 *Explanation:* Compliance with privacy regulations requires auditing and controlling data flows, especially when Generative AI processes sensitive data.  
📌 *Section Reference:* 3.2 Data Privacy and Security Risks / 3.4 AI Regulations, Standards, and Best Practices :contentReference[oaicite:8]{index=8}

---

### Q9  
An LLM-assisted testing tool suggests using deprecated APIs in test scripts. What type of risk is this?

A. Environmental risk  
B. Hallucination  
C. Regulatory compliance risk  
D. Energy inefficiency  

**✅ Answer: B**  
📘 *Explanation:* Suggesting outdated or incorrect API use is a form of hallucination—data that appears plausible but is incorrect relative to the system context.  
📌 *Section Reference:* 3.1 Hallucinations, Reasoning Errors and Biases – Hallucinations :contentReference[oaicite:9]{index=9}

---

### Q10  
Seeing an LLM repeatedly misprioritize security test scenarios because of language distribution in training data illustrates which risk?

A. Security vulnerability  
B. Reasoning error  
C. Bias  
D. Data breach  

**✅ Answer: C**  
📘 *Explanation:* Training data bias can lead to outputs that underrepresent certain kinds of tests (e.g., security), reflecting bias rather than logical error.  
📌 *Section Reference:* 3.1 Hallucinations, Reasoning Errors and Biases – Biases :contentReference[oaicite:10]{index=10}

---

### Q11  
A tester finds an LLM claims regulatory compliance for a test implementation task without checking standards. What best practices should mitigate this?

A. Ignore the claim  
B. Human verification + referring to formal regulations  
C. Use larger LLMs  
D. Add more training data  

**✅ Answer: B**  
📘 *Explanation:* Human review and alignment with formal regulatory frameworks is essential to validate claims made by GenAI, particularly under 3.4.  
📌 *Section Reference:* 3.4 AI Regulations, Standards and Best Practice Frameworks :contentReference[oaicite:11]{index=11}

---

### Q12  
Which approach directly helps detect hallucinations and reasoning errors during automated test output generation?

A. Increase temperature hyperparameter  
B. Automated verification of outputs against authoritative data  
C. Reduce prompt length  
D. Remove human-in-the-loop  

**✅ Answer: B**  
📘 *Explanation:* Automated verification against known, authoritative test data or specifications helps catch hallucinations or logical errors.  
📌 *Section Reference:* 3.1 Identify Hallucinations, Reasoning Errors and Biases in LLM Output :contentReference[oaicite:12]{index=12}

---

### Q13  
Which concept is essential to include in a risk mitigation policy for GenAI used in testing?

A. Prompt complexity guidelines  
B. Formal metrics for evaluating model energy consumption  
C. Structured data validation rules  
D. Automatic removal of all AI outputs  

**✅ Answer: C**  
📘 *Explanation:* Structured validation and verification rules are core to mitigating risks from incorrect or unsafe AI outputs.  
📌 *Section Reference:* 3.1 & 3.2 Risk Mitigation :contentReference[oaicite:13]{index=13}

---

### Q14  
A team must justify to stakeholders the environmental impact of their GenAI usage. Which measurement should they consider?

A. Number of tokens generated per test  
B. CO₂ emissions or energy consumption per task  
C. Accuracy rate of test outputs  
D. Number of hallucinations per session  

**✅ Answer: B**  
📘 *Explanation:* Assessing energy consumption or CO₂ equivalents per task is central to measuring environmental impact.  
📌 *Section Reference:* 3.3 Energy Consumption and Environmental Impact of Generative AI in Software Testing :contentReference[oaicite:14]{index=14}

---

### Q15  
An organization adopts an AI policy requiring that GenAI tools used for testing respond with traceable reasoning. Which syllabus topic does this MOST directly support?

A. Data privacy and security  
B. Mitigating reasoning errors  
C. Energy-efficient test generation  
D. Agent orchestration  

**✅ Answer: B**  
📘 *Explanation:* Ensuring traceable reasoning supports detection and mitigation of reasoning errors in output, reducing risk.  
📌 *Section Reference:* 3.1 Hallucinations, Reasoning Errors and Biases :contentReference[oaicite:15]{index=15}

---

## Exam Strategy Tip

> For Chapter 3, focus on **recognizing, identifying, and mitigating risks**: hallucinations, reasoning errors, biases, privacy/security implications, environmental impact, and regulatory compliance — and how to **operationalize detection and controls**. :contentReference[oaicite:16]{index=16}


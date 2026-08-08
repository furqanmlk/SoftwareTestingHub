# ISTQB® CT-GenAI v1.0  
# Chapter 03 – Quick Review Sheet  
Managing Risks of Generative AI in Software Testing

---

# 1️⃣ Hallucinations, Reasoning Errors & Biases

## Hallucinations
Definition: AI generates fabricated or incorrect information presented as fact.

Examples in Testing:
- Invented API endpoints
- Fake requirement IDs
- Non-existent SQL columns

How to Detect:
- Cross-check with requirements
- Validate against documentation
- SME review

Mitigation:
- Retrieval-Augmented Generation (RAG)
- Require citations
- Human-in-the-loop validation

---

## Reasoning Errors
Definition: Incorrect logical or mathematical conclusions.

Examples:
- Missing boundary conditions
- Wrong discount calculation
- Invalid assumptions

Detection:
- Ask for step-by-step reasoning
- Manual verification
- Compare multiple outputs

Mitigation:
- Chain-of-Thought prompting
- Structured input format
- Explicit validation steps

---

## Bias
Definition: Systematic unfair favoritism caused by training data.

Examples:
- Gender-based assumptions
- Limited accessibility coverage

Detection:
- Test demographic variations
- Compare outputs for neutrality

Mitigation:
- Diverse datasets
- Bias audits
- Neutral prompt instructions

---

# 2️⃣ Non-Deterministic Behavior

LLMs may produce different outputs for the same prompt.

Causes:
- Random sampling
- Temperature settings
- Token probability distribution

Mitigation:
- Set temperature = 0
- Fix random seed (if available)
- Version control prompts
- Log outputs
- Snapshot testing

Exam Tip:
Non-determinism ≠ hallucination

---

# 3️⃣ Data Privacy & Security Risks

## Key Risks
- Data leakage
- Prompt injection
- Model inversion attacks
- Exposure of secrets
- Unauthorized retention

Testing Risk Example:
Uploading production database to public AI tool.

---

## Vulnerabilities in Testing Tools
- Hardcoded API keys
- Proprietary code in prompts
- Shadow AI usage
- CI/CD AI without governance

---

## Mitigation

Technical Controls:
- Data anonymization
- Token masking
- Encryption
- On-prem deployment
- Role-based access

Process Controls:
- AI usage policy
- Vendor risk assessment
- Secure prompt guidelines

---

# 4️⃣ Energy & Environmental Impact

Why It Matters:
- Large model training consumes high GPU power
- Cloud inference increases CO₂ footprint
- Data center cooling costs

Testing Best Practices:
- Avoid unnecessary prompts
- Use smaller models when possible
- Optimize prompt efficiency
- Evaluate cost vs benefit

Exam Insight:
Environmental impact is a governance consideration.

---

# 5️⃣ Regulations & Frameworks

## EU AI Act
- Risk-based classification
- High-risk AI requires compliance documentation

## NIST AI Risk Management Framework (AI RMF)
- Identify risks
- Measure impact
- Manage continuously

## ISO Standards
- ISO/IEC 23894 – AI Risk Management
- ISO/IEC 42001 – AI Management System
- ISO 27001 – Information Security

## GDPR
- Protects personal data
- Applies to AI-generated processing

---

# 🔥 High-Probability Exam Areas

- Difference between hallucination and reasoning error
- Mitigation of non-deterministic behavior
- Prompt injection definition
- RAG as hallucination mitigation
- Privacy risks when using public AI tools
- Risk-based AI regulation concept
- Human-in-the-loop governance

---

# ⚡ 30-Second Recall Map

Hallucination → Fake facts → Use RAG  
Reasoning error → Logic mistake → Chain-of-Thought  
Bias → Unfair output → Diverse data & audit  
Non-determinism → Different outputs → Lower temperature  
Privacy risk → Data leakage → Anonymize & encrypt  
Environmental impact → High energy → Optimize usage  
Regulation → Risk-based compliance → EU AI Act / NIST

---

# End of Quick Review Sheet

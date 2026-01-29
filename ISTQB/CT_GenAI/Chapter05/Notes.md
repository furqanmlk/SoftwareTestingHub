# Chapter 5 – Deploying and Integrating Generative AI in Test Organizations  
**ISTQB CT-GenAI | Duration: 80 minutes**

---

## 5.1 Roadmap for the Adoption of Generative AI in Software Testing

A roadmap defines how an organization **plans, governs, adopts, scales, and sustains** the use of Generative AI in software testing while managing risks and ensuring value.

---

### 5.1.1 Risks of Shadow AI

**Shadow AI** is the use of AI tools by individuals or teams **without organizational approval, governance, or visibility**.

#### Key Risks
- **Data leakage**: Sensitive test or production data exposed to public AI tools.
- **Compliance violations**: Breach of regulations (e.g., data protection laws).
- **Inconsistent quality**: Different tools and prompts produce unreliable outputs.
- **Lack of auditability**: No traceability of prompts, decisions, or outputs.
- **Security risks**: Prompt injection, misuse, or exposure of internal logic.

**Example**  
A tester uploads real customer defect logs into a public AI chatbot to generate test cases, creating **privacy and compliance risks**.

---

### 5.1.2 Key Aspects of a Generative AI Strategy in Software Testing

A Generative AI strategy ensures **controlled, ethical, and value-driven adoption**.

#### Key Aspects
- **Governance**: Approved tools, access control, usage policies.
- **Risk management**: Managing hallucinations, bias, and incorrect outputs.
- **Security and privacy**: Data masking, anonymization, secure environments.
- **Ethics and compliance**: Responsible and fair AI usage.
- **Value alignment**: Clear testing goals (coverage, efficiency, quality).
- **Human oversight**: Testers remain accountable for outcomes.

**Example**  
AI-generated test cases must be **reviewed and approved by a human tester** before use.

---

### 5.1.3 Selecting LLMs / SLMs for Software Test Tasks

Different models suit different testing needs.

#### Selection Criteria
- **Task suitability**: Test analysis, design, data generation, automation support.
- **Model size**:
  - **LLMs**: Complex reasoning and exploratory support.
  - **SLMs**: Faster, cheaper, domain-specific tasks.
- **Accuracy and reliability**
- **Latency and cost**
- **Deployment model**: Cloud vs on-premises.
- **Security and compliance**: Data residency and retention.

**Example**  
An SLM trained on internal APIs is used for regression test generation to improve **security and performance**.

---

### 5.1.4 Phases when Adopting Generative AI in Software Testing

Adoption occurs in **progressive phases**.

1. **Exploration**
   - Pilots and experiments.
   - Low-risk use cases (e.g., test ideas).
2. **Controlled Adoption**
   - Governance and approved tools introduced.
3. **Integration**
   - AI embedded into test processes and CI/CD.
4. **Optimization and Scaling**
   - Reusable prompts, agents, RAG systems.
5. **Continuous Improvement**
   - Monitoring, feedback, and model updates.

**Example**  
A team starts with AI-generated test ideas and later integrates AI into automated regression pipelines.

---

## 5.2 Manage Change when Adopting Generative AI for Software Testing

Change management addresses **people, skills, processes, and culture**.

---

### 5.2.1 Essential Skills and Knowledge for Testing with Generative AI

Testers need new competencies to use AI effectively.

#### Essential Skills
- **AI literacy**: Understanding strengths and limitations.
- **Prompt engineering**: Writing effective prompts.
- **Critical thinking**: Detecting hallucinations and reasoning errors.
- **Domain knowledge**: Validating outputs against requirements.
- **Ethical awareness**: Bias and responsible use.
- **Data handling**: Secure and compliant usage.

**Example**  
A tester reviews AI-generated test cases and removes invalid ones caused by hallucinations.

---

### 5.2.2 Building Generative AI Capabilities in Test Teams

Organizations must enable teams, not just provide tools.

#### Capability-Building Activities
- Training and workshops.
- AI usage guidelines and best practices.
- Shared prompt libraries.
- Communities of practice.
- Collaboration with developers and data teams.
- Continuous learning and mentoring.

**Example**  
A team maintains a shared repository of **validated prompts** for API and regression testing.

---

### 5.2.3 Evolving Test Processes in AI-Enabled Test Organizations

Generative AI changes **how testing is performed**.

#### Process Evolution
- Shift from manual creation to AI-assisted generation.
- Increased focus on review, validation, and risk analysis.
- Testers act as **AI supervisors and quality gatekeepers**.
- Continuous feedback loops to improve AI outputs.
- Integration with DevOps and CI/CD pipelines.

**Example**  
AI generates exploratory test ideas, while testers focus on **risk prioritization and defect analysis**.

---

## Exam Pointers – Chapter 5
- Shadow AI = unauthorized and unmanaged AI usage.
- Strategy includes governance, ethics, and risk management.
- LLM vs SLM choice depends on task, cost, and security.
- Adoption is phased, not immediate.
- Human testers remain accountable.
- AI changes roles and processes, not responsibility.

---

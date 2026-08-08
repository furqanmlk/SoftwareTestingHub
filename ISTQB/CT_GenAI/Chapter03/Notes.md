# Exam Notes: Managing Risks of Generative AI in Software Testing
**Based on ISTQB® Certified Tester Specialist Level Syllabus – Testing with Generative AI (v1.0)**
**Covering Pages 34–41**

---

## 3. Managing Risks of Generative AI in Software Testing

### 3.1 Hallucinations, Reasoning Errors and Biases
Generative AI (GenAI) models, particularly Large Language Models (LLMs), are prone to specific defects that affect the quality of testware. The non-deterministic nature of LLMs makes fixing these defects difficult, as errors may disappear and reappear in different conversations [1], [2].

#### 3.1.1 Hallucinations, Reasoning Errors and Biases in Generative AI
*   **Hallucinations:** The LLM generates factually incorrect or irrelevant output [2].
    *   *Example:* Creating fictitious test cases, suggesting non-existent acceptance criteria, or generating non-functioning test scripts [2].
*   **Reasoning Errors:** Generative AI may produce outputs that contain flawed logic, invalid assumptions, or incorrect causal relationships, even when the text sounds coherent.
                          These errors are not necessarily “made-up facts” (hallucinations); they can be wrong conclusions derived from seemingly valid inputs.
    *  *Example:* (Testing Context): A model reviews a defect report and concludes the root cause is a “database issue” because a timeout appears in logs, but the real cause is a missing retry mechanism or rate limiting at the API gateway. The model’s conclusion is plausible but logically incorrect. [3].

*   **Biases:** Skewed outputs resulting from the data used to train the model, favoring certain information or assumptions [4].
    *   *Example:* AI generates test data biased toward Western names, formats, or usage patterns. [4].

#### 3.1.2 Identify Hallucinations, Reasoning Errors and Biases in LLM Output
Testers must employ detection methods through review or automated verification [5].

### Detection Overview (DM Format)

| Risk Type | Meaning (Easy Wording) | Detection Method | Example |
|---------|------------------------|------------------|---------|
| **Hallucinations** | AI creates information that is not real or not present in the system | Cross-verification against requirements and documentation | AI generates a test case for a feature that does not exist |
| | | Validation by subject matter experts (SMEs) | Business analyst confirms the workflow is incorrect |
| | | Consistency checks across outputs | One test says login is mandatory, another says optional |
| **Reasoning Errors** | AI uses incorrect logic even when facts look correct | Logical validation of steps and conclusions | AI assumes database failure without evidence |
| | | Output testing by executing generated tests or scripts | Automation script fails due to flawed logic |
| **Biases** | AI output is unbalanced and misses certain scenarios | Review of synthetic test data representation | Test data includes only one country or user group |
| | | Review of test type coverage | Functional tests generated, but no non-functional tests |


#### 3.1.3 Mitigation Techniques of GenAI Hallucinations, Reasoning Errors and Biases
Strategies to minimize risks when prompts are poorly designed or context is missing include [8]:
*   **Complete Context:** Ensure the prompt has all relevant information to guide accuracy [9].
*   **Prompt Segmentation:** Use **Prompt Chaining** to break complex prompts into smaller steps, verifying the output of each step [9].
*   **Clear Data Formats:** Use structured formats that are easy for the model to interpret [9].
*   **Model Selection:** Use an LLM specifically trained for the task [9].
*   **Model Comparison:** Run the same prompt on multiple models to compare results and detect errors [9].

#### 3.1.4 Mitigation of Non-Deterministic Behavior of LLMs
LLMs are probabilistic, meaning the same input can yield different outputs. This makes reproducibility difficult [10].
*   **Temperature Adjustment:** Lower the temperature setting during inference to narrow the probability distribution. This reduces randomness and improves consistency, though it limits creativity [11].
*   **Random Seeds:** Set a seed value for the random number generator to ensure the same pseudo-random sequence is used [11].

---

### 3.2 Data Privacy and Security Risks of Generative AI in Software Testing
Using GenAI introduces risks regarding the handling of sensitive info and vulnerabilities in the test infrastructure [12].

#### 3.2.1 Data Privacy and Security Risks Associated with Using Generative AI
*   **Privacy Concerns:**
    *   **Unintentional Exposure:** Accidental revelation of sensitive info in outputs [13].
    *   **Lack of Control:** Processing/storing data without user consent [13].
    *   **Compliance Risks:** Violating regulations like GDPR [13].
*   **Security Risks:**
    *   Vulnerabilities in the LLM infrastructure allowing data breaches [14].
    *   Malicious actors exploiting LLMs to alter behavior or extract data [14].
    *   Attackers introducing malicious input data [14].

#### 3.2.2 Data Privacy and Vulnerabilities in Generative AI for Test Processes and Tools
*   **Data Exfiltration:** Sending requests to extract confidential training data [15].
    *   *Example:* Overloading the context window to force the AI to reveal random snippets of training data [15].
*   **Request Manipulation:** Introducing data that disrupts output [15].
    *   *Example:* Using images to trick the AI into a different context, causing hallucinations on acceptance criteria [15].
*   **Data Poisoning:** Manipulating the training data itself [16].
    *   *Example:* Providing fake evaluations for AI-generated test reports [16].
*   **Malicious Code Generation:** Manipulating the LLM to create backdoors [16].
    *   *Example:* Generating code that opens a communication channel to a malicious IP address [16].

#### 3.2.3 Mitigation Strategies to Protect Data Privacy and Enhance Security
*   **Data Measures:**
    *   **Data Minimization:** Only use necessary non-sensitive data [17].
    *   **Anonymization/Pseudonymization:** Mask or replace sensitive info [17].
    *   **Secure Storage:** Implement encryption and access controls [17].
*   **Organizational & Technical Measures:**
    *   **Training:** Establish policies and training for responsible use [17].
    *   **Human Review:** Systematically review generated output [18].
    *   **Environment Choice:** Choose secure environments (e.g., secure cloud, on-premise infrastructure) based on confidentiality needs [18].
    *   **Security Audits:** Regular vulnerability assessments [18].
*   **Key Stakeholders:** Involve Security Engineers, Legal Counsel, CTO, or CISO in the strategy [19].

---

### 3.3 Energy Consumption and Environmental Impact of Generative AI in Software Testing
Training and processing LLMs require massive computing resources, impacting energy consumption [20].

#### 3.3.1 The Impact of Using GenAI on Energy Consumption and CO2 Emissions
*   **Usage vs. Energy:** Energy consumption rises sharply with usage volume and task complexity [20].
    *   *Example:* Generating one image with a powerful model can consume as much energy as fully charging a smartphone [20].
*   **Cumulative Impact:** While a single text generation task is negligible, the collective effect of millions of users creates significant CO2 emissions [21].
*   **Best Practice:** Limit unnecessary model interactions to mitigate environmental risks [21].

---

### 3.4 AI Regulations, Standards, and Best Practice Frameworks
Organizations must align with standards to address risks like reasoning errors, privacy, and environmental impact [22].

#### 3.4.1 AI Regulations, Standards and Frameworks Relevant to GenAI in Software Testing
*   **ISO/IEC 42001:2023 (Standard):** Specifies requirements for managing AI systems to ensure consistency and reliability [23].
*   **ISO/IEC 23053:2022 (Standard):** A framework for AI systems using Machine Learning; focuses on data quality, transparency, and fault tolerance [24].
*   **EU AI Act (Regulation):** A legal framework classifying AI by risk level; mandates compliance in transparency, accountability, and bias mitigation [24].
*   **NIST AI Risk Management Framework (US):** Guidelines for managing AI risks with a focus on fairness, transparency, and security (e.g., preventing biased results) [25].

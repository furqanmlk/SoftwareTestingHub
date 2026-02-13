# Chapter 2 – Quick Revision Sheet  
## Prompt Engineering for Effective Software Testing  
(ISTQB CT-GenAI – Pages 19–32)

---

# 2. Prompt Engineering for Effective Software Testing

Core Idea:
Prompt quality → Output quality  
GenAI is non-deterministic → Must evaluate and refine

---

# 2.1 Effective Prompt Development

Effective prompts:
- Reduce ambiguity
- Improve consistency
- Increase reliability
- Minimize hallucinations

Poor prompts cause:
- Missing test cases
- Irrelevant outputs
- Incorrect assumptions
- Rework

---

## 2.1.1 Structure of Prompts for Generative AI in Software Testing

Six Components (Memorize Order):

1. Role  
2. Context  
3. Instruction  
4. Input Data  
5. Constraints  
6. Output Format  

Quick Memory Tip:
RCIICO → Role, Context, Instruction, Input, Constraints, Output

Example Structure:

Role → Act as Test Analyst  
Context → Online banking login feature  
Instruction → Generate negative test cases  
Input Data → Requirements text  
Constraints → Use boundary value analysis  
Output Format → Table with 5 columns  

Exam Focus:
More structure = Higher output quality

---

## 2.1.2 Core Prompting Techniques for Software Testing

| Technique | Best Used For | Key Benefit |
|------------|---------------|-------------|
| Zero-shot | Simple tasks | Fast execution |
| Few-shot | Repetitive/format-heavy tasks | Consistency |
| Prompt Chaining | Complex multi-step tasks | Precision & reviewability |
| Meta Prompting | Improving prompts | Better prompt quality |

Exam Clues:
- Complex task → Prompt chaining
- Strict format needed → Few-shot
- Not sure how to write prompt → Meta prompting

---

## 2.1.3 System Prompt and User Prompt

System Prompt:
- Sets behavior & boundaries
- Persistent for session
- Controls how AI behaves

User Prompt:
- Task-specific instruction
- Changes per request
- Controls what AI does

Exam Memory:
System = Behavior  
User = Task  

---

# 2.2 Applying Prompt Engineering Techniques to Software Test Tasks

GenAI supports full testing lifecycle.

---

## 2.2.1 Test Analysis with Generative AI

Used for:
- Requirement ambiguity detection
- Test condition generation
- Risk prioritization
- Coverage analysis
- Technique suggestion

Exam Trigger:
“Ambiguous requirement” → Test Analysis

---

## 2.2.2 Test Design and Test Implementation with Generative AI

Used for:
- Test case generation
- Test data synthesis
- Automation script creation
- Scheduling optimization

Exam Trigger:
“Generate test scripts” → Test Design/Implementation

---

## 2.2.3 Automated Regression Testing with Generative AI

Used for:
- Impact analysis
- Self-healing tests
- Keyword-driven scripts
- Defect reporting

Exam Trigger:
“After code change” → Regression + Impact Analysis

---

## 2.2.4 Test Monitoring and Test Control with Generative AI

Used for:
- Metrics analysis
- Trend detection
- Risk prediction
- Stakeholder reporting

Exam Trigger:
“Analyze defect density trend” → Monitoring & Control

---

## 2.2.5 Choosing Prompting Techniques for Software Testing

| Scenario | Best Technique |
|-----------|----------------|
| Multi-step logical task | Prompt Chaining |
| Strict formatted output | Few-shot |
| Designing new prompt | Meta Prompting |
| Simple quick task | Zero-shot |

No single best technique for all tasks.

---

# 2.3 Evaluate Generative AI Results and Refine Prompts

GenAI is non-deterministic  
→ Must evaluate  
→ Must refine  
→ Continuous improvement cycle

---

## 2.3.1 Metrics for Evaluating GenAI Results

| Metric | What It Measures |
|---------|------------------|
| Accuracy | Overall correctness |
| Precision | Within requested scope |
| Recall | Coverage completeness |
| Relevance | Context alignment |
| Diversity | Variation without duplication |
| Execution Success Rate | Scripts run without errors |
| Time Efficiency | Productivity gain |

Exam Trap: Precision vs Recall

Precision → Only what was requested  
Recall → Everything that was required  

---

## 2.3.2 Techniques for Evaluating and Iteratively Refining Prompts

| Technique | Purpose |
|------------|----------|
| Iterative Modification | Add clarity gradually |
| A/B Testing | Compare prompt versions |
| Output Analysis | Study failure patterns |
| User Feedback | Improve usability |
| Adjusting Specificity | Tune detail level |

---

# Continuous Improvement Flow (Memorize)

1. Generate  
2. Evaluate  
3. Identify weakness  
4. Refine prompt  
5. Regenerate  

Repeat.

---

# High-Probability Exam Triggers

If question mentions:
- Coverage gaps → Recall  
- Out-of-scope output → Precision  
- Duplicate tests → Diversity  
- Wrong expected result → Accuracy  
- Script fails in CI/CD → Execution Success Rate  
- Faster than manual → Time Efficiency  

---

# Final Memory Anchor

Structure prompts correctly  
Choose right technique  
Evaluate outputs  
Refine iteratively  

Prompt engineering = Control + Evaluate + Improve

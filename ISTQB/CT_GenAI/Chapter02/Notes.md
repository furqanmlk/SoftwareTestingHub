# Chapter 2 – Prompt Engineering for Effective Software Testing

**Based on ISTQB® Certified Tester Specialist Level Syllabus – Testing with Generative AI (v1.0)**  
**Coverage: Sections 2 → 2.3.2 (Pages 19–32)**

---

# 2. Prompt Engineering for Effective Software Testing

Prompt engineering is the practice of designing, structuring, and refining prompts so that Generative AI produces accurate, relevant, and usable outputs for software testing tasks.

Well-designed prompts:
- Reduce ambiguity
- Improve consistency
- Increase reliability of AI-generated results
- Minimize hallucinations

---

## 2.1 Effective Prompt Development

Effective prompt development ensures that Generative AI clearly understands:
- The testing context
- The intended task
- The required output format
- Any constraints or limitations

Because Generative AI responds strictly to the instructions given, unclear prompts may lead to incomplete or misleading results.

---

### 2.1.1 Structure of Prompts for Generative AI in Software Testing

A structured prompt generally includes **six key components**:

1. **Role**  
   Defines the persona the AI should adopt (e.g., "Act as a Test Analyst").

2. **Context**  
   Provides background information (e.g., system under test, domain, assumptions).

3. **Instruction**  
   Specifies the task to be performed (e.g., "Generate boundary value test cases").

4. **Input Data**  
   Supplies the necessary information (e.g., user stories, requirements, logs, code).

5. **Constraints**  
   Defines rules or limitations (e.g., specific test techniques, compliance rules).

6. **Output Format**  
   Specifies how the response should be structured (e.g., table, Gherkin syntax, JSON).

**Exam Focus:**  
Not all prompts require all six components, but including more components improves clarity and output quality.

---

### 2.1.2 Core Prompting Techniques for Software Testing

Core prompting techniques help improve output quality depending on task complexity.

#### Zero-shot Prompting
- No examples provided.
- Relies on model’s general knowledge.
- Suitable for simple tasks.

#### Few-shot Prompting
- Provides one or more examples.
- Improves consistency and formatting.
- Useful for repetitive or structured tasks.

#### Prompt Chaining
- Breaks complex tasks into multiple sequential prompts.
- Output of one step becomes input for the next.
- Improves accuracy and reviewability.

#### Meta Prompting
- AI helps create or refine prompts.
- Useful when tester is unsure how to craft the best prompt.
- Enhances efficiency and collaboration.

---

### 2.1.3 System Prompt and User Prompt

#### System Prompt
- Sets overall behavior, personality, and boundaries.
- Typically defined at session level.
- Often hidden from end users.

Example:  
"You are a QA assistant. Follow ISTQB terminology."

#### User Prompt
- Specific instruction for a single interaction.
- Changes dynamically per request.

Example:  
"Generate equivalence partitioning test cases for the age field."

**Exam Focus:**  
System prompt controls behavior; user prompt controls task.

---

## 2.2 Applying Prompt Engineering Techniques to Software Test Tasks

Generative AI can support multiple testing activities across the lifecycle.

High-quality input is essential for meaningful output.

---

### 2.2.1 Test Analysis with Generative AI

Supports:
- Defect identification in requirements
- Test condition generation
- Risk-based prioritization
- Coverage gap detection
- Technique selection

---

### 2.2.2 Test Design and Test Implementation with Generative AI

Supports:
- Test case generation
- Test data synthesis
- Automated script generation
- Scheduling and prioritization

---

### 2.2.3 Automated Regression Testing with Generative AI

Supports:
- Keyword-driven script generation
- Impact analysis after code changes
- Self-healing tests
- Defect report generation

---

### 2.2.4 Test Monitoring and Test Control with Generative AI

Supports:
- Metrics analysis
- Trend detection
- Risk prediction
- Stakeholder reporting
- Test reprioritization insights

---

### 2.2.5 Choosing Prompting Techniques for Software Testing

Different techniques fit different scenarios:

- **Prompt Chaining** → Complex tasks requiring precision
- **Few-shot Prompting** → Repetitive tasks with strict formatting
- **Meta Prompting** → Crafting or refining new prompts

No single prompting technique is best for all situations.

---

## 2.3 Evaluate Generative AI Results and Refine Prompts

Generative AI is **non-deterministic**, meaning the same prompt can produce different outputs at different times.

Therefore:
- Outputs must be evaluated.
- Weak outputs must be improved.
- Prompts must be refined iteratively.

Evaluation ensures AI-generated test artifacts are:
- Correct
- Complete
- Usable
- Reliable

Prompt engineering is not a one-time action — it is a continuous improvement process.

---

## 2.3.1 Metrics for Evaluating GenAI Results

The following metrics help determine whether AI outputs are acceptable for testing tasks.

---

### Accuracy
**Definition:** Correctness compared to a reference standard or expert review.

**Example:**  
If AI generates 20 test cases and 3 have incorrect expected results, accuracy is reduced.

**In practice:**  
Compare AI-generated test cases with:
- Requirement specifications
- Expert-written test cases
- Known correct outputs

---

### Precision
**Definition:** Correctness for a specific objective.

**Example:**  
If the task is to generate only *negative test cases*, but the AI generates both positive and negative cases, precision is low.

Precision focuses on:
- Staying within scope
- Producing exactly what was requested

---

### Recall
**Definition:** Coverage of all relevant cases.

**Example:**  
If testing an age field (valid range 18–60), but the AI misses boundary values (18 and 60), recall is incomplete.

Recall measures:
- Did the AI include all required test conditions?
- Were edge cases covered?

---

### Relevance
**Definition:** Appropriateness to the given context.

**Example:**  
If generating test cases for a banking system, but AI suggests gaming-related test scenarios, relevance is low.

Relevance checks:
- Domain alignment
- Feature alignment
- Business logic alignment

---

### Diversity
**Definition:** Coverage of varied scenarios without unnecessary repetition.

**Example:**  
If AI generates 15 login test cases but 10 are slightly reworded duplicates, diversity is low.

Diversity ensures:
- Edge cases are included
- Different paths are explored
- Redundant cases are minimized

---

### Execution Success Rate
**Definition:** Percentage of generated scripts that run without syntax or runtime errors.

**Example:**  
If AI generates 10 automation scripts and 3 fail due to syntax errors, execution success rate is 70%.

This is especially important for:
- Automated script generation
- CI/CD pipeline integration

---

### Time Efficiency
**Definition:** Time saved compared to manual effort.

**Example:**  
If manual test design takes 3 hours and AI-assisted design takes 45 minutes (including review), time efficiency is high.

Time efficiency must include:
- Generation time
- Review time
- Correction time

---

## 2.3.2 Techniques for Evaluating and Iteratively Refining Prompts

When outputs are weak, prompts must be refined systematically.

---

### Iterative Modification
Gradually improve the prompt by:
- Adding missing context
- Clarifying scope
- Specifying techniques

**Example:**

Initial prompt:  
"Generate test cases for login."

Improved prompt:  
"Generate boundary value and negative test cases for the login screen. Use a table format with columns: Test ID, Preconditions, Steps, Expected Result."

Result: Higher clarity → better output.

---

### A/B Testing
Compare two different prompts and evaluate which produces better results based on metrics.

**Example:**

Prompt A:  
"Generate test cases for age field."

Prompt B:  
"Generate boundary value and equivalence partitioning test cases for age field (valid range 18–60)."

Evaluate:
- Which has better recall?
- Which has higher precision?
- Which requires less correction?

---

### Output Analysis
Analyze common failure patterns.

Common issues:
- Missing boundary values
- Hallucinated requirements
- Duplicate test cases
- Incorrect assumptions

Refine prompt to prevent recurrence.

**Example:**  
If AI assumes password rules not mentioned in requirements, add:  
"Do not assume rules not explicitly provided."

---

### User Feedback
Collect feedback from testers on:
- Clarity
- Usability
- Completeness
- Practical value

Refine prompts based on:
- Real-world usage
- Team experience

---

### Adjusting Specificity
Experiment with prompt detail level.

Sometimes:
- More context improves accuracy.
- Too much detail restricts creativity.
- Too little detail causes hallucination.

**Example:**

Too vague:  
"Generate tests."

Too restrictive:  
"Generate exactly 12 test cases using only BVA with no additional edge cases."

Balanced:  
"Generate boundary value and negative test cases covering normal and edge scenarios."

---

## Continuous Improvement Cycle

1. Generate output  
2. Evaluate using metrics  
3. Identify weaknesses  
4. Refine prompt  
5. Re-generate improved output  

Prompt engineering is an ongoing improvement cycle.

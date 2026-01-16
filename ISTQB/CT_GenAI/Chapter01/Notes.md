# ISTQB CT-GenAI – Chapter 1 Notes  
**Syllabus Version:** CT-GenAI v1.0  
**Pages Covered:** 13–18  
**Knowledge Levels:** K1, K2  

---

## 1.1 Generative AI Foundations and Key Concepts

Generative AI (GenAI) refers to AI systems that use **large pre-trained models** to generate new content such as text, images, or code. These outputs are created by learning patterns from massive datasets rather than following fixed rules.

Large Language Models (LLMs) are a key type of GenAI. They are trained on large amounts of text data and generate responses based on **prompts**.

### Key Concepts Introduced
- **Tokenization**: Breaking text into smaller units (tokens) for processing.
- **Embeddings**: Numerical vector representations capturing semantic meaning.
- **Context window**: The maximum amount of input the model can consider at once.
- **Multimodal models**: Models that can process more than one data type (e.g., text + images).

### Testing Relevance
LLMs can support testers across the test process by:
- Improving requirements
- Generating test cases and test data
- Supporting exploratory testing
- Drafting test documentation

**Important exam point:**  
GenAI supports testers but does **not replace human judgment**.

---

## 1.1.1 AI Spectrum: Symbolic AI, Classical ML, Deep Learning, GenAI

### Symbolic AI
- Rule-based
- Uses symbols and logical rules
- Deterministic behavior

**Testing example:**  
Rule-based defect classification system.

**Analogy:**  
A strict checklist.

---

### Classical Machine Learning
- Learns from historical data
- Requires feature selection and data preparation
- Predictive rather than generative

**Testing example:**  
Predicting defect-prone components based on past data.

**Analogy:**  
Learning from previous bug trends.

---

### Deep Learning
- Uses neural networks
- Learns features automatically
- Effective with large, complex datasets

**Testing example:**  
Image recognition for UI comparison.

**Analogy:**  
Learning patterns without being explicitly told what to look for.

---

### Generative AI
- Uses deep learning to generate new content
- Includes LLMs
- Can create text, images, or code

**Key advantage for testing:**  
Pre-trained models can be applied directly to testing tasks.

**Risk:**  
Outputs may be plausible but incorrect.

---

## 1.1.2 Basics of Generative AI and LLMs

LLMs are typically based on **transformer architectures** and trained on very large datasets.

### Important Concepts
- **Inference**: The process where an LLM predicts the next most likely token.
- **Non-determinism**: The same prompt may produce different outputs.
- **Small Language Models (SLMs)**: Smaller, faster, and more focused models.

### Context Window
- Determines how much information the model can consider at once
- Larger context windows improve coherence but require more computation

**Exam reminder:**  
LLMs generate statistically probable outputs, not guaranteed correct answers.

---

## 1.1.3 Foundation, Instruction-Tuned, and Reasoning LLMs

### Foundation LLMs
- Trained on large, diverse datasets
- General-purpose
- Require adaptation for specific tasks

**Testing use:**  
General summarization or analysis.

---

### Instruction-Tuned LLMs
- Fine-tuned to follow instructions
- Better at structured outputs

**Testing use:**  
Generating test cases in a specific format (e.g., Gherkin).

---

### Reasoning LLMs
- Optimized for logical, multi-step reasoning
- Suitable for complex analysis tasks

**Testing use:**  
Root-cause analysis or complex defect reasoning.

**Exam point:**  
Different LLM types are selected based on task complexity.

---

## 1.1.4 Multimodal LLMs and Vision-Language Models

### Multimodal LLMs
- Can process multiple data types (text, images, audio, video)

### Vision-Language Models
- Combine visual and textual information
- Convert images into embeddings before processing

**Testing applications:**
- Comparing UI screenshots with requirements
- Analyzing wireframes alongside user stories
- Generating tests from visual designs

**Key idea:**  
Multimodal capability increases testing insight but still requires human validation.

---

## 1.2 Leveraging Generative AI in Software Testing: Core Principles

GenAI can assist testers through:
- Text and code generation
- Question answering
- Summarization
- Translation
- Image analysis (for multimodal models)

There are **two main ways** testers interact with LLMs:
1. AI chatbots  
2. LLM-powered testing applications

---

## 1.2.1 Key LLM Capabilities for Test Tasks

LLMs can support:
- Requirements analysis (finding ambiguities and gaps)
- Test case generation
- Test oracle creation (expected results)
- Test data generation
- Test automation support
- Test result analysis
- Test documentation and reporting

**Important exam point:**  
LLMs assist across the lifecycle but do **not make final decisions**.

---

## 1.2.2 AI Chatbots vs LLM-Powered Testing Applications

### AI Chatbots
- Conversational interface
- Immediate feedback
- Useful for exploratory testing and brainstorming
- Accessible to non-technical users

### LLM-Powered Testing Applications
- Integrated via APIs into tools and frameworks
- More scalable and customizable
- Suitable for automation and enterprise use

**Critical success factor:**  
Effective **prompt engineering** is required in both approaches.

---

## Chapter 1 – Key Exam Takeaways

- GenAI is probabilistic, not deterministic
- Human oversight is mandatory
- Different AI and LLM types serve different testing needs
- Multimodal models enhance, but do not replace, testers
- Prompt quality strongly influences output quality

---

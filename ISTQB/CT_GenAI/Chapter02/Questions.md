## Section 2.1: Effective Prompt Development

**1. Which component of a structured prompt defines the perspective or persona the Generative AI model should adopt?**
*   A. Context
*   B. Role
*   C. Constraint
*   D. Output Format
    *   **Answer:** B
    *   **Reference:** Section 2.1.1 [1]

**2. A tester provides the following text in a prompt: "Do not use external libraries. Keep descriptions under 50 words." Which prompt component does this represent?**
*   A. Instruction
*   B. Input Data
*   C. Constraints
*   D. Context
    *   **Answer:** C
    *   **Reference:** Section 2.1.1 [1]

**3. In the context of structured prompts, what is the purpose of "Context"?**
*   A. To provide background information, such as details about the test object.
*   B. To specify the expected structure of the response (e.g., JSON).
*   C. To provide the specific directive or task to be performed.
*   D. To provide the persona the AI should adopt.
    *   **Answer:** A
    *   **Reference:** Section 2.1.1 [1]

**4. Which prompting technique involves breaking a complex task into a series of intermediate steps?**
*   A. Meta prompting
*   B. Few-shot prompting
*   C. Zero-shot prompting
*   D. Prompt chaining
    *   **Answer:** D
    *   **Reference:** Section 2.1.2 [2]

**5. A tester provides an LLM with three examples of a user story paired with the corresponding Gherkin test case before asking it to generate a test case for a new story. Which technique is being used?**
*   A. Zero-shot prompting
*   B. Prompt chaining
*   C. Few-shot prompting
*   D. System prompting
    *   **Answer:** C
    *   **Reference:** Section 2.1.2 [3]

**6. What is "Meta Prompting"?**
*   A. Asking the AI to generate or refine its own prompts.
*   B. Providing no examples to the model.
*   C. Using a chain of thoughts to solve math problems.
*   D. Setting the temperature parameter to zero.
    *   **Answer:** A
    *   **Reference:** Section 2.1.2 [4]

**7. Which technique is most beneficial when a tester is unsure how to craft an effective prompt and wants to collaborate with the AI to co-create it?**
*   A. Few-shot prompting
*   B. Meta prompting
*   C. One-shot prompting
*   D. Prompt chaining
    *   **Answer:** B
    *   **Reference:** Section 2.1.2 [4]

**8. Which of the following statements about System Prompts is TRUE?**
*   A. They change with every interaction in a chat session.
*   B. They are strictly optional and rarely used in testing tools.
*   C. They are usually defined by the developer/tester to guide overall behavior and stay constant.
*   D. They represent the specific input data for a single task.
    *   **Answer:** C
    *   **Reference:** Section 2.1.3 [5], [6]

**9. A user inputs the query: "List the key differences between black-box and white-box testing." What type of prompt is this?**
*   A. System Prompt
*   B. User Prompt
*   C. Constraint Prompt
*   D. Role Prompt
    *   **Answer:** B
    *   **Reference:** Section 2.1.3 [6]

---

## Section 2.2: Applying Prompt Engineering to Software Test Tasks

**10. How can GenAI assist in "Test Analysis"?**
*   A. By executing the code on the production server.
*   B. By identifying ambiguities or missing information in the test basis (e.g., requirements).
*   C. By automatically fixing defects in the code.
*   D. By managing the project budget.
    *   **Answer:** B
    *   **Reference:** Section 2.2.1 [7]

**11. When prioritizing test conditions based on risk level, what information might an LLM consider?**
*   A. The color of the user interface.
*   B. Regulatory compliance, user-facing features, and historical defect data.
*   C. The number of developers on the team.
*   D. The specific hardware temperature of the server.
    *   **Answer:** B
    *   **Reference:** Section 2.2.1 [7]

**12. GenAI supports "Coverage Analysis" by:**
*   A. Creating a graphical user interface for the application.
*   B. Mapping requirements to test conditions to identify gaps.
*   C. Running the tests 100 times to ensure stability.
*   D. Deleting unused code.
    *   **Answer:** B
    *   **Reference:** Section 2.2.1 [7]

**13. In the context of Test Design, what is "Test Data Synthesis"?**
*   A. Encrypting production data.
*   B. Creating representative, privacy-preserving synthetic data that resembles production data.
*   C. Deleting old test data from the database.
*   D. Compressing test data to save storage space.
    *   **Answer:** B
    *   **Reference:** Section 2.2.2 [8]

**14. How can GenAI support automated test script generation?**
*   A. It can only generate Python code, no other languages.
*   B. It translates manual test steps into code compatible with test automation frameworks.
*   C. It installs the IDE on the tester's machine.
*   D. It executes the script and fixes compilation errors automatically without human review.
    *   **Answer:** B
    *   **Reference:** Section 2.2.2 [8]

**15. Which task related to "Test Execution Scheduling" can GenAI support?**
*   A. Physically turning on the test servers.
*   B. Optimizing schedules based on priority, risks, and dependencies.
*   C. Hiring manual testers for execution.
*   D. Deciding the release date of the software.
    *   **Answer:** B
    *   **Reference:** Section 2.2.2 [8]

**16. In Automated Regression Testing, what is "Impact Analysis"?**
*   A. Analyzing code changes to identify high-risk areas for targeted testing.
*   B. Calculating the financial cost of a bug.
*   C. determining which developers are most productive.
*   D. Analyzing the impact of AI on the environment.
    *   **Answer:** A
    *   **Reference:** Section 2.2.3 [9]

**17. What is "Self-Healing" in the context of GenAI-supported regression testing?**
*   A. The AI rewriting the application business logic.
*   B. Automatically adjusting test scripts to handle minor UI or API changes (e.g., dynamic locators).
*   C. The AI rebooting itself after a crash.
*   D. The AI generating new test cases for new features.
    *   **Answer:** B
    *   **Reference:** Section 2.2.3 [9]

**18. How can GenAI support API regression testing?**
*   A. By generating the API documentation only.
*   B. By adapting test scripts automatically to evolving API specifications and generating diverse test data.
*   C. By preventing developers from changing the API.
*   D. By converting REST APIs to SOAP APIs.
    *   **Answer:** B
    *   **Reference:** Section 2.2.3 [10]

**19. Which activity falls under "Test Monitoring and Control" with GenAI?**
*   A. Writing unit tests.
*   B. Analyzing trends to predict potential risks and alert teams of deviations.
*   C. Installing test tools.
*   D. Training the neural network.
    *   **Answer:** B
    *   **Reference:** Section 2.2.4 [11]

**20. According to the syllabus, which prompting technique is best suited for "Complex tasks requiring precision with human verification at each step" (e.g., Test Analysis)?**
*   A. Few-shot prompting
*   B. Prompt chaining
*   C. Zero-shot prompting
*   D. Meta prompting
    *   **Answer:** B
    *   **Reference:** Section 2.2.5 [12]

**21. According to the syllabus, which prompting technique is best suited for "Repetitive or specific/constrained output format tasks" (e.g., Gherkin style test cases)?**
*   A. Prompt chaining
*   B. Meta prompting
*   C. Few-shot prompting
*   D. Zero-shot prompting
    *   **Answer:** C
    *   **Reference:** Section 2.2.5 [13]

**22. According to the syllabus, which prompting technique is best suited for "Flexible, dynamic tasks" (e.g., crafting prompts for new tasks)?**
*   A. Prompt chaining
*   B. Few-shot prompting
*   C. Meta prompting
*   D. Input constraint prompting
    *   **Answer:** C
    *   **Reference:** Section 2.2.5 [13]

---

## Section 2.3: Evaluation and Refinement

**23. Which metric measures the "overall correctness of the generated output against expert-written test cases or requirements"?**
*   A. Precision
*   B. Recall
*   C. Accuracy
*   D. Diversity
    *   **Answer:** C
    *   **Reference:** Section 2.3.1 [14]

**24. Which metric measures "the degree to which the generated test cases correctly identify anomalies"?**
*   A. Accuracy
*   B. Precision
*   C. Diversity
*   D. Time Efficiency
    *   **Answer:** B
    *   **Reference:** Section 2.3.1 [14]

**25. Which metric measures "the ability of a model to identify all relevant instances" (e.g., covering all valid equivalence partitions)?**
*   A. Recall
*   B. Precision
*   C. Execution Success Rate
*   D. Relevance
    *   **Answer:** A
    *   **Reference:** Section 2.3.1 [15]

**26. Which metric ensures "a wide range of inputs and scenarios are covered, avoiding repetition"?**
*   A. Accuracy
*   B. Relevance
*   C. Diversity
*   D. Time Efficiency
    *   **Answer:** C
    *   **Reference:** Section 2.3.1 [15]

**27. What does "Execution Success Rate" measure?**
*   A. How fast the AI generates the code.
*   B. The proportion of generated test scripts that can be executed without syntax errors.
*   C. The number of bugs found by the script.
*   D. The cost of running the script.
    *   **Answer:** B
    *   **Reference:** Section 2.3.1 [16]

**28. Which metric compares the "time required by the AI to generate test cases versus the time a human would take"?**
*   A. Execution Success Rate
*   B. Time Efficiency
*   C. Recall
*   D. Latency
    *   **Answer:** B
    *   **Reference:** Section 2.3.1 [17]

**29. What is "Iterative Prompt Modification"?**
*   A. Starting with a base prompt and gradually adjusting context or wording based on observed results.
*   B. Running the same prompt 100 times to see if it changes.
*   C. Using a prompt created by another team member.
*   D. Changing the AI model instead of the prompt.
    *   **Answer:** A
    *   **Reference:** Section 2.3.2 [18]

**30. A tester creates two versions of a prompt and compares which version produces better metrics. What is this technique called?**
*   A. Meta Prompting
*   B. A/B Testing
*   C. Prompt Chaining
*   D. Zero-shot Prompting
    *   **Answer:** B
    *   **Reference:** Section 2.3.2 [18]

**31. Why is "Output Analysis" important for prompt refinement?**
*   A. It allows the tester to ignore the results.
*   B. It helps understand the types of errors (inaccuracies/inconsistencies) to refine prompts and avoid similar defects.
*   C. It increases the cost of testing.
*   D. It guarantees the AI will never make a mistake again.
    *   **Answer:** B
    *   **Reference:** Section 2.3.2 [18]

**32. Which of the following is a recommended technique for refining prompts?**
*   A. Integrate user feedback from testers about the utility of the output.
*   B. Always make the prompt shorter, regardless of results.
*   C. Never change the System Prompt.
*   D. Stop using the tool if the first result is bad.
    *   **Answer:** A
    *   **Reference:** Section 2.3.2 [18]

**33. When refining prompts, what might be the effect of "Adjusting Specificity"?**
*   A. Adding more context always confuses the model.
*   B. Adding more context can improve response quality, while shorter prompts may yield better generalization.
*   C. Specificity has no impact on LLMs.
*   D. You should always use the maximum context window.
    *   **Answer:** B
    *   **Reference:** Section 2.3.2 [19]

**34. Why is sharing prompt practices across the test team recommended?**
*   A. To ensure everyone uses the exact same password.
*   B. To standardize techniques, maintain consistent quality, and promote a culture of learning.
*   C. To increase the competition between testers.
*   D. To prevent testers from learning prompt engineering.
    *   **Answer:** B
    *   **Reference:** Section 2.3.2 [19]

**35. A tester wants to generate acceptance criteria for a User Story. They use a prompt that processes the User Story text and a GUI wireframe image simultaneously. This is an example of:**
*   A. Text-only prompting
*   B. Multimodal prompting
*   C. Audio prompting
*   D. System prompting
    *   **Answer:** B
    *   **Reference:** Section 2.2.1 [20]

**36. Which prompt component includes "User stories, acceptance criteria, screenshots, or code"?**
*   A. Role
*   B. Input Data
*   C. Instruction
*   D. Output Format
    *   **Answer:** B
    *   **Reference:** Section 2.1.1 [1]

# Choosing the Right Estimation Technique

| **Technique**                | **Best For**                           | **Example** | **Limitations**                          |
|------------------------------|---------------------------------------|------------|------------------------------------------|
| **Work Breakdown Structure (WBS)** | Large projects with clear tasks | A test plan is broken down into **Test Planning (10 hrs), Test Case Design (20 hrs), Test Execution (30 hrs), Bug Reporting (15 hrs), and Regression Testing (25 hrs)**. The sum is used as the estimate. | Can be time-consuming |
| **Function Point Analysis (FPA)** | Business function-based estimation | A login feature has **Simple (3 hrs), Medium (5 hrs), and Complex (8 hrs) function points**. Each function is estimated, and the total is calculated. | Requires detailed function breakdown |
| **PERT (Three-Point Estimation)** | Uncertain/complex projects | For testing a payment gateway, **Optimistic (20 hrs), Pessimistic (50 hrs), and Most Likely (30 hrs)** estimates are used in the formula: **(O + 4M + P) / 6 = 32 hrs**. | Needs multiple inputs (O, P, M) |
| **Use-Case Point Estimation** | User-centric applications | A checkout system has **3 Use Cases (Login, Add to Cart, Checkout)**. Each use case is **assigned an effort multiplier**, and the total is used for estimation. | Needs a clear use-case model |
| **Expert Judgment**           | Fast estimation with experience      | A senior QA engineer estimates **3 weeks for testing a new module** based on past experience with a similar project. | Less data-driven |
| **Test Case-Based Estimation** | Test-heavy projects                 | 200 test cases are planned, with **each taking 10 mins to execute**. The total estimate is **2000 minutes (~33 hours)**. | Depends on the accuracy of test case counts |

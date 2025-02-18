# Code Coverage Tools & Metrics

## 1. What is Code Coverage?  
**Code coverage** is a software quality metric that measures the extent to which the source code of an application is executed during testing. It helps identify untested parts of code, ensuring better test effectiveness.

---

## 2. Code Coverage Metrics & Definitions  

| **Metric** | **Description** | **Formula** |
|------------|---------------|-------------|
| **Statement Coverage** | Measures the percentage of statements executed during tests. | `(Executed Statements / Total Statements) * 100` |
| **Branch Coverage** | Ensures that both **true** and **false** conditions in control structures (if/else, loops) are tested. | `(Executed Branches / Total Branches) * 100` |
| **Function Coverage** | Checks if all functions/methods in the code were invoked. | `(Executed Functions / Total Functions) * 100` |
| **Line Coverage** | Determines how many lines of code were executed during testing. | `(Executed Lines / Total Lines) * 100` |
| **Path Coverage** | Ensures that all possible execution paths (combinations of branches) are covered. | `(Executed Paths / Total Paths) * 100` |
| **Mutation Coverage** | Assesses test effectiveness by introducing **mutations (faults)** in the code and ensuring that tests catch them. | `(Killed Mutants / Total Mutants) * 100` |

---

## 3. Popular Code Coverage Tools  

| **Tool** | **Language Support** | **Coverage Metrics** | **Integration** |
|----------|-----------------|----------------|--------------|
| **JaCoCo** | Java | Line, Branch, Instruction | Integrated with Maven, Gradle, Jenkins |
| **Istanbul** | JavaScript, TypeScript | Statement, Branch, Function, Line | Works with Jest, Mocha, Cypress |
| **PyTest-Cov** | Python | Line, Branch | Works with PyTest |
| **Cobertura** | Java | Line, Branch | Supports Ant, Maven |
| **Clover** | Java, Groovy | Statement, Branch, Method, Path | Atlassian tool, integrates with CI/CD |
| **BullseyeCoverage** | C, C++ | Statement, Branch | Used for embedded systems |
| **Gcov & LCOV** | C, C++ | Line, Function, Branch | Works with GNU Compiler Collection (GCC) |
| **OpenCover** | .NET | Line, Branch | Works with NUnit, MSTest |
| **Codecov & Coveralls** | Multiple languages | Aggregates code coverage from various tools | Cloud-based, integrates with GitHub Actions, GitLab CI |

---

## 4. Best Practices for Using Code Coverage Tools  

✅ **Set a Minimum Coverage Threshold**  
- Aim for **70%-80% coverage** in CI/CD pipelines.  
- Define thresholds per module (e.g., business logic needs 90% coverage, UI tests may require less).  

✅ **Measure **Branch & Mutation Coverage**, Not Just Line Coverage**  
- **Line coverage alone is misleading**; ensure both **true/false conditions** are tested.  
- Use **mutation testing** to validate **test effectiveness**.  

✅ **Integrate Coverage Reports into CI/CD Pipelines**  
- Use **JaCoCo for Java, Istanbul for JavaScript, PyTest-Cov for Python**.  
- Generate **coverage reports** and block merges if coverage drops below the threshold.  

✅ **Focus on High-Risk Code Areas**  
- Prioritize coverage in **core logic, security modules, and high-risk components**.  
- **Low-priority areas (logs, simple getters/setters)** don’t need 100% coverage.  

✅ **Use Code Coverage Alongside Other Metrics**  
- Combine coverage with **code complexity analysis** (e.g., Cyclomatic Complexity).  
- Use **static analysis tools** (e.g., SonarQube, Code Climate) to assess **code maintainability**.  

---

## 5. Example: Generating Code Coverage Reports in Different Languages  

### **Java: Using JaCoCo in Maven**  
```xml
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <version>0.8.7</version>
    <executions>
        <execution>
            <goals>
                <goal>prepare-agent</goal>
            </goals>
        </execution>
    </executions>
</plugin>

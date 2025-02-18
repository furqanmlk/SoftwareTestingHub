# POC: Shift-Left Testing with API and Contract Testing

## 1. Objective
UI tests are often run late in the pipeline, leading to **delayed defect detection**. This POC explores **contract testing** (e.g., using Pact) to shift-left and detect **integration issues early**.

---

## 2. What is Contract Testing? 📝
**Contract Testing** is a testing approach where **interactions between microservices or APIs are verified** by ensuring that both **providers (services)** and **consumers (clients)** adhere to a predefined **contract**.

### ✅ **Key Concepts**
- The **contract** specifies the **expected requests and responses** between services.
- The **consumer** (e.g., frontend, another service) defines expectations for API responses.
- The **provider** (e.g., backend API) must conform to this contract.
- **Contract testing ensures backward compatibility**, preventing breaking changes.

---

## 3. Steps to Implement Contract Testing

### **Step 1: Write API Contract Tests Before UI Tests**
- **Define a contract** between API consumers (e.g., frontend) and providers (e.g., backend service).
- Use **Pact, OpenAPI Spec, or Postman** to structure and validate API interactions.

### **Step 2: Validate API Request/Response Formats**
- Use **Pact** (for consumer-driven contracts) or **Postman/Newman** to verify API responses.
- Ensure API payloads match the expected **data schema**.

### **Step 3: Run Contract Tests in CI/CD Pipelines**
- Integrate contract tests into **pre-merge checks**.
- Fail builds if contract mismatches are detected.
- Automate contract verification using tools like **Pact Broker**.

### **Step 4: Identify Mismatches in API Contracts Before Deployment**
- Compare **current API responses** against the **stored contract version**.
- Generate a **contract diff report** if changes are detected.
- Notify developers before changes impact downstream services.

---

## 4. Example: Pact Contract Test (Node.js)
Below is an example **consumer-driven contract test using Pact**.

### **Consumer Test (Frontend)**
```js
const { Pact } = require('@pact-foundation/pact');
const { expect } = require('chai');
const request = require('supertest');

const provider = new Pact({
  consumer: 'FrontendApp',
  provider: 'UserService',
  port: 8081
});

describe('Pact Contract Test', () => {
  before(() => provider.setup());

  it('should return user data', async () => {
    await provider.addInteraction({
      state: 'User exists',
      uponReceiving: 'A request for user data',
      withRequest: {
        method: 'GET',
        path: '/users/1'
      },
      willRespondWith: {
        status: 200,
        body: {
          id: 1,
          name: 'John Doe',
          email: 'john.doe@example.com'
        }
      }
    });

    const response = await request('http://localhost:8081').get('/users/1');
    expect(response.status).to.equal(200);
    expect(response.body.name).to.equal('John Doe');
  });

  afterEach(() => provider.verify());
  after(() => provider.finalize());
});

# Types of Testing

## 1. Functional Testing

### Unit Testing
- Testing individual components in isolation.  
  **Example:** Testing a login function to verify it returns correct authentication results.  

### Integration Testing
- Ensuring multiple components work together.  
  **Example:** Checking if a user’s order is correctly processed after payment.  

### System Testing
- Testing the entire system as a whole.  
  **Example:** Verifying that an e-commerce website allows users to search, add items to a cart, and complete a purchase.  

### Regression Testing
- Checking if new code changes break existing functionality.  
  **Example:** Running automated test cases after a feature update to ensure old features still work.  

### User Acceptance Testing (UAT)
- Ensuring the system meets business requirements.  
  **Example:** Having end users validate a newly developed payroll system before deployment.  

## 2. Non-Functional Testing

### Performance Testing
- Evaluating system speed and stability.  
  **Example:** Measuring how a banking app performs under high traffic.  

### Load Testing
- Checking system behavior under expected loads.  
  **Example:** Simulating 1,000 users logging in simultaneously to see if the system slows down.  

### Stress Testing
- Testing beyond normal operational capacity.  
  **Example:** Sending excessive requests to a server to check if it crashes.  

### Security Testing
- Identifying vulnerabilities.  
  **Example:** Testing an online banking system for SQL injection or unauthorized access.  

### Usability Testing
- Evaluating user-friendliness.  
  **Example:** Observing how easily new users navigate a mobile app.  

### Compatibility Testing
- Ensuring software works across different environments.  
  **Example:** Checking if a website functions correctly on Chrome, Firefox, and Safari.  

## 3. Specialized Testing

### Smoke Testing
- Verifying basic functionality before deeper testing.  
  **Example:** Checking if a new mobile app build launches and its main menu is accessible.  

### Sanity Testing
- Ensuring small fixes don’t break major functionality.  
  **Example:** After fixing a password reset bug, verifying that login still works.  

### End-to-End Testing
- Testing workflows from start to finish.  
  **Example:** Checking an online travel booking system from searching flights to completing payment.  

### Exploratory Testing
- Random testing without predefined cases.  
  **Example:** Manually navigating a new e-commerce platform to find bugs.  

### Ad-hoc Testing
- Unstructured testing to break the system.  
  **Example:** Entering unexpected inputs to check if a form crashes.  

## 4. Automated Testing

### UI Automation Testing
- Using scripts to test user interfaces.  
  **Example:** Using Selenium to verify login functionality on a web app.  

### API Testing
- Validating API responses.  
  **Example:** Using Postman to check if a REST API correctly returns user data.  

### Continuous Testing (CI/CD)
- Running tests automatically in a pipeline.  
  **Example:** GitHub Actions executing automated tests after every code commit.  

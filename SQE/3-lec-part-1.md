## SQE Views on Quality (One-liners with Examples)

- **Transcendental View**: Quality is abstract, recognized but not defined.  
  _Example_: "I know good UI when I see it."

- **User View**: Quality is fitness for purpose.  
  _Example_: App that helps users easily transfer funds.

- **Manufacturing View**: Quality is conformance to specs.  
  _Example_: Login must accept min 8-character passwords as defined.

- **Product View**: Quality depends on inherent product features.  
  _Example_: Fast load times, responsive UI.

- **Value-Based View**: Quality depends on what users will pay.  
  _Example_: Premium antivirus software with better features.


## 4Ps in Software Development


- **Process**: Activities/methods followed (e.g., SDLC)
- **People**: Stakeholders (e.g., Developers, Testers)
- **Project**: Time and resource-bound task (e.g., Banking App)
- **Product**: Final deliverable (e.g., Mobile banking app)


## Testing Vocabulary (One-liners + Examples)

- **Test Process**: Full testing lifecycle.  
  _Example_: From planning to reporting.

- **Test Policy**: Organization’s top-level test principles.  
  _Example_: "All releases must go through security testing."

- **Test Strategy**: Generic testing approach for multiple projects.  
  _Example_: "All web apps use Selenium + JMeter."

- **Test Approach**: Strategy applied to a specific project.  
  _Example_: "Login module tested using Black Box Testing."

- **Test Plan**: What, when, and how testing will be done.  
  _Example_: "Test login, dashboard, and payment before 25th April."

- **Test Estimation**: Predict time, cost, test cases.  
  _Example_: "We need 20 hours to test login."

- **Test Design**: Create test cases from conditions.  
  _Example_: "If user forgets password → Password reset page."

- **Test Basis**: Source for test design.  
  _Example_: "User story: As a user, I want to transfer funds."

- **Test Condition**: What to test.  
  _Example_: "Login must work with valid credentials."

- **Test Analysis**: Finding test conditions from requirements.  
  _Example_: "Check login, signup, and logout."

- **Test Case**: Step-by-step test scenario.  
  _Example_: "1. Enter credentials → 2. Click login → 3. Verify dashboard."

- **Test Script**: Automated test code.  
  _Example_: Selenium script to auto test login form.

- **Test Procedure**: Set of test cases with order.  
  _Example_: Run login, password reset, dashboard tests.

- **Test Suite**: Group of test cases.  
  _Example_: "Login Test Suite = login, forgot password, OTP tests."

- **Test Data**: Data used during testing.  
  _Example_: Username: `user01`, Password: `Test@123`

- **Test Object**: System/component to test.  
  _Example_: "Banking App Login Page"

- **Test Item**: Part of system under test.  
  _Example_: Login button on the screen.

- **Test Objective**: Reason to test something.  
  _Example_: Ensure only valid users can login.

- **Test Oracle**: Expected result reference.  
  _Example_: "Account balance = previous + deposit - withdrawal"

- **Test Automation**: Scripts or tools to test automatically.  
  _Example_: Using Cypress to run 100 login tests.

- **Test Environment**: Setup needed for testing.  
  _Example_: Chrome browser, staging server, DB mock.

- **Testware**: All testing artifacts.  
  _Example_: Test plans, cases, scripts, data.

- **Test Input**: Data entered to run tests.  
  _Example_: "Input: email=user@mail.com"

- **Test Implementation**: Prepare everything for execution.  
  _Example_: "Create test data, setup staging env."

- **Test Execution**: Run tests, compare expected vs actual.  
  _Example_: "Test login → Login failed → Log defect"

- **Test Harness**: Tools/stubs to support testing.  
  _Example_: "Dummy database driver for unit tests"

- **Test Progress Report**: Regular update on testing.  
  _Example_: "60% test cases executed, 10 defects found"

- **Test Summary Report**: Final review of testing.  
  _Example_: "90% passed, 5 critical bugs fixed"


## Example: Testing a Banking App


- **Test Plan**: "We will perform functional & security testing on all features."
- **Test Suite**: "Login system test suite includes all login-related test cases."
- **Test Case**: "Incorrect password → Error message should show."
- **Test Procedure**: "1. Go to login page → 2. Enter wrong password → 3. Check error"


## Test Process (Simplified One-Liners)


1. **Test Planning** – Define scope, strategy, resources.
2. **Test Monitoring & Control** – Track progress, manage changes.
3. **Test Analysis** – Find what needs to be tested.
4. **Test Design** – Create test cases from analysis.
5. **Test Implementation** – Prepare data, scripts, environment.
6. **Test Execution** – Run test cases, log defects.
7. **Test Completion** – Wrap up, report results, archive testware.

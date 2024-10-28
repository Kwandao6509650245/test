## Unit and Integration Testing Overview
Our team uses the following tools for testing :
- Jest: Used for unit testing individual functions or modules, ensuring that each component works as expected in isolation.
- Supertest: Handles integration testing, focusing on how different parts of the application interact, especially useful for testing API endpoints.
- Babel: Transpiles ES6+ JavaScript code to ensure compatibility with Jest, allowing the use of modern JavaScript features in tests.
- GitHub Actions: Automates testing in CI/CD. Each push and pull request triggers the GitHub Actions workflow, running our test suite in various environments (e.g., macos-latest, ubuntu-24.04). This setup ensures consistent test results across platforms, and notifies us immediately if any tests fail, providing valuable feedback on code quality before merging.

## Setting Up Tests
- To set up the testing environment, make sure you have Yarn installed. Then, install the required packages by running :

```bash
yarn 
```
- The CI pipeline automatically runs whenever code is updated (through push or pull requests) and follows these steps:

	1.	Code Checkout: GitHub Actions uses the actions/checkout@v4 action to pull the latest code from the repository onto the runner (the virtual environment where the CI runs).
2.	Set Up Environment: The CI pipeline sets up the runtime environment, like OS and Node.js version, based on the configuration in the .yml file. This can include environments like ubuntu, macOS, windows, or different versions of Node.js.
	3.	Install Dependencies: The pipeline uses commands like npm ci (or similar) to install the project dependencies specified, ensuring a stable environment and minimizing issues due to missing packages.
	4.	Run Automated Tests: It runs the test suite using a command such as npm test and sets up necessary environment variables from secrets to ensure tests run correctly.

## Running Tests
Running Tests Locally: Before pushing code, you can run tests locally with these commands:

```bash
npm test
```
CI Pipeline Process:
1.	Every time there’s a push or pull request to any branch (indicated by '*' in the .yml file), the pipeline triggers automatically.
	2.	GitHub Actions starts running the Run-Test-Suite job, following each step in sequence: checking out code, setting up the environment, installing dependencies, and running the test suite.
	3.	The matrix strategy makes the pipeline test the code across multiple OS and Node.js versions, as specified, to confirm compatibility across all environments.
## Test File Structure
The Unit Test files in this project are stored in the src/__test__ folder :

CreatePetEntry.test.js 
- Handle input changes form Create Pet Entry
- Calls createNewPet on button click with correct data
- Does not call createNewPet if required fields are not filled
EditPetEntry.test.js
- Handle input changes form Edit Pet Entry
- Calls updatePet on button click with correct data
- Should not have the same values as initial mock repo after editing 
Petintegration.test.js
- 

## Test Coverage
This repository includes thorough test coverage across two key areas:

Unit Testing: Focuses on individual functions or modules to confirm they work as expected when isolated from the rest of the code. Each unit is tested with a range of inputs to ensure reliable and consistent behavior, helping to catch any issues early.

Integration Testing: Verifies that different parts of the API interact correctly. By testing how modules work together, integration testing ensures data flows smoothly between components, helping to catch issues that might only appear when components are combined.

## Viewing Test Results 
- In CI pipeline: Access test results via GitHub Actions by navigating to the Actions tab.
- Locally: Test results display in the terminal, including a summary of passed/failed tests and any errors encountered.
to viewing Test Results by following this command :
```bash
npm test
```

## Adding New Tests
 ...

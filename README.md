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
- 

## Running Tests
...
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

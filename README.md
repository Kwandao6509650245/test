## Unit and Integration Testing Overview
Our team uses the following tools for testing :
- **Jest**: For unit testing.
- **Supertest**: For integration testing.
- **Babel**: For transpiling ES6+ JavaScript code to ensure compatibility with Jest.
  
## Setting Up Tests
To set up the testing environment, make sure you have Yarn installed. Then, install the required packages by running :

```bash
yarn 
```

## Running Tests
...
## Test File Structure
all of Test File will be in src/__test__
src/
  ├── components/
  │    ├── ComponentA/
  │    │   ├── ComponentA.js
  │    │   └── ComponentA.test.js
  ├── services/
  │    ├── serviceA.js
  │    └── serviceA.test.js
tests/
  ├── integration/
  └── unit/

## Test Coverage
The tests in this repository cover the following functionality:
 - Unit Testing: Tests individual functions or modules in isolation to ensure each unit works as expected.
 - Integration Testing: Verifies that API can work together correctly.

## Viewing Test Results 
to viewing Test Results by following this command :
```bash
npm test
```
## Adding New Tests
 ...

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


  ├── __mocks__/                
  │   ├── styleMock.js               <br>
  │   ├── integration/ 								<br>
  │   │   └── PetIntegration.test.js                <br>
  │   ├── unit/              <br>
  │   │   ├── CreatePetEntry.test.js                <br>
  │   │   └── EditPetEntry.test.js                  <br>
  ├── component/                                    <br>
  ├── contexts/               <br>                      
  ├── main/                                   <br>      
  ├── app.js                              <br>          
  ├── app.css                                       <br>
  ├── http.js                                    <br>   
  ├── index.js                                     <br> 
  └── index.css                                    <br>


## Test Coverage
This repository includes thorough test coverage across two key areas:

Unit Testing: Focuses on individual functions or modules to confirm they work as expected when isolated from the rest of the code. Each unit is tested with a range of inputs to ensure reliable and consistent behavior, helping to catch any issues early.

Integration Testing: Verifies that different parts of the API interact correctly. By testing how modules work together, integration testing ensures data flows smoothly between components, helping to catch issues that might only appear when components are combined.

## Viewing Test Results 
to viewing Test Results by following this command :
```bash
npm test
```

## Adding New Tests
 ...

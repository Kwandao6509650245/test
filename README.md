## Unit and Integration Testing Overview
Our team uses the following tools for testing :
- **Jest**: Used for unit testing individual functions or modules, ensuring that each component works as expected in isolation.
- **Supertest**: Handles integration testing, focusing on how different parts of the application interact, especially useful for testing API endpoints.
- **Babel**: Transpiles ES6+ JavaScript code to ensure compatibility with Jest, allowing the use of modern JavaScript features in tests.
- **GitHub Actions**: Automates testing in CI/CD. Each push and pull request triggers the GitHub Actions workflow, running our test suite in various environments (e.g., macos-latest, ubuntu-24.04). This setup ensures consistent test results across platforms and notifies us immediately if any tests fail, providing valuable feedback on code quality before merging.


## Setting Up Tests

- For local, to set up the testing environment, make sure you have Yarn installed. Then, install the required packages by running:

    ```bash
    yarn 
    ```

- In our project, the CI pipeline automatically runs whenever code is updated (through push or pull requests) in every branch and follows these steps:

    1. **Trigger (on:)**  
       The pipeline automatically runs on any `push` or `pull_request` event to any branch (`'*'`). This ensures the workflow is triggered for all updates across branches.

    2. **Job Setup (Run-Test-Suite)**  
       The job is configured to run on different operating systems using a matrix strategy (`ubuntu-24.04`, `windows-latest`, `macos-latest`), ensuring compatibility across environments. Different Node.js versions (`16.x`, `22.x`, and `node`) are also tested, ensuring the code runs smoothly on multiple versions of Node.js.

    3. **Steps**:
        - **System Information**:
            - `echo "This job is now running on a ${{ matrix.os }}"` outputs the OS currently in use for easier debugging and identification.
            - Displays the branch name and repository using `echo`, showing contextual information for the test.
        
        - **Checkout Code**:  
          Uses `actions/checkout@v4` to pull the latest code from the repository into the runner environment, ensuring the job has the most recent code.
        
        - **Setup Node.js**:  
          - Installs Node.js on the runner according to the specified `matrix.node-version`. The `cache: 'npm'` option is used to save previously downloaded packages and speed up future runs.
        
        - **List Repository Files**:  
          - Lists all files in the repository with `ls`, helping confirm that the code is available and accessible for subsequent steps.
        
        - **Install Dependencies**:  
          - Runs `npm ci` to install all project dependencies as specified in `package-lock.json`, ensuring consistent dependency versions.
        
        - **Run Test Suite**:  
          - Runs `npm test` to execute the automated tests.
          - The environment variables (`APP_KEYS`, `API_TOKEN_SALT`, `ADMIN_JWT_SECRET`, `TRANSFER_TOKEN_SALT`, `JWT_SECRET`) are set using GitHub secrets, securely providing necessary values for tests.
        
        - **If tests fail**, an error is logged specifying which tests failed on each OS and Node.js version.
        
        - **Display Job Status**:  
          - Logs the job’s final status (e.g., success or failure) using `echo`, providing a summary of the job outcome for easier troubleshooting.


## Running Tests
- **Running Tests Locally**: Before pushing code, you can run tests locally with these commands:

```bash
npm test
```
- **CI Pipeline Process**:
  1. Every time there’s a push or pull request to any branch (indicated by '*' in the `.yml` file), the pipeline triggers automatically.
  2. GitHub Actions starts running the Run-Test-Suite job, following each step in sequence: checking out code, setting up the environment, installing dependencies, and running the test suite.
  3. The matrix strategy makes the pipeline test the code across multiple operating systems and Node.js versions, as specified, to confirm compatibility across all environments.


## Test File Structure

The unit test and integration test files in this project are stored in the `src/__test__` folder:

### Unit Tests

**CreatePetEntry.test.js**
- Handles input changes for Create Pet Entry.
- Calls `createNewPet` on button click with correct data.
- Does not call `createNewPet` if required fields are not filled.

**EditPetEntry.test.js**
- Handles input changes for Edit Pet Entry.
- Calls `updatePet` on button click with correct data.
- Should not have the same values as the initial mock repo after editing.

### Integration Tests

**PetIntegration.test.js**
- **Create a New Pet Entry**: Tests POST `/api/pets` to create a new entry and checks the created data.
- **Update a Pet Entry**: Tests PUT `/api/pets/:id` to update an existing pet’s data.
- **Retrieve All Pets**: Tests GET `/api/pets` to retrieve all pet entries.
- **Handle Missing Fields**: Tests POST `/api/pets` with missing data to check for error handling.
- **Retrieve a Pet by ID**: Tests GET `/api/pets/:id` to fetch a specific pet.
- **Delete a Pet Entry**: Tests DELETE `/api/pets/:id` to ensure a pet entry is deleted properly.
- **Handle Non-Existing Pet Requests**: Checks PUT and GET requests for non-existing pet IDs, ensuring proper error responses.

### CI Configuration

The `test-suite.yml` file used for GitHub Actions CI is stored in `.github/workflows`:
- This file is configured to handle CI for our testing pipeline.


## Test Coverage
This repository includes thorough test coverage across two key areas:
- **Unit Testing**: Focuses on individual functions or modules to confirm they work as expected in isolation. Each unit is tested with a range of inputs to ensure reliable and consistent behavior, catching issues early in development.

- **Integration Testing**: Verifies that different parts of the API interact correctly. By testing how modules work together, integration testing ensures data flows smoothly between components, identifying issues that may appear when components are combined.

  As part of our CI setup, every push or pull request automatically triggers the test suite using GitHub Actions (configured in `.github/workflows/test-suite.yml`). This CI process runs both unit and integration tests across multiple environments, providing:

	- **Immediate Feedback**: Notifications alert us to any failed tests, enabling quick fixes and reducing the risk of breaking changes.
	- **Cross-Platform Compatibility**: The CI pipeline runs tests on different operating systems (e.g., `macOS`, `Ubuntu`, `Windows`) and Node.js versions, ensuring consistent performance across environments.

## Viewing Test Results 

You can view test results both in the CI pipeline on GitHub and locally in your terminal. Here’s how:

### 1. Viewing Test Results in GitHub Actions
   - **Go to the Repository on GitHub**:
     - Navigate to your project repository where the CI pipeline is set up.
   - **Access the “Actions” Tab**:
     - In this tab, you’ll see all triggered workflows, such as those from pushes or pull requests.
     - The latest workflow appears at the top with statuses like ✔️ success, ❌ failure, or ⏳ in progress.
   - **Select the Workflow**:
     - Click on the workflow to see its details. This opens a page showing each job created from the `.yml` file (e.g., build).
   - **View the Job Log**:
     - Click on the job (e.g., build) to check logs for each step.
     - Logs show details for steps like dependency installation, test execution, and any errors or failures.
   - **Notifications and Test Reports**:
     - If a test fails, GitHub Actions provides error details, showing which assertions did not pass.

### 2. Viewing Test Results in Terminal (Local Testing)
   - **Run Tests Locally**:
     - Run tests with the command:
     
       ```bash
       npm test
       ```

     - Results will appear in the terminal in real-time.

   - **Test Results**:
     - The terminal shows detailed results, including:
       - Number of tests passed and failed
       - Time taken per test
       - Error details for any failed assertions
   - **Summary**:
     - At the end, the terminal provides a summary, such as `Tests: 10 passed, 2 failed`, giving an overview of the test outcomes.


## Adding New Tests

Add new test files within the `src/__test__` directory, following these steps:

1. **Create Test Files**:
   - For **unit tests**, add files under `src/__test__/unit/`.
   - For **integration tests**, place files under `src/__test__/integration/`.
   - Each test file should follow a naming convention that reflects its purpose. For example:
     - `NewComponent.test.js` for unit tests.
     - `APIEndpointIntegration.test.js` for integration tests.

2. **Write Test Cases**:
   - Define test cases that validate specific functions, components, or API endpoints.
    - Use Jest’s `describe` and `it` functions to organize tests for unit testing.
   - For integration tests with Supertest.

3. **Run Tests Locally**:
   - Ensure that new tests pass locally by running:
     
     ```bash
     npm test
     ```
   - Check that tests produce expected outcomes without breaking existing functionality.

4. **Commit and Push**:
   - After validating new tests locally, select the branch associated with the new test (e.g., `sprint2-unit-test`).
   - Commit and push the code to trigger CI tests in GitHub Actions. This will run the test suite across different environments, reinforcing compatibility and quality.
 
5. **Review Test Results**:
   - Monitor the GitHub Actions workflow to confirm that all tests pass.
  
6. **Merge to Main Branch**:
   - After ensuring that all tests pass successfully, you can merge your branch into the main branch.




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

	1.	Trigger (on:)
	•	The pipeline automatically runs on any push or pull_request event to any branch ('*'). This ensures the workflow is triggered for all updates across branches.
	2.	Job Setup (Run-Test-Suite)
	•	The job is configured to run on different operating systems using matrix strategy (ubuntu-24.04, windows-latest, macos-latest), ensuring compatibility across environments.
	•	Different Node.js versions (16.x, 22.x, and node) are also tested, which ensures the code runs smoothly on multiple versions of Node.js.
	3.	Steps:
	•	System Information:
	•	echo "This job is now running on a ${{ matrix.os }}" outputs the OS currently in use for easier debugging and identification.
	•	Displays the branch name and repository using echo, showing contextual information for the test.
	•	Checkout Code:
	•	Uses actions/checkout@v4 to pull the latest code from the repository into the runner environment, ensuring the job has the most recent code.
	•	Setup Node.js:
	•	Installs Node.js on the runner according to the specified matrix.node-version. The cache: 'npm' option is used to save previously downloaded packages and speed up future runs.
	•	List Repository Files:
	•	Lists all files in the repository with ls, helping confirm that the code is available and accessible for subsequent steps.
	•	Install Dependencies:
	•	Runs npm ci to install all project dependencies as specified in package-lock.json, ensuring consistent dependency versions.
	•	Run Test Suite:
	•	Runs npm test to execute the automated tests.
	•	The environment variables (APP_KEYS, API_TOKEN_SALT, ADMIN_JWT_SECRET, TRANSFER_TOKEN_SALT, JWT_SECRET) are set using GitHub secrets, securely providing necessary values for tests.
	•	If tests fail, an error is logged specifying which tests failed on each OS and Node.js version.
	•	Display Job Status:
	•	Logs the job’s final status (e.g., success or failure) using echo, providing a summary of the job outcome for easier troubleshooting.

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
- Create a New Pet Entry: Tests POST /api/pets to create a new entry and checks the created data.
- Update a Pet Entry: Tests PUT /api/pets/:id to update an existing pet’s data.
- Retrieve All Pets: Tests GET /api/pets to retrieve all pet entries.
- Handle Missing Fields: Tests POST /api/pets with missing data to check for error handling.
- Retrieve a Pet by ID: Tests GET /api/pets/:id to fetch a specific pet.
- Delete a Pet Entry: Tests DELETE /api/pets/:id to ensure a pet entry is deleted properly.
- Handle Non-Existing Pet Requests: Checks PUT and GET requests for non-existing pet IDs, ensuring proper error responses.

## Test Coverage
This repository includes thorough test coverage across two key areas:

Unit Testing: Focuses on individual functions or modules to confirm they work as expected when isolated from the rest of the code. Each unit is tested with a range of inputs to ensure reliable and consistent behavior, helping to catch any issues early.

Integration Testing: Verifies that different parts of the API interact correctly. By testing how modules work together, integration testing ensures data flows smoothly between components, helping to catch issues that might only appear when components are combined.

## Viewing Test Results 
You can view test results in the CI pipeline both on GitHub and in your terminal when running tests locally. Here’s how:

	1.	View Test Results in GitHub Actions:
	1.	Go to the Repository on GitHub:
	•	Navigate to your project repository where the CI pipeline is set up.
	2.	Access the “Actions” Tab:
	•	In this tab, you’ll see all triggered workflows, such as from pushes or pull requests.
	•	The latest workflow appears at the top with statuses like ✔️ success, ❌ failure, or ⏳ in progress.
	3.	Select the Workflow:
	•	Click on the workflow to see its details. This opens a page showing each job created from the .yml file (e.g., build).
	4.	View the Job Log:
	•	Click on the job (e.g., build) to check logs for each step.
	•	Logs show details for steps like dependency installation, test execution, and any errors or failures.
	5.	Notifications and Test Reports:
	•	If a test fails, GitHub Actions provides error details, showing which assertions did not pass.
	
2.	View Test Results in Terminal (Local Testing):
	1.	Run Tests Locally:
	•	Run tests with the command:

```bash
npm test
```

	•	Results will appear in the terminal in real-time.

	2.	Test Results:
	•	The terminal shows detailed results, including:
	•	Number of tests passed and failed
	•	Time taken per test
	•	Error details for any failed assertions
	3.	Summary:
	•	At the end, the terminal provides a summary, such as Tests: 10 passed, 2 failed, giving an overview of the test outcomes.


## Adding New Tests
 ...

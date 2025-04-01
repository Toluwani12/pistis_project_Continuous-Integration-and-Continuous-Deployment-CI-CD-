1. **Create a Workflow Directory:** Create a directory for your GitHub Actions workflows:
`mkdir -p .github/workflows`

    ![](Img/mkdir.png)

2. **Create a Simple Workflow:** Create a new workflow file: `touch .github/workflows/main.yml`.
Open main.yml and add the following content:
    ```yaml
    name: CI   # The name of the workflow (CI stands for Continuous Integration)


    on: [push, pull_request]   # Triggers the workflow on every 'push' or 'pull request' to the repository

    jobs:
    build:  # The name of the job within this workflow
        runs-on: ubuntu-latest  # The job will run on the latest version of the Ubuntu runner provided by GitHub

        steps:
        # Step 1: Checkout the code from the repository
        - name: Checkout code
        uses: actions/checkout@v2   # Uses the GitHub-provided action to check out the repository's code

        # Step 2: Set up the Node.js environment
        - name: Set up Node.js
        uses: actions/setup-node@v2  # Uses the action to set up Node.js on the runner
        with:
            node-version: '14'   # Specifies that Node.js version 14 will be used

        # Step 3: Install project dependencies
        - name: Install dependencies
        run: npm install    # Runs 'npm install' to install dependencies from package.json

        # Step 4: Run the test suite
        - name: Run tests
        run: npm test  # Runs 'npm test' to execute the project's test scripts
    ```

### <mark>ERROR!!!</mark>
* After pushing it the first time I got the error: ![package_Error](Img/ERROR%201.png)

- **Troubleshooting:**
    * `sudo apt-get update`
    * `sudo apt-get install -f`

    *   `sudo apt-get clean`

        `sudo apt-get update --fix-missing`

        `sudo apt-get upgrade`
 
    * `sudo apt install npm`



# Building an Efficient CI/CD Pipeline for a Monorepo

### Context
Your company utilizes a monorepo structure to manage its codebase, with each service residing in its own dedicated folder. This approach promotes code sharing and consistency but introduces complexity when it comes to building an efficient Continuous Integration and Continuous Delivery (CI/CD) pipeline.

### Challenge
You need to create a GitHub Actions workflow that intelligently identifies changes within individual service folders and triggers the appropriate pipeline stages only for the affected services. This approach optimizes resource usage and reduces build times by avoiding unnecessary builds and deployments for services that haven't been modified.

### Instructions
- **Change Detection:** Implement a mechanism within your GitHub Actions workflow to accurately detect which service folders have been modified in a given commit.

- **Matrix Jobs:** Utilize matrix jobs in your workflow to dynamically generate separate jobs for each service that has undergone changes.
- **Pipeline Stages:** Define the necessary pipeline stages (e.g., build, test, deploy) within the matrix jobs. These stages should execute only for the services identified in step 1.
- **Conditional Execution:** Incorporate conditional logic to ensure that each pipeline stage runs only when the corresponding service has been modified.

**Answer:**


### ✅ STEP 1: I structuredProject as a Monorepo

I then created a folder with multiple services inside:

```bash
mkdir monorepo && cd monorepo
mkdir service-a service-b service-c
```

I added a sample file to each:

```bash
echo "console.log('Service A')" > service-a/index.js
echo "console.log('Service B')" > service-b/index.js
echo "console.log('Service C')" > service-c/index.js
```

I initialized and pushed to Git:

```bash
git init
git add .
git commit -m "Initial commit with monorepo structure"
git psuh
```
\

*(You need to have [GitHub CLI](https://cli.github.com/) installed and authenticated.)*

---

### ✅ STEP 2: Create the GitHub Actions Workflow

Inside the project, I created the GitHub Actions folder and workflow file:

```bash
mkdir -p .github/workflows
touch .github/workflows/monorepo-ci.yml
```
And pasted this in the yaml file - 
```yaml
name: Monorepo CI/CD

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  detect-changes:
    runs-on: ubuntu-latest
    outputs:
      services: ${{ steps.set-matrix.outputs.services }}
    steps:
      - uses: actions/checkout@v3

      - name: Get list of changed services
        id: set-matrix
        run: |
          changed_dirs=$(git diff --name-only ${{ github.event.before }} ${{ github.sha }} | cut -d/ -f1 | sort -u | uniq)
          services=$(echo $changed_dirs | jq -R -s -c 'split(" ") | map(select(. != ""))')
          echo "services=$services" >> $GITHUB_OUTPUT

  build-test-deploy:
    needs: detect-changes
    runs-on: ubuntu-latest
    if: needs.detect-changes.outputs.services != '[]'
    strategy:
      matrix:
        service: ${{ fromJson(needs.detect-changes.outputs.services) }}
    steps:
      - uses: actions/checkout@v3

      - name: Build ${{ matrix.service }}
        working-directory: ./${{ matrix.service }}
        run: echo "Building ${{ matrix.service }}..."

      - name: Test ${{ matrix.service }}
        working-directory: ./${{ matrix.service }}
        run: echo "Testing ${{ matrix.service }}..."

      - name: Deploy ${{ matrix.service }}
        working-directory: ./${{ matrix.service }}
        run: echo "Deploying ${{ matrix.service }}..."
```

---

### ✅ STEP 3: I commited and Pushed

```bash
git add .github
git commit -m "Add monorepo CI/CD workflow"
git push origin main
```
![alt text](Img\monorepo.png)


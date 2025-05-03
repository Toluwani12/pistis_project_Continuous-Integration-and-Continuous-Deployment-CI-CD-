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


# GitLab CI/CD Lab Guide with VSCode

### 1) Create a .gitlab-ci.yml File
Open .gitlab-ci.yml and add the following content to define a simple pipeline:
```yml
stages:
  - build   # The 'build' stage where build-related jobs are executed
  - test  # The 'test' stage where testing jobs are executed

build_job:
  stage: build
  script:
    - echo "Building the project..."
    - # Add your build commands here

test_job:
  stage: test
  script:
    - echo "Running tests..."
    - # Add your test commands here
```
Commit and push the .gitlab-ci.yml file to your repository using the VSCode Git interface:
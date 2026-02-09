
# **Task 2: Complex Jenkins Pipeline with Advanced Error Handling**

## Objective

The objective of Task 2 was to design and implement a **robust declarative Jenkins pipeline** that supports **dynamic parameters**, **error handling**, **retry logic**, and **post-build actions**, simulating real-world CI/CD behavior.



## 1. Declarative Pipeline with Dynamic Parameters

A **Declarative Jenkinsfile** was created to allow runtime inputs and flexible execution.

### Parameters Configured:

* **Git Branch Parameter**

  * A string parameter (`BRANCH`) with default value `master`
  * Allows users to choose which Git branch to build
* **Boolean Failure Simulation Parameter**

  * A boolean parameter (`FAIL_TEST`)
  * Used to intentionally simulate test failures for validating error handling

This makes the pipeline reusable and configurable without modifying code.


## 2. Pipeline Stages Implementation

The pipeline consists of **four sequential stages**, each representing a typical CI/CD lifecycle.

### Stage 1: Checkout

* Jenkins checks out code from the specified Git branch
* GitHub authentication is handled securely using a **Personal Access Token (PAT)** stored in Jenkins credentials
* Error handling is implemented using `try/catch` to gracefully fail the build if a non-existent branch is provided

**Outcome:**
Invalid branches fail early with a clear error message.


### Stage 2: Build

* Simulates application build using simple shell commands
* Represents compilation or packaging steps in a real-world pipeline

**Outcome:**
Build runs only if checkout succeeds.


### Stage 3: Test (with Retry Logic)

* Test execution is wrapped inside a `retry(2)` block
* If the test fails, Jenkins retries the stage up to **two times**
* The boolean parameter `FAIL_TEST` is used to intentionally trigger failures

**Outcome:**
Simulates flaky tests and validates retry-based error handling.


### Stage 4: Deploy

* Executes only if all previous stages pass successfully
* No explicit condition is required, as declarative pipelines automatically enforce stage order

**Outcome:**
Deployment is skipped if any earlier stage fails.


## 3. Advanced Error Handling Strategy

### Retry Mechanism

* Implemented at the **Test stage level**
* Prevents transient failures from immediately failing the pipeline
* Improves pipeline resilience

### Controlled Failure Simulation

* The `error` step is used to intentionally fail the pipeline when required
* Helps validate failure handling and notification logic


## 4. Post-Build Actions

Post-build actions were implemented using the `post` block to handle outcomes after pipeline execution.

### On Failure:

* Simulates sending an email notification using `echo`
* Ensures the team is notified when the pipeline fails

### On Success:

* Generates a log file
* Archives the log using `archiveArtifacts` for traceability and auditing


## 5. Automation Trigger (Optional)

* Jenkins job is configured to support **GitHub Webhook triggering**
* Allows automatic pipeline execution on code push events
* Eliminates the need for SCM polling


## Final Outcome

* Implemented a **parameterized, fault-tolerant Jenkins pipeline**
* Handled invalid inputs gracefully
* Added retry logic for flaky test scenarios
* Ensured controlled deployment
* Implemented post-build success and failure actions
* Followed Infrastructure-as-Code best practices by defining behavior in Jenkinsfile



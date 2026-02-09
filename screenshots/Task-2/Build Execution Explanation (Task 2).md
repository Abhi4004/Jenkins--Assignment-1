Build Execution Explanation (Task 2)

The Jenkins pipeline was executed with runtime parameters to validate dynamic behavior and error handling. When the FAIL_TEST parameter was set to true, the pipeline intentionally failed during the Test stage after retrying twice, demonstrating the configured retry mechanism and controlled failure handling. As expected, the Deploy stage was skipped, while post-build actions executed successfully to handle the failure scenario.

In a subsequent run, when FAIL_TEST was set to false, all stages including Checkout, Build, Test, and Deploy completed successfully. Upon successful completion, a log file (logs.txt) was generated and archived, which is visible under Last Successful Artifacts, confirming correct execution of post-success actions.

This validates that the pipeline correctly responds to parameter values, enforces retry logic, skips deployment on failure, and archives artifacts only on successful builds.
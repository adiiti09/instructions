# Typical CI/CD Pipeline Implementation in Jenkins
## Stages of typical CI pipeline

    Code Checkout from Git
    Compile
    Test

This pipeline should run every night, so it should be scheduled. 

## Stages of typical CD pipeline

    Code Checkout from Git
    Compile
    Test
    Deploy

This pipeline should run every time a merge happens to the default branch.


# Security Actions
- [Security Actions](#security-actions)
  - [Terraform](#terraform)
    - [TFSec](#tfsec)
  - [SonarQube/Cloud](#sonarqubecloud)
    - [SonarQube](#sonarqube)
    - [SonarCloud](#sonarcloud)
  - [Snyk Actions](#snyk-actions)
    - [Snyk NPM](#snyk-npm)
    - [Snyk Python](#snyk-python)
    - [Snyk Docker Images](#snyk-docker-images)

## Terraform
### TFSec
`actions/tfsec-action` will run the [Flexion/tfsec-action](https://github.com/flexion/flexion-sig-security/actions/tfsec-action) on all `pull_request` for the repositories. This simply runs the `tfsec` docker container from within an action. 

## SonarQube/Cloud
### SonarQube
[SonarSource/sonarqube-scan-action](https://github.com/SonarSource/sonarqube-scan-action) is an officially supported action for running the SonarQube CLI Scanner within Github Actions.
<details>
    <summary>Example</summary>
    ```yaml
        on:
        # Trigger analysis when pushing in master or pull requests, and when creating
        # a pull request. 
        push:
            branches:
            - master
        pull_request:
            types: [opened, synchronize, reopened]

        name: Main Workflow
        jobs:
        sonarqube:
            runs-on: ubuntu-latest
            steps:
            - uses: actions/checkout@v2
            with:
                # Disabling shallow clone is recommended for improving relevancy of reporting
                fetch-depth: 0
            - name: SonarQube Scan
            uses: sonarsource/sonarqube-scan-action@master
            env:
                SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
                SONAR_HOST_URL: ${{ secrets.SONAR_HOST_URL }}
    ```
</details>

### SonarCloud
[SonarSource/sonarcloud-github-action](https://github.com/SonarSource/sonarcloud-github-action) is an officially supported action for running the SonarCloud Scanner within Github Actions.
<details>
    <summary>Example</summary>
    ```yaml
        on:
        # Trigger analysis when pushing in master or pull requests, and when creating
        # a pull request.
        push:
            branches:
            - master
        pull_request:
            types: [opened, synchronize, reopened]
        name: SonarCloud Workflow
        jobs:
        sonarcloud:
            runs-on: ubuntu-latest
            steps:
            - uses: actions/checkout@v2
            with:
                # Disabling shallow clone is recommended for improving relevancy of reporting
                fetch-depth: 0
            - name: SonarCloud Scan
            uses: sonarsource/sonarcloud-github-action@master
            env:
                GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
                SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
    ```
</details>

## Snyk Actions
### Snyk NPM
[snyk/actions/node@master](https://github.com/snyk/actions/tree/master/node) is an action for running the [Snyk CLI](https://github.com/snyk/snyk) against Node projects.
<details>
    <summary>Example</summary>
    ```yaml
    name: Example workflow for Node using Snyk
    on: push
    jobs:
    security:
        runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@master
        - name: Run Snyk to check for vulnerabilities
            uses: snyk/actions/node@master
            env:
            SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
            with:
            args: --severity-threshold=high
    ```
</details>

### Snyk Python
[snyk/actions/python@master](https://github.com/snyk/actions/tree/master/python) is an action for running the [Snyk CLI](https://github.com/snyk/snyk) against Python projects.
<details>
    <summary>Example</summary>
    ```yaml
        name: Example workflow for Python using Snyk
        on: push
        jobs:
        security:
            runs-on: ubuntu-latest
            steps:
            - uses: actions/checkout@master
            - name: Run Snyk to check for vulnerabilities
                uses: snyk/actions/python@master
                env:
                SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
    ```
</details>

### Snyk Docker Images
[snyk/actions/docker@master](https://github.com/snyk/actions/tree/master/docker) is an action for running the [Snyk CLI](https://github.com/snyk/snyk) to check for vulnerabilities in your Docker images.
<details>
    <summary>Example</summary>
    ```yaml
        name: Example workflow for Docker using Snyk 
        on: push
        jobs:
        security:
            runs-on: ubuntu-latest
            steps:
            - name: Run Snyk to check Docker image for vulnerabilities
            uses: snyk/actions/docker@master
            env:
                SNYK_TOKEN: ${{ secrets.SNYK_TOKEN }}
            with:
                image: your/image-to-test
    ```
</details>
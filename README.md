# [Java] [GitHub Actions] Secure Pipelines Demo

[![CI_DevSecOps](https://github.com/adavarski/DevSecOps-GitHub-Actions-pipeline-java/workflows/CI_DevSecOps/badge.svg)](https://github.com/adavarski/DevSecOps-GitHub-Actions-pipeline-java/actions)

Sample Secure (DevSecOps) Pipeline with GithHub Actions (Ideal for Open Source Projects)

## Setup

- Add Snyk API Token in GitHub Repositority Secrets - SNYK_TOKEN (https://app.snyk.io/account to get SNYK_TOKEN - login with GH)
- Add Git Guardian API Token for in GitHub Repositority Secrets - GITGUARDIAN_API_KEY
- Add DockeHub (or used Docker Registry) credentials ( example: DOCKERHUB_USERNAME, DOCKERHUB_TOKEN)

## GitHub Actions Used 

| Step                                                    | Github Action                                                                            | Comments | Open Source Alternative                             |
| ------------------------------------------------------- | ---------------------------------------------------------------------------------------- | -------- | --------------------------------------------------- |
| Secrets Scanner                                         | [GitGuardian](https://github.com/GitGuardian/gg-shield-action)                           |          | [truffleHog](https://github.com/dxa4481/truffleHog) |
| SCA: Software Composition Analysis (Dependency Checker) | [snyk](https://github.com/marketplace/actions/snyk)                                      |          | OWASP Dependency Check                              |
| SCA: Software Composition Analysis (Dependency Checker) | GitHub Dependabot                                                                        |          |                                                     |
| SAST: Static Code Analysis                              | [Spot Bugs](https://github.com/jwgmeligmeyling/spotbugs-github-action)                   |          |                                                     |
| SAST: Static Code Analysis                              | [CodeQL](https://github.com/github/codeql-action)                                        |          |                                                     |
| Container Scan                                          | [Anchore](https://github.com/marketplace/actions/anchore-container-scan)                 |          |                                                     |
| Container Lint                                          | [Dockle](https://github.com/marketplace/actions/runs-dockle)                             |          |                                                     |
| K8s Hardening                                           | [Dockle](https://github.com/marketplace/actions/controlplane-kubesec)                    |          |                                                     |
| License Checker                                         | [License finder](https://github.com/pivotal/LicenseFinder)                               |          |                                                     |
| DAST: Dynamic Application Security Testing              | [OWASP ZAP Basline Scan](https://github.com/marketplace/actions/owasp-zap-baseline-scan) |          |                                                     |


```
Note: OWASP (Open Web Application Security Project) ZAP (Zed Attack Proxy) -> 

Follow the following steps for fixing ZAP scan error "Resource not accessible by integration"

Go to Settings of the repo

Click on Actions drop down on the left hand side of the web page

From the Actions drop down, Click on General

Scroll down, Under Workflow Permissions, see the permission

Make sure to Select Read and write permissions

Check "Allow GitHub Actions to create and aprove pull requests"

Click on Save button to save your changes.
```

### DevSecOps Pipeline

![GitHub Pipeline](imgs/pipeline_light.png)

### GH Actions References: 

List of GitHub Actions:

https://github.com/actions

https://github.com/marketplace?type=actions

Syntax: 

https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions



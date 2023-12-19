# [Java] [GitHub Actions] Secure Pipelines Demo

[![CI_DevSecOps](https://github.com/adavarski/DevSecOps-GitHub-Actions-pipeline-java/workflows/CI_DevSecOps/badge.svg)](https://github.com/adavarski/DevSecOps-GitHub-Actions-pipeline-java/actions)


Sample Secure Pipeline with GithHub Actions - Ideal for Open Source Projects

## Setup

- Add Snyk API Token in GitHub Repositority Secrets - SNYK_TOKEN
- Add Git Guardian API Token for in GitHub Repositority Secrets - GITGUARDIAN_API_KEY

## Actions Used

| Step                     | Github Action                                                                            | Comments | Open Source Alternative                             |
| ------------------------ | ---------------------------------------------------------------------------------------- | -------- | --------------------------------------------------- |
| Secrets Scanner          | [GitGuardian](https://github.com/GitGuardian/gg-shield-action)                           |          | [truffleHog](https://github.com/dxa4481/truffleHog) |
| SCA - Dependency Checker | [snyk](https://github.com/marketplace/actions/snyk)                                      |          | OWASP Dependency Check                              |
| Static Code Analysis     | [Spot Bugs](https://github.com/jwgmeligmeyling/spotbugs-github-action)                   |          |                                                     |
| Static Code Analysis     | [CodeQL](https://github.com/github/codeql-action)                                        |          |                                                     |
| Container Scan           | [Anchore](https://github.com/marketplace/actions/anchore-container-scan)                 |          |                                                     |
| Container Lint           | [Dockle](https://github.com/marketplace/actions/runs-dockle)                             |          |                                                     |
| K8s Hardening            | [Dockle](https://github.com/marketplace/actions/controlplane-kubesec)                    |          |                                                     |
| License Checker          | [License finder](https://github.com/pivotal/LicenseFinder)                               |          |                                                     |
| DAST                     | [OWASP ZAP Basline Scan](https://github.com/marketplace/actions/owasp-zap-baseline-scan) |          |                                                     |
|                          |                                                                                          |          |                                                     |

# Pipeline

![GitHub Pipeline](imgs/pipeline_light.png)

Note: 

OWASP (Open Web Application Security Project) ZAP (Zed Attack Proxy)

Note: K8s is Kubernetes. K3s is a lightweight K8s distribution. K3d is a wrapper to run K3s in Docker. K3d/K3s are especially good for development and CI purposes, as it takes only 20-30 seconds of time till the cluster is ready (for comparison, Kind/Minikube takes more time till ready)

Note: Follow the following steps for fixing ZAP scan error "Resource not accessible by integration"

Go to Settings of the repo

Click on Actions drop down on the left hand side of the web page

From the Actions drop down, Click on General

Scroll down, Under Workflow Permissions, see the permission

Make sure to Select Read and write permissions

Check "Allow GitHub Actions to create and aprove pull requests"

Click on Save button to save your changes.


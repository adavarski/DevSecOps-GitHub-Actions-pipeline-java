# DevSecOps Pipelines with GitHub Actions Demo [Java app] 

[![CI_DevSecOps](https://github.com/adavarski/DevSecOps-GitHub-Actions-pipeline-java/workflows/CI_DevSecOps/badge.svg)](https://github.com/adavarski/DevSecOps-GitHub-Actions-pipeline-java/actions)

Sample Secure (DevSecOps) Pipeline with GithHub Actions 

## Setup

- Add Snyk API Token in GitHub Repositority Secrets - SNYK_TOKEN (https://app.snyk.io/account to get SNYK_TOKEN - login with GH)
- Add Git Guardian API Token for in GitHub Repositority Secrets - GITGUARDIAN_API_KEY
- Add Docker Registry credentials ( Example -> DockerHub Registry: DOCKERHUB_USERNAME, DOCKERHUB_TOKEN)

## GitHub Actions Used 

| Step                                                    | Github Action                                                                            | Comments | Open Source Alternative                             |
| ------------------------------------------------------- | ---------------------------------------------------------------------------------------- | -------- | --------------------------------------------------- |
| Secrets Scanner                                         | [GitGuardian](https://github.com/GitGuardian/gg-shield-action)                           |          | [truffleHog](https://github.com/dxa4481/truffleHog) |
| SCA: Software Composition Analysis (Dependency Checker) | [snyk](https://github.com/marketplace/actions/snyk)                                      |          | OWASP Dependency Check                              |
| SCA: Software Composition Analysis (Dependency Checker) | GitHub Dependabot                                                                        |          |                                                     |
| SAST: Static Code Analysis                              | [Spot Bugs](https://github.com/jwgmeligmeyling/spotbugs-github-action)                   |          |                                                     |
| SAST: Static Code Analysis                              | [CodeQL](https://github.com/github/codeql-action)                                        |          |                                                     |
| Container Scan                                          | [Docker Scout](https://github.com/marketplace/actions/docker-scout)                      |          |                                                     |
| Container Scan                                          | [Trivy](https://github.com/marketplace/actions/aqua-security-trivy)                      |          |                                                     |
| Container Scan                                          | [Anchore](https://github.com/marketplace/actions/anchore-container-scan)                 |          |                                                     |
| Container Lint                                          | [Dockle](https://github.com/marketplace/actions/runs-dockle)                             |          |                                                     |
| K8s Hardening                                           | [Dockle](https://github.com/marketplace/actions/controlplane-kubesec)                    |          |                                                     |
| License Checker                                         | [License finder](https://github.com/pivotal/LicenseFinder)                               |          |                                                     |
| DAST: Dynamic Application Security Testing              | [OWASP ZAP Basline Scan](https://github.com/marketplace/actions/owasp-zap-baseline-scan) |          |                                                     |



### DevSecOps Pipeline

![GitHub Pipeline](imgs/pipeline_light.png)


### SCA Scan with Snyk:

SCA (Software Composition Analysis): check external dependencies/libraries used by the project have no known vulnerabilities. Third-party dependency scanning with Snyk.

Ref: Snyk:
- https://github.com/snyk/actions
- https://github.com/snyk/actions/tree/master/python-3.8
- https://snyk.io/partners/docker/ (Snyk: Configure integration for DockerHub for docker images scanning : https://docs.snyk.io/integrate-with-snyk/snyk-container-integrations/container-security-with-docker-hub-integration/configure-integration-for-docker-hub)

Note: https://app.snyk.io/account to get SNYK_TOKEN ( login with GH). Add Snyk API Token in GitHub Repositority Secrets - SNYK_TOKEN

Note: We can use Snyk for SCA (Software Composition Analysis) and Docker Scout for Docker Image scanning: (Bitbucket use Snyk for SCA for example)

Note: We can upload result (serif report) to GitHub Code Scanning using GitHub Action -> github/codeql-action/upload-sarif@v2 (Snyk GitHub integration @https://app.snyk.io/org/adavarski -> https://docs.snyk.io/integrate-with-snyk/git-repositories-scms-integrations-with-snyk/snyk-github-integration)

### Container Image Scanning with Trivy:
Identify vulnerabilities in built images -> Trivy Image Scanner

Ref: https://github.com/aquasecurity/trivy-action

### Deploy app to k8s (k3d) and OWASP ZAP Scan (DAST: Dynamic Application Security Testing)

OWASP (Open Web Application Security Project) 
ZAP (Zed Attack Proxy)

Note: K8s is Kubernetes. K3s is a lightweight K8s distribution. K3d is a wrapper to run K3s in Docker. K3d/K3s are especially good for development and CI purposes, as it takes only 20-30 seconds of time till the cluster is ready (for comparison, Kind/Minikube takes more time till ready)

Note: Follow the following steps for fixing ZAP scan error "Resource not accessible by integration"

1) Go to Settings of the repo

2) Click on Actions drop down on the left hand side of the web page

3) From the Actions drop down, Click on General

4) Scroll down, Under Workflow Permissions, see the permission

5) Make sure to Select Read and write permissions
   
7) Check "Allow GitHub Actions to create and aprove pull requests"

8) Click on Save button to save your changes.

Ref: https://github.com/zaproxy/action-baseline

Ref: https://github.com/zaproxy/action-full-scan

Ref: https://github.com/adavarski/k3d-GH-Actions

### How to generate scan reports (Snyk & Docker Scout & Trivy & OWASP ZAP)

### How to analyze scan reports (json & serif report files)

Ref: 
https://docs.github.com/en/code-security/code-scanning/integrating-with-code-scanning/sarif-support-for-code-scanning

SARIF (Static Analysis Results Interchange Format) 

Example: https://www.defectdojo.org

https://github.com/DefectDojo/django-DefectDojo

Add Product -> Add Engagemets (Import Scan results: SARIF files) -> Findings

TODO: defectdojo_send_scans.py or use/create GitHub action

<img src="imgs/defectdojo-java-app-ovwrview.png?raw=true" width="800">

<img src="imgs/defectdojo-java-app-findings.png?raw=true" width="800">


Add Product -> Add Engagemets (Import Scan results: SARIF files) -> Findings 

https://github.com/alexgracianoarj/gitlab-pipeline-demo/blob/main/.gitlab-ci.yml (example python script to upload scan results to defectdojo)

### GitHub Code Scanning using GitHub Actions and Github CodeQL for Code scanning (SAST : Static Application Security Testing)

Repo "Settings" - < Code Security and Analysis (setup Code scanning: Advanced -> codeql.yml workflow and view report after CodeQL workflow execution)

### Keeping supply chain secure with GitHub Dependabot (SCA : Software Composition Analysis)
Monitor vulnerabilities in dependencies used in your project and keep your dependencies up-to-date with Dependabot (dependabot.yml)

Ref: https://docs.github.com/en/code-security/getting-started/dependabot-quickstart-guide

Ref: https://docs.github.com/en/code-security/dependabot

Ref: https://docs.github.com/en/code-security/dependabot/working-with-dependabot/automating-dependabot-with-github-actions

Ref: https://github.blog/2022-09-09-sca-vs-sast-what-are-they-and-which-one-is-right-for-you/

Note: Dependabot raises pull requests to update dependencies. Depending on how your repository is configured, Dependabot may raise pull requests for version updates and/or for security updates. You manage these pull requests in the same way as any other pull request, but there are also some extra commands available. For information about enabling Dependabot dependency updates, see ["Configuring Dependabot security updates"](https://docs.github.com/en/code-security/dependabot/dependabot-security-updates/configuring-dependabot-security-updates) and ["Configuring Dependabot version updates."](https://docs.github.com/en/code-security/dependabot/dependabot-version-updates/configuring-dependabot-version-updates)

### GH Actions References: 

List of GitHub Actions:

https://github.com/actions

https://github.com/marketplace?type=actions

Syntax: 

https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions



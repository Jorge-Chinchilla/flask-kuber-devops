# Flask App to Kubernetes Engine
This repository is a step by step project on how to deploy a Flask Application to a Kubernetes cluster following DevOps 
best practices suck as CI/CD and basics of Infrastructure as Code using yaml files. 
---
## Scope
> Deploying a simple Flask Application to Google Kubernetes Engine, and expose it to https://[yourdomain].com
---
## What we'll be using:
* Github branching
* Docker
* Google Cloud
  * Google Kubernetes Engine
  * Cloudbuild
  * Artifact Registry
* Owned domain
---
## Guide

### Step 1:
Creating the GitHub repository with the development, staging and default main branches.
To ensure good practices when merging our features into the different stages, we create a ruleset that apply to these branches, and requires Pull Requests before merging.

1. Create your GitHub repository
2. Create the `main`, `staging` and `development` branches.
3. Setup a Ruleset that requires a Pull Request for merging on the above mentioned branches ![PR Branches](assets/images/pr_branches.png) ![Require Pull Requests](assets/images/pr_required.png)
4. Clone your repository locally to start the guide
### Step 2: Creating our test Flask App
In progress

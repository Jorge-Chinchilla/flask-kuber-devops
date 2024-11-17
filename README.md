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
Creating the GitHub repository with the development, staging and default main branches. To Prevent untested code to make its way into production, we'll require Pull requests via a repository Ruleset.

1. Create your GitHub repository
2. Create the `main`, `staging` and `development` branches.
3. Setup a Ruleset that requires a Pull Request for merging on the above mentioned branches ![PR Branches](assets/images/pr_branches.png) ![Require Pull Requests](assets/images/pr_required.png)
4. Clone your repository locally to start the guide

### Step 2: Creating our test Flask App
The main focus of the project is to deploy a production ready web application using CI/CD and GKE (Google Kubernetes Engine in GCP). For this project, we are building a simple Flask app.
```
.
.
├── Dockerfile
├── README.md
├── app.py
├── requirements.txt
├── .gitignore
├── .dockerignore
├── static
│           └── styles.css
└── templates
    └── index.html
```

1. Ensure you clone your repository locally.
2. Create a branch named 'feature/flask-app-start' and checkout to it. You can use `git checkout -b feature/flask-app-start` to create and navigate to the branch locally.
2. Create the Dockerfile. .dockerignore, app.py, requirements.txt, styles.css and index.html files which build your containerized flask app. You can find the source code in this repository.
3. Test your app.
   - Ensure you have Docker installed and running on your system
   - Open your terminal and navigate to the root of your directory
   - Build your image with the command `docker build -t test-flask-image .`
     - You can list the images created with `docker images` command
   - Run your image in a new container with the command `docker run --name flask-app-container -p 5001:5000 test-flask-image`.
   - Go to localhost:5001 on your browser ensure your app is running as expected.
10. Commit and push your changes to the repository.

### Step 3: Google Cloud Setup
The app will be deploy in kubernetes cluster in Google Cloud, to avoid charges to our credit cards, we will create an account with a 90 days trial and 300$ in credits.
All details are listed in the [Google Cloud Free Program](https://cloud.google.com/free/docs/free-cloud-features) documentation.
1. Creating your free account (summarized):
   - Login with a Google Account that has not been registered in Google Cloud
   - Follow the steps for enabling your Free Trial
   - Setup your billing information
5. Create a Project [Creating a Google Cloud project](https://developers.google.com/workspace/guides/create-project). Projects allow us to organize our cloud resources.
6. Search for the GKE Service ![GKE Search](assets/images/gke_search.png)
7. Enable the Kubernetes Engine API ![GKE Enable](assets/images/gke_enable.png)
8. Wait for a few minutes, then go to the Kubernetes Engine service again to create your cluster: ![Create cluster](assets/images/cluster_create.png)
9. On the creation screen, follow this steps:
   - Switch to *standard cluster* creation ![Switching to standard creation](assets/images/cluster-standard.png)
   - Set cluster name to "master-cluster" and Location type to Zonal as it is cheaper than regional. Consider Regional types for production deployments for High Availability. ![cluster setting](assets/images/cluster-settings.png)
   - To reduce costs during this demo, click on the "default-pool" options in your left panel, then click on Nodes and change the machine type to **e2-micro** and Boot disk size to 20GB, this should change the estimated cost for the GKE cluster to ~97.34$ monthly.
10. Wait a few minutes for the cluster to create, and then click on the three dots to connect to the cluster. You can connect via the built in Cloud Shell, or setup the Google Cloud CLI on your machine ([Install the gcloud CLI](https://cloud.google.com/sdk/docs/install)).
11. If you setup the Google CLI, you might get the error "gke-gcloud-auth-plugin not found", if so, install it using the `  gcloud components install gke-gcloud-auth-plugin` command.


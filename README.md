# spring-gumball ci/cd example

### This example demonstrates the following two GitHub Workflows.

* https://help.github.com/actions/language-and-framework-guides/building-and-testing-java-with-gradle

* https://github.com/google-github-actions/setup-gcloud/tree/master/example-workflows/gke

### Build Dependencies

* Gradle 5.6
* JDK 11


# Journal

## CI Workflow

![](images/01_gradle_workflow.png)
![](images/02_yaml.png)

Create a new "Java CI with Gradle" workflow in Actions -> New workflow and change the yml file if needed.
This creates a new CI workflow whenever there is a push or pull request.

![](images/03_edit.png)

Edit the source code then push it.

![](images/04_gradle_workflow.png)
![](images/05_gradle_workflow.png)
![](images/06_gradle_workflow.png)
![](images/07_gradle_workflow.png)
![](images/08_gradle_workflow.png)
![](images/09_gradle_workflow.png)

The CI workflow is executed, and it performs a series of actions as specified in the yml file.

## CD Workflow

![](images/10_cluster.png)
![](images/11_cluster.png)

Create a new cluster on Google Kubernetes Engine.

![](images/12_enable_api.png)
![](images/13_api.png)
![](images/14_api.png)

Enable Container Registry API and Kubernetes Engine API for the project.

![](images/15_project_id.png)
![](images/16_service_account.png)
![](images/17_service_account.png)
![](images/18_service_account.png)

Create a new Service account that has the roles "Kubernetes Engine Developer" and "Storage Admin".

![](images/19_private_key.png)
![](images/20_private_key.png)

Create a new Private key for the Service account and save the JSON file on the computer.

![](images/21_secret.png)
![](images/22_secret.png)
![](images/23_secret.png)
![](images/24_secret.png)

Create 2 Secrets for the GitHub repository. This enables the CD Workflow to connect to GKE.

![](images/25_gke_workflow.png)

Create a new "Build and Deploy to GKE" CD workflow in Actions -> New workflow. The yml file uses Secrets
created in the previous step to connect to GKE.

![](images/26_release.png)
![](images/27_release.png)

Create a new Release, which executes the CD workflow automatically.

![](images/28_gke_workflow.png)
![](images/29_workflows.png)
![](images/30_gke-workflow.png)
![](images/31_gke_workflow.png)
![](images/32_gke_workflow.png)

The CD workflow is executed when a new Release on the repository is created.

![](images/33_deployment.png)

The CD workflow creates a "spring-gumball-deployment" Deployment on GKE using deployment.yaml.

![](images/34_service.png)

The CD workflow also creates a "spring-gumball-service" Service on GKE using service.yaml.

![](images/35_ingress.png)
![](images/36_ingress.png)
![](images/37_ingress.png)
![](images/38_ingress.png)
![](images/39_ingress.png)

Create a new Ingress for the "spring-gumball-service" to create a public IP address and 
make it accessible from the browser.

![](images/40_gumball.png)
![](images/41_gumball.png)

Access the "spring-gumball" webpage using the IP address of the Ingress. Server Host/IP changes when
the user refreshes the page or interact with the page, which proves the load balancer at work.


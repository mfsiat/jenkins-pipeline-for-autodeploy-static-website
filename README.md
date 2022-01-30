# Jenkins-pipeline-for-autodeploy-static-website

We will deploy a static website using Jenkins pipeline

## Prerequisites

1. Jenkins (version 2 or later) installed with [SSH](https://plugins.jenkins.io/ssh/) and [SSH Pipeline Steps plugin](https://plugins.jenkins.io/ssh-steps/)
2. A remote server with nginx installed

## Creating The Pipeline

1. First we open the Jenkins panel and create a new pipeline job

    ![](/snapshots/creating-new-job.png)

2. We put the Jenkinsfile content in the pipeline script section and save the job

    ![](/snapshots/pipeline-script.png)

4. On ```Home->Manage Jenkins->Configure System->SSH remote hosts``` section we put our remote server credentials
5. Now go to our job page and click "Build Now". Our Jenkins pipeline should start building

    ![](/snapshots/jenkins-job.png)

7. To check this we can hit our remote server url and our static HTML website should be up and running

    ![](/snapshots/before-change.png)

9. To check the pipline functionality properly we can change our codebase and again build the pipeline. The change should be reflected in the website

    ![](/snapshots/after-change.png)

10. To configure automatic job trigger we can select "GitHub hook" or "Poll SCM" or any other from the Build Triggers section of the job

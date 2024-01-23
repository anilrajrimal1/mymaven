# Project 4: CI/CD Setup with GitHub, Jenkins, Maven & Tomcat

  ![project-image](https://github.com/anilrajrimal1/mymaven/blob/master/screenshots/project%20image.png)

## Overview

This project focuses on setting up a Continuous Integration/Continuous Deployment (CI/CD) pipeline using GitHub, Jenkins, Maven, and Tomcat. The primary objectives include setting up Jenkins, configuring Maven and Git, setting up a Tomcat Server, integrating GitHub, Maven, and Tomcat Server with Jenkins, creating CI and CD jobs, and testing the deployment of a Java web application.

# Table of Contents

1. [Installing and Configuring Tomcat Server](#installing-and-configuring-tomcat-server)
2. [Installing and Configuring Maven](#installing-and-configuring-maven)
3. [Jenkins Pipeline for Maven Java Web App](#jenkins-pipeline-for-maven-java-web-app)

## 1. Installing and Configuring Tomcat Server

This section provides instructions for installing and configuring Tomcat Server as part of the CI/CD pipeline setup. It outlines the essential steps to ensure a successful deployment environment for the Java web application.

### Project File

- [install_tomcat.md](https://github.com/anilrajrimal1/mymaven/blob/master/install_tomcat.md) - Read this file containing Complete instructions for installing and configuring Tomcat Server.

## 2. Installing and Configuring Maven

This section provides instructions for installing and configuring Maven as part of the CI/CD pipeline setup. It covers the necessary steps to set up Maven on the Jenkins server, enabling seamless integration for building and packaging Java web applications.

### Project File
- [install_maven.md](https://github.com/anilrajrimal1/mymaven/blob/master/install_maven.md) - Read this file containing Complete instructions for installing and configuring Maven.

## 3. Jenkins Pipeline for Maven Java Web App

This section details the Jenkins pipeline for building and deploying Java web applications using Maven. It guides you through configuring Jenkins to automate the integration of Maven, GitHub, and Tomcat Server. The pipeline includes steps for pulling source code, building the Maven project, packaging the Java web application, and deploying the artifact.

### Creating a New Repo in GitHub for Our Java-based Web Website

To start, follow these steps to create a new repository on GitHub for your Java-based web application.

- Login to GitHub.
- Create a new repository named `mymaven`.
  ![repo-maven](https://github.com/anilrajrimal1/mymaven/blob/master/screenshots/github%20repo.png)
- Copy the repository URL.

On the developer's machine:

```bash
# Create a folder for your project
mkdir -p /root/project/mymaven
cd /root/project/mymaven/

# Clone an existing Maven project or initialize a new one
git pull <any existing Maven project>
# Remove unnecessary files if any

# Initialize and push to the new GitHub repository
git init
git remote add origin <your repo URL>
git pull origin master
git add -A
git commit -m "maven java web app first commit"
git push origin master
```
### Install the "Deploy to Container" Plugin in Jenkins Master
Ensure the Jenkins master is set up with the necessary plugins.
  ![deploy-plugin](https://github.com/anilrajrimal1/mymaven/blob/master/screenshots/Deploy%20to%20container%20plugin%20download.png)
```markdown
- Open Jenkins dashboard.
- Navigate to "Manage Jenkins" 
    -> "Manage Plugins."
- In the "Available/Installed"
    -> Search for "Deploy to Container."
- Install the plugin without restarting Jenkins.
```
Start and enable the NTP server:
  ![start-enable](https://github.com/anilrajrimal1/mymaven/blob/master/screenshots/chronyd%20setup.png)
```bash
systemctl start chronyd
systemctl enable chronyd
```
### Creating a Jenkins Job for Maven Java Web App Deployment
Follow these steps to create a Jenkins job for building and deploying your Java web application.

- Open Jenkins dashboard.

- Create a new freestyle project.
  ![freestyle-job](https://github.com/anilrajrimal1/mymaven/blob/master/screenshots/create%20jenkins%20job.png)

- Set Git repository URL and credentials.
  ![git-code](https://github.com/anilrajrimal1/mymaven/blob/master/screenshots/add%20repo%20to%20job.png)

- Use "Poll SCM" for build triggers.
  ![buld-trrigres](https://github.com/anilrajrimal1/mymaven/blob/master/screenshots/poll%20scm.png)

- Configure build steps for Maven and Invoke top-level Maven target.
  ![top-level](https://github.com/anilrajrimal1/mymaven/blob/master/screenshots/top%20level%20maven.png)

- Add a post-build action to deploy the WAR file to a Tomcat container.
  ![post-build](https://github.com/anilrajrimal1/mymaven/blob/master/screenshots/post%20build%20action.png)

- Configure container details, including the URL, credentials, and WAR file path.
  ![global-cred](https://github.com/anilrajrimal1/mymaven/blob/master/screenshots/jenkins%20credentials%20.png)

- Apply and save the configuration.

Access your deployed web application at http://your-ip-address/javaweb.

  ![webserver-output](https://github.com/anilrajrimal1/mymaven/blob/master/screenshots/tomcat%20final%20output.png)




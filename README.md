
## 3. Jenkins Pipeline for Maven Java Web App

This section details the Jenkins pipeline for building and deploying Java web applications using Maven. It guides you through configuring Jenkins to automate the integration of Maven, GitHub, and Tomcat Server. The pipeline includes steps for pulling source code, building the Maven project, packaging the Java web application, and deploying the artifact.

### Creating New Repo in GitHub for Our Java-based Web Website

To start, follow these steps to create a new repository on GitHub for your Java-based web application.

- Login to GitHub.
- Create a new repository named `mymaven`.
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
### Install "Deploy to Container" Plugin in Jenkins Master
Ensure the Jenkins master is set up with the necessary plugins.

```markdown
- Open Jenkins dashboard.
- Navigate to "Manage Jenkins" 
    -> "Manage Plugins."
- In the "Available/Installed"
    ->search for "Deploy to Container."
- Install the plugin without restarting Jenkins.
```
Start and enable the NTP server:

```bash
systemctl start chronyd
systemctl enable chronyd
```
### Creating a Jenkins Job for Maven Java Web App Deployment
Follow these steps to create a Jenkins job for building and deploying your Java web application.

- Open Jenkins dashboard.

- Create a new freestyle project.

- Set Git repository URL and credentials.

- Use "Poll SCM" for build triggers.

- Configure build steps for Maven and top-level Maven invoker.

- Add a post-build action to deploy the WAR file to a Tomcat container.

- Configure container details, including the URL, credentials, and WAR file path.

- Apply and save the configuration.

Access your deployed web application at http://your-ip-address/javaweb.

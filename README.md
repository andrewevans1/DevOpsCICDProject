# DevOps Course: CI/CD Project 1
## Building a CI/CD Pipeline with Jenkins

Build a web app with Springboot, Maven, Git, Jenkins, Tomcat, AWS EC2, JUnit

## Procedure
### Create Git Repository
1. From Github.com, create a new repository
2. From command line, git clone <repository url>

### Create Sprintboot App
1. Go to start.spring.io
2. Set the following
- Project = Maven Project
- Language = Java
- Sprint Boot = 2.4.2
- Packaging = Jar
- Java = 8
3. Click Add Depenedencies > Spring Web
4. Click Generate
5. Extract downloaded zip file to project directory (git repo)

### Create Jenkins Build Job
1. From the Jenkins dashboard, select New Item > Freestyle Project. Name the project "CICD-Project1-Build"
2. Under Source Code Management, select Git. Paste the link to your github repo in the Repository URL field.
3. Under Build Triggers, select Poll SCM. Enter "0 0 * * *" to check every night for new commits to trigger a build.
4. Under Build Environment, select Delete workspace before build starts
5. Under Build, select Add build step > Execute Shell. Enter "mvn spring-boot:build-image" in the Command field.
6. Under Post-build Actions select Ad post-build action > Build other projects.
7. Enter CICD-Project1-Test in the Projects to build field, and select Trigger only if build is stable.

### Create Jenkins Test Job

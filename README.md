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
- Sprint Boot = 2.4.6
- Packaging = War
- Java = 8
3. Click Add Depenedencies > Spring Web
4. Click Generate
5. Extract downloaded zip file to project directory (git repo)

### Add Unit Tests

### Configure Jenkins
1. From the Jenkins dashboard, select Mangage Jenkins > Manage Plugins.
2. Search for Build Pipeline, and install.
3. Search for Copy Artifact, and install.
4. Search for Deploy to container, and install.
5. Search for AWS Elastic Beanstalk, and install.

### Create Jenkins Build Job
1. From the Jenkins dashboard, select New Item > Freestyle Project. Name the project "CICD-Project1-Build"
2. Under Source Code Management, select Git. Paste the link to your github repo in the Repository URL field.
3. Under Build Triggers, select Poll SCM. Enter "0 0 * * *" to check every night for new commits to trigger a build.
4. Under Build Environment, select Delete workspace before build starts
5. Under Build, select Add build step > Execute Shell. Enter "mvn spring-boot:build-image" in the Command field.
6. Under Post-build Actions select Add post-build action > Archive the artifacts.
7. Enter "target/*.war" in the Files to archive field.
8. Under Post-build Actions select Add post-build action > Build other projects.
9. Enter CICD-Project1-Test in the Projects to build field, and select Trigger only if build is stable.

### Create Jenkins Test Job
1. From the Jenkins dashboard, select New Item > Freestyle Project. Name the project "CICD-Project1-Test"
2. Under Source Code Management, select Git. Paste the link to your github repo in the Repository URL field.
3. Under Build, select Add build step > Execute shell. Enter "mvn test" as the Command.
4. Under Post-build Actions select Add post-build action > Build other projects.
5. Enter CICD-Project1-Deploy in the Projects to build field, and select Trigger only if build is stable.
6. Under Post-build Actions select Add post-build action > Publish Junit test result report.
7. Enter "target/surefire-reports/*.xml" in the Test report XMLs field.
8. Save.

### Create Jenkins Pipeline View
1. 
2. 
3. 
  
### Create AWS Project
1. Sign into AWS as root user.
2. Create an Elastic-Beanstalk environment named Devopscicdproject-env and a Project named DevOpsCICDProject
3. Copy AWS Credential and region
  
### Create Jenkins Deploy Job
1. From the Jenkins dashboard, select New Item > Freestyle Project. Name the project "CICD-Project1-Deploy"
2. Under Build Environment, select "Delete workspace before build starts"
3. Under Build, select Add build step > Copy artifacts from another project. Set the following
  - Project name: CICD-Project1-Build
  - Which build: Latest successful build
  - Artifacts to copy: **/*.war
4. Under Build, select Add build step > AWS Elastic Beanstalk. Set the following
  - AWS Credentials and Region
    - Credentials: copied from above
    - AWS Region: copied from above
  - Application and Environment
    - Application Name: DevOpsCICDProject
    - Devopscicdproject-env
  
  

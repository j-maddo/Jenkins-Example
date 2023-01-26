Please note, the below steps are for UNIX systems.
Proceed to follow the below steps only after ensuring Docker is installed on the host machine

Docker
Set up Docker to run the Jenkins containers:
Head to https://github.com/jenkinsci/docker

Create a script or simply execute the script via the terminal to start executing Jenkins if a volume does not already exist on your machine
docker run -p 8080:8080 -p 50000:50000 --restart=on-failure -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk11

Copy the admin password to login to jenkins from /var/jenkins_home/secrets/initialAdminPassword

Browser 
In browser, type in port specified. For this example, that will be localhost:8080. 
Unlock Jenkins with the admin password you copied previously.
A Getting Started page should appear that will allow you to customize your Jenkins pipeline with plugins. Feel free to choose your own adventure here.
--
After plugins have been installed, create your first admin user by filling out the input fields on the Create First Admin User Page.
On the Instance Configuration page, for simplicity, click the Save and Finish button.
The Jenkins is ready page should pop up. Click the Start using Jenkins button to move forward.
--

Pipeline creation
Click the Create a job link

Name your pipeline, click Pipeline from the list of options, then click the Ok button.

Configure pipeline
Define your build triggers.
This repo will use Poll SCM to leverage the source code manager, GitHub to run jobs. To do this go to the General >> Pipeline >> Definition. Click the Definition dropdown to select Pipeline Script from SCM (source code manager).
The SCM will be Git. The repo will be whichever GitHub repo you wish to have Jenkins as a CI/CD provider.

** Note: When using GitHub with Jenkins, you will likely need to add credentials for Jenkins to have access to the repo. SSH is the easiest way
Either generate one using this userflow https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent or enter an existing one.
SSH Username with private key


** Note: This repo will be using Declarative Jenkins syntax to build declarative pipelines. If unfamiliar with Declarative pipelines, check out https://www.jenkins.io/doc/book/pipeline/syntax/ for more information.



Add a Dockerfile
This repo will use the docker image from:
https://github.com/cypress-io/cypress-docker-images/tree/master/browsers/node18.6.0-chrome105-ff104

Install the Docker Jenkins plugin to avoid 'WorkflowScript: 3: Invalid agent type "docker" specified.' error

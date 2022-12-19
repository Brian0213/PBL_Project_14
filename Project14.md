# EXPERIENCE CONTINUOUS INTEGRATION WITH JENKINS | ANSIBLE | ARTIFACTORY | SONARQUBE | PHP

## PREREQUISITES

- Links to documentation to study:

[Java](https://en.wikipedia.org/wiki/Java)

[.Net](https://en.wikipedia.org/wiki/.NET_Framework)

[Php](https://en.wikipedia.org/wiki/PHP)

[JavaScript](https://en.wikipedia.org/wiki/JavaScript)

- Install Jenkins on the server:

![Ansible Mysql Download](./images/ansible-mysql.PNG)

- Add command to the bash files:

`sudo vi .bash_profile`

![Bash Profile](./images/bash-profile.PNG)

`source ~/.bash_profile`

![Bash Reload](./images/bash-reload.PNG)

- Check Jenkins status

`sudo systemctl start jenkins`

`sudo systemctl enable jenkins`

`sudo systemctl status jenkins`

![Jenkins Success](./images/jenkins-status.PNG)

`sudo systemctl daemon-reload`

![Daemon reload](./images/daemon-reload.PNG)

- To display jenkins initial password:

`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`

![Jenkins Password](./images/jenkins-initial-pass.PNG)

- Pick the option Install Selected plug-in

![Jenkins Password](./images/jenkins-install-sel.PNG)

- Install & Open Blue Ocean Jenkins Plugin:

![Blue Ocean Install](./images/jenkins-blueocean-install.PNG)

- Create a new pipeline:

- Select GitHub

- Connect Jenkins with GitHub

- Login to GitHub & Generate an Access Tokenhttps://www.darey.io/wp-content/uploads/2021/07/Jenkins-Create-Access-Token-To-Github.png

- Copy Access Token

- Paste the token and connect

- Create a new Pipeline

- At this point you may not have a Jenkinsfile in the Ansible repository, so Blue Ocean will attempt to give you some guidance to create one. But we do not need that. We will rather create one ourselves. So, click on Administration to exit the Blue Ocean console.

- Let us create our Jenkinsfile
Inside the Ansible project, create a new directory deploy and start a new file Jenkinsfile inside the directory.

![Deploy Jenkinsfile](./images/deploy-jenkins.PNG)

- Add the code snippet below to start building the Jenkinsfile gradually. This pipeline currently has just one stage called Build and the only thing we are doing is using the shell script module to echo Building Stage:

![Deploy Jenkinsfile Update](./images/deploy-jenkinsf-update.PNG)

- Now go back into the Ansible pipeline in Jenkins, and select configure:

- Update the Build Configuration script path to display the path of the Jenskinsfile:

 ![Deploy Jenkinsfile Path](./images/build-scriptph-deployjenkinsf.PNG)

 - Scroll down to Build Configuration section and specify the location of the Jenkinsfile at deploy/Jenkinsfile:

  ![Build Configure](./images/build-configure-output.PNG)

  - Back to the pipeline again, this time click "Build now":

  - This will trigger a build and you will be able to see the effect of our basic Jenkinsfile configuration by going through the console output of the build.

To really appreciate and feel the difference of Cloud Blue UI, it is recommended to try triggering the build again from Blue Ocean interface.

- Click on Blue Ocean

![Blueocean Jenkinsfile](./images/blueocean-jenkinsf-output.PNG)

- Select your project

- Click on the play button against the branch:

![Branch Output](./images/branch-output.PNG)

- Notice that this pipeline is a multibranch one. This means, if there were more than one branch in GitHub, Jenkins would have scanned the repository to discover them all and we would have been able to trigger a build for each branch.

- Let us see this in action.

- Create a new git branch and name it feature/jenkinspipeline-stages.

- Currently we only have the Build stage. Let us add another stage called Test. Paste the code snippet below and push the new changes to GitHub

![Branch Output](./images/branch-output.PNG)
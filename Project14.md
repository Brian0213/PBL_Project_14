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

- To make your new branch show up in Jenkins, we need to tell Jenkins to scan the repository.

- Click on the "Administration" button

- Navigate to the Ansible project and click on "Scan repository now"

- Refresh the page and both branches will start building automatically. You can go into Blue Ocean and see both branches there too.

![New Branch](./images/new-branch.PNG)

![Jenkins File](./images/Jenkinsf-build-test.PNG)

- In GitHub, create a pull and merge, navigate to Jenkins Blueocean and confirm the GitHub actions:

 ![Jenkins File](./images/blueo-main-update1.PNG)

 - A QUICK TASK FOR YOU!

 1. Create a pull request to merge the latest code into the main branch.

2. After merging the PR, go back into your terminal and switch into the main branch.

3. Pull the latest change.

4. Create a new branch, add more stages into the Jenkins file to simulate below phases. (Just add an echo command like we have in build and test stages)
   1. Package 
   2. Deploy 
   3. Clean up
5. Verify in Blue Ocean that all the stages are working, then merge your feature branch to the main branch

6. Eventually, your main branch should have a successful pipeline like this in blue ocean

Display Jenkins worksapce:

`ls -l /var/lib/jenkins/workspace/`

![Jenkins File](./images/jenkins-workspace.PNG)

![Quick Task](./images/quick-task.PNG)

![Main Output](./images/blueo-main-latest.PNG)

- Clean up output:

![Main Output](./images/cleanup-output.PNG)

### RUNNING ANSIBLE PLAYBOOK FROM JENKINS

Now that you have a broad overview of a typical Jenkins pipeline. Let us get the actual Ansible deployment to work by:

1. Installing Ansible on Jenkins

![Ansible Install](./images/ansible-success.PNG)

![Ansible Version](./images/ansible-version.PNG)

- Install Dependencies:

`sudo apt-get install python3-pip`

`python3 -m pip install --upgrade setuptools`

`python3 -m pip install --upgrade pip`

`python3 -m pip install PyMySQL`

`python3 -m pip install mysql-connector-python`

![Dependency Installation](./images/depend-install-5.PNG)

`python3 -m pip install psycopg2==2.7.5 --ignore-installed`

![Dependency Installation](./images/depend-install-6.PNG)

-Install Postgres Sql Database:

![Postgresql Installation](./images/postgresql-install.PNG)

2. Installing Ansible plugin in Jenkins UI:

![Postgresql Installation](./images/ansible-jenkins-install.PNG)

3. Creating Jenkinsfile from scratch. (Delete all you currently have in there and start all over to get Ansible to run successfully)
You can watch a 10 minutes video here to guide you through the entire setup

Note: Ensure that Ansible runs against the Dev environment successfully.

Possible errors to watch out for:

Ensure that the git module in Jenkinsfile is checking out SCM to main branch instead of master (GitHub has discontinued the use of Master due to Black Lives Matter. You can read more here)

Jenkins needs to export the ANSIBLE_CONFIG environment variable. You can put the .ansible.cfg file alongside Jenkinsfile in the deploy directory. This way, anyone can easily identify that everything in there relates to deployment. Then, using the Pipeline Syntax tool in Ansible, generate the syntax to create environment variables to set.

![Jenkins Build Documentation](https://wiki.jenkins.io/display/JENKINS/Building+a+software+project)

- Create anisble.cfg file insode the deploy folder

![Ansible Cfg file](./images/ansible-cfg-1.PNG)

![Ansible Cfg file](./images/ansible-cfg-2.PNG)

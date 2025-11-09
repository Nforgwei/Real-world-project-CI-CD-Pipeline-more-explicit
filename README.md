# Real-world-project-CI-CD-Pipeline-more-explicit
End to End real world ci/cd pipeline



End-to-End Jenkins CI/CD Pipeline Project Architecture (Java Web Application)
CompleteCICDProject!Project ToolBox 🧰
Git Git will be used to manage our application source code.
Github Github is a free and open source distributed VCS designed to handle everything from small to very large projects with speed and efficiency
Jenkins Jenkins is an open source automation CI tool which enables developers around the world to reliably build, test, and deploy their software
Maven Maven will be used for the application packaging and building including running unit test cases
Checkstyle Checkstyle is a static code analysis tool used in software development for checking if Java source code is compliant with specified coding rules and practices.
SonarQube SonarQube Catches bugs and vulnerabilities in your app, with thousands of automated Static Code Analysis rules.
Nexus Nexus Manage Binaries and build artifacts across your software supply chain
Ansible Ansible will be used for the application deployment to both lower environments and production
EC2 EC2 allows users to rent virtual computers (EC2) to run their own workloads and applications.
Slack Slack is a communication platform designed for collaboration which can be leveraged to build and develop a very robust DevOps culture. Will be used for Continuous feedback loop.
Prometheus Prometheus is a free software application used for event/metric monitoring and alerting for both application and infrastructure.
Grafana Grafana is a multi-platform open source analytics and interactive visualization web application. It provides charts, graphs, and alerts for the web when connected to supported data sources.
Splunk Splunk is an innovative technology which searches and indexes application/system log files and helps organizations derive insights from the data.
Jenkins Complete CI/CD Pipeline Environment Setup Runbook
Create a GitHub Repository with the name Jenkins-CICD-Project and push the code in this branch(main) to your remote repository (your newly created repository).Go to GitHub (github.com)
Login to your GitHub Account
Open this page and click Fork.
My repo is going to be replicated on your Github Account
Confirm that the code exist on GitHub
Jenkins/Maven/AnsibleCreate an Amazon Linux 2 VM instance and call it "jenkins-maven-ansible"
Instance type: t2.medium
Security Group (Open): 8080, 9100 and 22 to 0.0.0.0/0
Key pair: Select or create a new keypair
User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/maven-nexus-sonarqube-jenkins-install/jenkins-install.sh
Launch Instance
SonarQubeCreate an Create an Ubuntu 20.04 VM instance and call it "SonarQube"
Instance type: t2.medium
Security Group (Open): 9000, 9100 and 22 to 0.0.0.0/0
Key pair: Select or create a new keypair
User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/maven-nexus-sonarqube-jenkins-install/sonarqube-install.sh
Launch Instance
NexusCreate an Amazon Linux 2 VM instance and call it "Nexus"
Instance type: t2.medium
Security Group (Open): 8081, 9100 and 22 to 0.0.0.0/0
Key pair: Select or create a new keypair
User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/maven-nexus-sonarqube-jenkins-install/nexus-install.sh
Launch Instance
EC2 (Dev/Stage/Prod)Create 3 Amazon Linux 2 VM instance and call them (Names: Dev-Env, Stage-Env and Prod-Env)
Instance type: t2.micro
Security Group (Open): 8080, 9100, 9997 and 22 to 0.0.0.0/0
Key pair: Select or create a new keypair
User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/tomcat-splunk-installation/tomcat-ssh-configure.sh
Launch Instance
PrometheusCreate an Ubuntu 20.04 VM instance and call it "Prometheus"
Instance type: t2.micro
Security Group (Open): 9090 and 22 to 0.0.0.0/0
Key pair: Select or create a new keypair
Launch Instance
GrafanaCreate an Ubuntu 20.04 VM instance and call it "Grafana"
Instance type: t2.micro
Security Group (Open): 3000 and 22 to 0.0.0.0/0
Key pair: Select or create a new keypair
Launch Instance
EC2 (Splunk)Create an Amazon Linux 2 VM instance and call it (Names: Splunk-Server)
Instance type: t2.micro
Security Group (Open): 22, 8000, 9997, 9100 to 0.0.0.0/0
Key pair: Select or create a new keypair
Launch Instance
NOTE: Confirm and make sure you have a total of 8 VM instances
PipelineEnvSetup!SlackGo to the bellow Workspace and create a Private Slack Channel and name it "yourfirstname-jenkins-cicd-pipeline-alerts"
Link: https://join.slack.com/t/realworldcicdproject/shared_invite/zt-1tryd7x1v-g8a~zEJBKKchVvvK87jkeQ
You can either join through the browser or your local Slack App
Create a Private Channel using the naming convention cicd-pipeline-project-alerts
Click on the Drop down on the Channel and select Integrations and take Add an App
Search for Jenkins and click on View -->> Configuration/Install -->> Add to Slack
On Post to Channel: Click the Drop Down and select your channel above cicd-pipeline-project-alerts
Click Add Jenkins CI Integration
SAVE SETTINGS/CONFIGURATIONS
Leave this page open SlackConfig!
NOTE: Update Your Jenkins file with your Slack Channel Name
Go back to your local, open your "Jenkins-CICD-Project" repo/folder/directory on VSCODE
Open your "Jenkinsfile"
Update the slack channel name on line "97" (there about)
Change name from "cicd-project-alerts" (or whatever name thst's there) to yours
Add the changes to git, commit and push to GitHub
Confirm the changes are available on GitHub
Save and Push to GitHub
Configure All Systems
Configure Promitheus
Login/SSH to your Prometheus Server
Clone the following repository: https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
Change directory to "realworld-cicd-pipeline-project"
Swtitch to the "prometheus-and-grafana" git branch
Run: ./install-prometheus.sh
Confirm the status shows "Active (running)"
Exit
Configure Grafana
Login/SSH to your Grafana Server
Clone the following repository: https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
Change directory to "realworld-cicd-pipeline-project"
Swtitch to the "prometheus-and-grafana" git branch
Run: ls or ll (to confirm you have the branch files)
Run: ./install-grafana.sh
Confirm the status shows "Active (running)"
Exit
Configure The "Node Exporter" accross the "Dev", "Stage" and "Prod" instances including your "Pipeline Infra"
Login/SSH into the "Dev-Env", "Stage-Env" and "Prod-Env" VM instance
Perform the following operations on all of them
Install git by running: sudo yum install git -y
Clone the following repository: https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
Change directory to "realworld-cicd-pipeline-project"
Swtitch to the "prometheus-and-grafana" git branch
Run: ls or ll (to confirm you have the branch files)
Run: ./install-node-exporter.sh
Confirm the status shows "Active (running)"
Access the Node Exporters running on port "9100", open your browser and run the below
Dev-EnvPublicIPaddress:9100 (Confirm this page is accessible)
Stage-EnvPublicIPaddress:9100 (Confirm this page is accessible)
Prod-EnvPublicIPaddress:9100 (Confirm this page is accessible)
Exit
Configure The "Node Exporter" on the "Jenkins-Maven-Ansible", "Nexus" and "SonarQube" instances
Login/SSH into the "Jenkins-Maven-Ansible", "Nexus" and "SonarQube" VM instance
Perform the following operations on all of them
Install git by running: sudo yum install git -y (The SonarQube server already has git)
Clone the following repository: https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
Change directory to "realworld-cicd-pipeline-project"
Swtitch to the "prometheus-and-grafana" git branch
Run: ls or ll (to confirm you have the branch files including "install-node-exporter.sh")
Run: ./install-node-exporter.sh
Make sure the status shows "Active (running)"
Access the Node Exporters running on port "9100", open your browser and run the below
Jenkins-Maven-AnsiblePublicIPaddress:9100 (Confirm the pages are accessible)
NexusPublicIPaddress:9100
SonarQubePublicIPaddress:9100
Exit NodeExporter!
Update the Prometheus config file and include all the IP Addresses of the Pipeline Instances that are
running the Node Exporter API. That'll include ("Dev", "Stage", "Prod", "Jenkins-Maven-Ansible", "Nexus" and "SonarQube")SSH into the Prometheus instance either using your GitBash (Windows) or Terminal (macOS) or browser
Run the command: sudo vi /etc/prometheus/prometheus.yml
Navigate to "- targets: ['localhost:9090']" and add the "IPAddress:9100" for all the above Pipeline instances. Ecample "- targets: ['localhost:9090', 'DevIPAddress:9100', 'StageIPAddress:9100', 'ProdIPAddress:9100', 'Jenkins-Maven-AnsibleIPAddress:9100'] ETC..."
Save the Config File and Quit
Open a TAB on your choice browser
Copy the Prometheus PublicIP Addres and paste on the browser/tab with port 9100 e.g "PrometheusPublicIPAddres:9100"
Once you get to the Prometheus Dashboard Click on "Status" and Click on "Targets"
Confirm that Prometheus is able to reach everyone of your Nodes, do this by confirming the Status "UP" (green)
Done ConfigurePrometheus!
Open a New Tab on your browser for Grafana also if you've not done so already.
Copy your Grafana Instance Public IP and put on the browser with port 3000 e.g "GrafanaPublic:3000"
Once the UI Opens pass the following username and password
Username: admin
Password: admin
New Username: admin
New Password: admin
Save and Continue ConfigureGrafana!
Once you get into Grafana, follow the below steps to Import a Dashboard into Grafana to visualize your Infrastructure/App Metrics
Click on "Configuration/Settings" on your left
Click on "Data Sources"
Click on "Add Data Source"
Select Prometheus
Underneath HTTP URL: http://PrometheusPublicOrPrivateIPaddress:9090
Click on "SAVE and TEST"
Navigate to "Create" on your left (the + sign)
Click on "Import"
Copy the following link: https://grafana.com/grafana/dashboards/1860
Paste the above link where you have "Import Via Grafana.com"
Click on Load (The one right beside the link you just pasted)
Scrol down to "Prometheus" and select the "Data Source" you defined ealier which is "Prometheus"
CLICK on "Import"
Refresh your Grafana Dashbaord
Click on the "Drop Down" for "Host" and select any of the "Instances(IP)" GrafanaMetrics!
Setup Splunk Server and Configure Forwarders
A) SSH into your Splunk Server including Dev, Stage and Prod Instances to Configure Splunk
NOTE: Execute and Perform all operations across all your Dev, Stage and Prod EnvironmentsNOTE: Run all commands and queries across all your VMs (Dev, Stage and Prod)Download the Splunk RPM installer package for Linux
wget -O splunk-9.0.4.1-419ad9369127-linux-2.6-x86_64.rpm "https://download.splunk.com/products/splunk/releases/9.0.4.1/linux/splunk-9.0.4.1-419ad9369127-linux-2.6-x86_64.rpm"
Install Splunk
sudo yum install ./splunk-9.0.2-17e00c557dc1-linux-2.6-x86_64.rpm -y
Start the splunk server
sudo bash
cd /opt/splunk/bin
./splunk start --accept-license --answer-yes
Enter administrator username and password, remember this because you will need this to log into the applicationNOTE: The Password must be up to 8 characters. SplunkSetup1!Access your Splunk Installation at http://Splunk-Server-IP:8000 and log into splunkUsername: admin, Password: Same Password You Just Configured Above SplunkSetup2!
NOTE(MANDATORY): Once you login to the splunk IndexerClick on Settings -->> Click Server Settings -->> Click General Settings
Go ahead and Change the Pause indexing if free disk space from 5000 to 50
Click on Save SplunkSetup3!
Step 2: Install The Splunk Forwarder only on the Dev, Stage and Prod Servers
NOTE: Execute every command mentioned bellow across all application servers in all the enviroments
NOTE: Do Not install the Splunk Server in these resources/environments
SSH Into your instances, as normal user ec2-user or ubuntu or centos etc
exit
Download the Splunk forwarder RPM installer package
wget -O splunkforwarder-9.0.4-de405f4a7979-linux-2.6-x86_64.rpm "https://download.splunk.com/products/universalforwarder/releases/9.0.4/linux/splunkforwarder-9.0.4-de405f4a7979-linux-2.6-x86_64.rpm"
Install the Forwarder
ls -al
sudo yum install ./splunkforwarder-9.0.4-de405f4a7979-linux-2.6-x86_64.rpm -y
Change to the splunkforwarder bin directory and start the forwarder
NOTE: The Password must be at least 8 characters long.
Set the port for the forwarder to 9997, this is to keep splunk server from conflicting with the splunk forwarder
sudo bash
cd /opt/splunkforwarder/bin
./splunk start --accept-license --answer-yes
SplunkSetup2!Set the forwarder to forward to the splunk server on port 9997, and will need to enter username and password (change IP address with your own server IP address). When prompted for username and password, enter what you set above for username and password.
./splunk add forward-server SPLUNK-SERVER-Public-IP-Address:9997
Restart Splunk on the VM you are configuring the Forwarder
./splunk restart
Set the forwarder to monitor the /var/log/tomcat/ directory and restart
./splunk add monitor /var/log/tomcat/
Set the port for the splunk server to listen on 9997 and restart
cd /opt/splunk/bin
./splunk enable listen 9997
Step 3: View Application Logs in Splunk
Login to your Splunk Server at http://Splunk-Server-IP:8000Click on Search and Reporting -->> Data Summary -->> Select any of the displayed Environments Host to visualize App Logs SplunkSetup4!Application Log Indexed SplunkSetup3!Jenkins setup
Access Jenkins
Copy your Jenkins Public IP Address and paste on the browser = ExternalIP:8080Login to your Jenkins instance using your Shell (GitBash or your Mac Terminal)
Copy the Path from the Jenkins UI to get the Administrator Password
Run: sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Copy the password and login to Jenkins JenkinsSetup1!
Plugins: Choose Install Suggested Plugings
Provide
Username: admin
Password: admin
Name and Email can also be admin. You can use admin all, as its a poc.
Continue and Start using Jenkins JenkinsSetup2!
Plugin installations:
Click on "Manage Jenkins"
Click on "Plugin Manager"
Click "Available"
Search and Install the following Plugings "Install Without Restart"
SonarQube Scanner
Maven Integration
Pipeline Maven Integration
Maven Release Plug-In
Slack Notification
Nexus Artifact Uploader
Build Timestamp (Needed for Artifact versioning)
Once all plugins are installed, select Restart Jenkins when installation is complete and no jobs are running PluginInstallation!
Global tools configuration:
Click on Manage Jenkins -->> Global Tool Configuration JDKSetup!JDK -->> Add JDK -->> Make sure Install automatically is enabled -->>Note: By default the Install Oracle Java SE Development Kit from the website make sure to close that option by clicking on the image as shown below.JDKSetup!Click on Add installer
Select Extract .zip/.tar.gz -->> Fill the below values
Name: localJdk
Download URL for binary archive: https://download.java.net/java/GA/jdk11/13/GPL/openjdk-11.0.1_linux-x64_bin.tar.gz
Subdirectory of extracted archive: jdk-11.0.1
Git -->> Add Git -->> Install automatically(Optional) GitSetup!SonarQube Scanner -->> Add SonarQube Scanner -->> Install automatically(Optional) SonarQubeScanner!Maven -->> Add Maven -->> Make sure Install automatically is enabled -->> Install from Apache -->> Fill the below valuesName: localMaven
Version: Keep the default version as it is
Click on SAVE MavenSetup!Credentials setup(SonarQube, Nexus, Ansible and Slack):
Click on Manage Jenkins -->> Manage Credentials -->> Global credentials (unrestricted) -->> Add Credentials
SonarQube secret token (SonarQube-Token)
Generating SonarQube secret token:
Login to your SonarQube server (http://SonarServer-Sublic-IP:9000, with the credentials username: admin & password: admin)
Click on profile -->> My Account -->> Security -->> Tokens
Generate Tokens: Fill SonarQube-Token
Click on Generate
Copy the token
Store SonarQube Secret token in Jenkins:
Click on Add Credentials
Kind: Secret text!!
Secret: Fill the SonarQube token value that we have created on the SonarQube server
ID: SonarQube-Token
Description: SonarQube-Token
Click on Create
Slack secret token (slack-token)
Click on Add Credentials
Kind: Secret text
Secret: Place the Integration Token Credential ID (Note: Generate for slack setup)
ID: Slack-Token
Description: slack-token
Click on Create
Nexus Credentials (Username and Password)
Login to Nexus and Set Password
Access Nexus: http://Nexus-Pub-IP:8081/
Default Username: admin
NOTE: Login into your "Nexus" VM and "cat" the following file to get the password.
Command: sudo cat /opt/nexus/sonatype-work/nexus3/admin.password
Password: Fill In The Password and Click Sign In
Click Next -->> Provide New Password: "admin"
Configure Anonymous Access: "Enable anonymous access" -->> Finish
Nexus credentials (username & password)
Click on Add Credentials
Kind: Username with password
Username: admin
Enable Treat username as secret
Password: admin
ID: Nexus-Credential
Description: nexus-credential
Click on Create
Ansible deployment server credential (username & password)
Click on Add Credentials
Kind: Username with password
Username: ansibleadmin
Enable Treat username as secret
Password: ansibleadmin
ID: Ansible-Credential
Description: Ansible-Credential
Click on Create
SonarQubeServerSetup!
Configure system:
Click on Manage Jenkins -->> Configure System
SonarQube Servers SonarQubeServerSetup!
Click on Manage Jenkins -->> Configure System
Go to section Slack
Use new team subdomain & integration token credentials created in the above slack joining step
Workspace: Replace with Team Subdomain value (created above)
Credentials: select the slack-token credentials (created above)
Default channel / member id: #PROVIDE_YOUR_CHANNEL_NAME_HERE
Test Connection
Click on Save SlackSetup!
SonarQube Configuration
Setup SonarQube GateKeeper
Click on -->> Quality Gate SonarQubeSetup2!Click on -->> Create SonarQubeSetup2!Add a Quality Gate Condition to Validate the Code Against (Code Smells or Bugs) SonarQubeSetup3!Add Quality to SonarQube ProjectNOTE: Make sure to update the SonarQube stage in your Jenkinsfile and Test the Pipeline so your project will be visible on the SonarQube Project Dashboard.Click on Projects -->> Administration -->> Select Quality Gate SonarQubeSetup3!Setup SonarQube Webhook to Integrate Jenkins (To pass the results to Jenkins)
Still on AdministrationSelect WebhookClick on Create WebhookName: jenkinswebhook
URL: http://Jenkins-Server-Private-IP:8080/sonarqube-webhook SonarQubeSetup4!
Go ahead and Confirm in the Jenkinsfile you have the “Quality Gate Stage”. The stage code should look like the below;stage('SonarQube GateKeeper') {
    steps {
      timeout(time : 1, unit : 'HOURS'){
      waitForQualityGate abortPipeline: true
      }
   }
}
Run Your Pipeline To Test Your Quality Gate (It should PASS QG)
(OPTIONAL) FAIL Your Quality Gate: Go back to SonarQube -->> Open your Project -->> Click on Quality Gates at the top -->> Select your Project Quality Gate -->> Click EDIT -->> Change the Value to “0” -->> Update Condition
(OPTIONAL) Run/Test Your Pipeline Again and This Time Your Quality Gate Should Fail
(OPTIONAL) Go back and Update the Quality Gate value to 10. The Exercise was just to see how Quality Gate Works
Pipeline creation
Update The Jenkinsfile If NeccessaryUpdate SonarQube IP address in your JenkinsfileUpdate the SonarQube projectKey or name in your JenkinsfileUpdate your Slack Channel Name in the JenkinsfileLog into Jenkins: http://Jenkins-Public-IP:8080/
Click on New Item
Enter an item name: Jenkins-Complete-CICD-Pipeline & select the category as Pipeline
Now scroll-down and in the Pipeline section -->> Definition -->> Select Pipeline script from SCM
GitHub project: Provide Your Project Repo Git URL
GitHub hook trigger for GITScm polling: Check the box
NOTE: Make sure to also configure it on GitHub's side
SCM: Git
Repositories
Repository URL: FILL YOUR OWN REPO URL (that we created by importing in the first step)
Branch Specifier (blank for 'any'): */main
Script Path: Jenkinsfile
Save
NOTE: Make Sure Your Pipeline Succeeds Until SonarQube GateKeeper. Upload to Artifactory would fail.
TEST Pipeline
A. Pipeline Test Results
Jenkins Pipeline Job JenkinsJobResult!SonarQube Code Inspection Result SonarQubeResult!Slack Continuous Feedback Alert SlackResult!SonarQube GateKeeper Webhook Payload SonarQubeGateKeeper!B. Troubleshooting (Possible Issues You May Encounter and Suggested Solutions)
1st ISSUE: If you experience a long wait time at the level of GateKeeper, please check if your Sonar Webhook is associated with your SonarQube Project with SonarQube Results
If you check your jenkins Pipeline you'll most likely find the below message at the SonarQube GateKeper stage
JENKINS CONSOLE OUTPUTChecking status of SonarQube task 'AYfEB4IQ3rP3Y6VQ_yIa' on server 'SonarQube'
SonarQube task 'AYfEB4IQ3rP3Y6VQ_yIa' status is 'PENDING'
Nexus Configuration
Accessing Nexus:
The nexus service on port 8081. To access the nexus dashboard, visit http://Nexus-Pub-IP:8081. You will be able to see the nexus homepage as shown below.Default username: admin
Default Password: sudo cat /app/sonatype-work/nexus3/admin.password
NOTE: Once you login, you will be prompted to reset the password
Go ahead and create your Nexus Project Repositories
CREATE 1st REPO: Click on the Gear Icon -->> Repository -->> Create Repository -->> Select maven2(hosted) -->> Name: maven-project-releases -->> Create RepositoryCREATE 2nd REPO: Click Create Repository -->> Select maven2(hosted) -->> Name: maven-project-snapshots -->> Version Policy: Select Snapshot -->> Create RepositoryCREATE 3rd REPO: Click Create Repository -->> Select maven2(proxy) -->> Name: maven-project-central -->> Remote Storage: provide this link https://repo.maven.apache.org/maven2 -->> Create RepositoryCREATE 4th REPO: Click Create Repository -->> Select maven2(group) -->> Name: maven-project-group -->> Version Policy: Select Mixed -->> Assign All The Repos You Created to The Group -->> Create RepositoryOnce you select create repository and select maven2(group)NexusSetup!Update Maven POM and Integrate/Configure Nexus With Jenkins
A) Update Maven POM.xml fileUpdate the Following lines of Code (Line 32 and 36) in the maven POM file and save
<url>http://Nexus-Server-Private-IP:8081/repository/maven-project-snapshots/</url><url>http://Nexus-Server-Private-IP:8081/repository/maven-project-releases/</url>
Add the following Stage in your Jenkins pipeline config and Update the following Values (nexusUrl, repository, credentialsId, artifactId, file etc.). If necessaryThe following environment config represents the NEXUS CREDENTIAL stored in jenkins. we're pulling the credential with the use of the predefine NEXUS_CREDENTIAL_ID environment variable key. Which jenkins already understands.environment {
  WORKSPACE = "${env.WORKSPACE}"
  NEXUS_CREDENTIAL_ID = 'Nexus-Credential'
}
Here we're using the Nexus Artifact Uploader stage config to store the app artifactstage("Nexus Artifact Uploader"){
    steps{
        nexusArtifactUploader(
          nexusVersion: 'nexus3',
          protocol: 'http',
          nexusUrl: '172.31.82.36:8081',
          groupId: 'webapp',
          version: "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}",
          repository: 'maven-project-releases',  //"${NEXUS_REPOSITORY}",
          credentialsId: "${NEXUS_CREDENTIAL_ID}",
          artifacts: [
              [artifactId: 'webapp',
              classifier: '',
              file: '/var/lib/jenkins/workspace/jenkins-complete-cicd-pipeline/webapp/target/webapp.war',
              type: 'war']
          ]
        )
    }
}
After confirming all changes, go ahead and save, then push to GitHub.Test your Pipeline to Make Sure That The Artifacts Upload Stage Succeeds.Navigate to Jenkins Dashboard (Run/Test The Job) PipelineStagesArtifactSuccess!Navigate to Nexus as well to confirm that the artifact was Stored in the maven-project-releases repository ArtifactStored!Configure Ansible To Deploy to Dev, Stage and Prod
NOTE: Make sure you Assign an IAM ROLE / PROFILE with EC2 Full Access to your JENKINS server
NOTE: Update ALL Pipeline Deploy Stages with your Ansible Credentials ID (IMPORTANT)
Also Make sure the following Userdata was executed across all the Environment Deployment Nodes/Areas
#!/bin/bash
# Tomcat Server Installation
sudo su
amazon-linux-extras install tomcat8.5 -y
systemctl enable tomcat
systemctl start tomcat# Provisioning Ansible Deployer Access
useradd ansibleadmin
echo ansibleadmin | passwd ansibleadmin --stdin
sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
systemctl restart sshd
echo "ansibleadmin ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
TEST PIPELINE DEPLOYMENT
Confirm/Confirm that your deployments where all successful accross all Environments PipelineStagesCompleted!Verify/Confirm Slack Success Feedback. SlackSuccessAllStages!Confirm Access to your application: http://Dev-or-Stage-or-Prod-PubIP:8080/webapp/ FinalProductDisplay!NOTE: That By completing this project, you are now considered a Professional DevOps Engineer.
You've been able to accomplish something very unique and special which most people only dream of in their IT journey. Remmber that during an interview, you may be asked some challenging questions or be faced with a trial assignment that require you to both utilize your existing skillsets and think out of the box. During this time you must be very confident and determined in your pursuit.Never forget that you have what it takes to add more than enough VALUE to any organization out there in the industry and to STAND OUT in any interview setting no matter who is sitted on the interview seat.Congratulations Team!!!👨🏼‍💻 Congratulations!!!👨🏼‍💻


Explain how i can achieve the above project 

Step by stepShow moreComplete End-to-End Jenkins CI/CD Pipeline Implementation Guide

I'll break down this comprehensive DevOps project into manageable steps. This project implements a production-grade CI/CD pipeline for a Java web application.
Phase 1: Initial Setup & Prerequisites
Step 1: AWS Account Preparation

Log into your AWS Console
Select a region (recommend US-East-1 or US-West-2)
Create an IAM user with EC2 full access if you haven't already
Generate and download SSH key pair (.pem file) for EC2 access

Step 2: GitHub Repository Setup

Go to GitHub and log in to your account
Navigate to the source repository: https://github.com/awanmbandi/realworld-cicd-pipeline-project
Click Fork to create your own copy
Verify the code is in your repository
Note your repository URL (you'll need this later)


Phase 2: Infrastructure Provisioning (8 EC2 Instances)
Step 3: Launch Jenkins-Maven-Ansible Server
Instance Configuration:

AMI: Amazon Linux 2
Instance Type: t2.medium
Security Group: Create new or use existing

Port 22 (SSH) - Source: 0.0.0.0/0
Port 8080 (Jenkins) - Source: 0.0.0.0/0
Port 9100 (Node Exporter) - Source: 0.0.0.0/0


Key Pair: Select your key pair
User Data: Copy and paste from:

  https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/maven-nexus-sonarqube-jenkins-install/jenkins-install.sh

Tag: Name = jenkins-maven-ansible
Click Launch Instance

Step 4: Launch SonarQube Server
Instance Configuration:

AMI: Ubuntu 20.04
Instance Type: t2.medium
Security Group:

Port 22 (SSH) - Source: 0.0.0.0/0
Port 9000 (SonarQube) - Source: 0.0.0.0/0
Port 9100 (Node Exporter) - Source: 0.0.0.0/0


Key Pair: Select your key pair
User Data: Copy from:

  https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/maven-nexus-sonarqube-jenkins-install/sonarqube-install.sh

Tag: Name = SonarQube
Click Launch Instance

Step 5: Launch Nexus Repository Server
Instance Configuration:

AMI: Amazon Linux 2
Instance Type: t2.medium
Security Group:

Port 22 (SSH) - Source: 0.0.0.0/0
Port 8081 (Nexus) - Source: 0.0.0.0/0
Port 9100 (Node Exporter) - Source: 0.0.0.0/0


Key Pair: Select your key pair
User Data: Copy from:

  https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/maven-nexus-sonarqube-jenkins-install/nexus-install.sh

Tag: Name = Nexus
Click Launch Instance

Step 6: Launch Application Environment Servers (3 Instances)
Create THREE identical instances with these specs:
Instance Configuration (for each):

AMI: Amazon Linux 2
Instance Type: t2.micro
Security Group:

Port 22 (SSH) - Source: 0.0.0.0/0
Port 8080 (Tomcat) - Source: 0.0.0.0/0
Port 9100 (Node Exporter) - Source: 0.0.0.0/0
Port 9997 (Splunk Forwarder) - Source: 0.0.0.0/0


Key Pair: Select your key pair
User Data: Copy from:

  https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/tomcat-splunk-installation/tomcat-ssh-configure.sh

Tags:

Instance 1: Name = Dev-Env
Instance 2: Name = Stage-Env
Instance 3: Name = Prod-Env



Step 7: Launch Prometheus Server
Instance Configuration:

AMI: Ubuntu 20.04
Instance Type: t2.micro
Security Group:

Port 22 (SSH) - Source: 0.0.0.0/0
Port 9090 (Prometheus) - Source: 0.0.0.0/0


Key Pair: Select your key pair
Tag: Name = Prometheus
Click Launch Instance (no user data needed)

Step 8: Launch Grafana Server
Instance Configuration:

AMI: Ubuntu 20.04
Instance Type: t2.micro
Security Group:

Port 22 (SSH) - Source: 0.0.0.0/0
Port 3000 (Grafana) - Source: 0.0.0.0/0


Key Pair: Select your key pair
Tag: Name = Grafana
Click Launch Instance (no user data needed)

Step 9: Launch Splunk Server
Instance Configuration:

AMI: Amazon Linux 2
Instance Type: t2.micro
Security Group:

Port 22 (SSH) - Source: 0.0.0.0/0
Port 8000 (Splunk Web) - Source: 0.0.0.0/0
Port 9997 (Splunk Receiver) - Source: 0.0.0.0/0
Port 9100 (Node Exporter) - Source: 0.0.0.0/0


Key Pair: Select your key pair
Tag: Name = Splunk-Server
Click Launch Instance

Step 10: Verify All Instances

Go to EC2 Dashboard
Verify you have 8 running instances
Note down all Public and Private IP addresses (you'll need these throughout)


Phase 3: Monitoring Setup (Prometheus & Grafana)
Step 11: Configure Prometheus

SSH into Prometheus server:

bash   ssh -i your-key.pem ubuntu@<Prometheus-Public-IP>

Clone the repository:

bash   git clone https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
   cd realworld-cicd-pipeline-project

Switch to monitoring branch:

bash   git checkout prometheus-and-grafana
   ls -l  # Verify install-prometheus.sh exists

Install Prometheus:

bash   chmod +x install-prometheus.sh
   ./install-prometheus.sh

Verify installation:

bash   sudo systemctl status prometheus
   # Should show "active (running)"

Access Prometheus UI:

Open browser: http://<Prometheus-Public-IP>:9090
You should see the Prometheus dashboard



Step 12: Configure Grafana

SSH into Grafana server:

bash   ssh -i your-key.pem ubuntu@<Grafana-Public-IP>

Clone and setup:

bash   git clone https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
   cd realworld-cicd-pipeline-project
   git checkout prometheus-and-grafana

Install Grafana:

bash   chmod +x install-grafana.sh
   ./install-grafana.sh

Verify installation:

bash   sudo systemctl status grafana-server
   # Should show "active (running)"

Access Grafana UI:

Open browser: http://<Grafana-Public-IP>:3000
Default login:

Username: admin
Password: admin


Set new password: admin (or your choice)



Step 13: Install Node Exporter on Application Servers
Perform these steps on Dev-Env, Stage-Env, and Prod-Env:

SSH into each server:

bash   ssh -i your-key.pem ec2-user@<Server-Public-IP>

Install Git and clone repo:

bash   sudo yum install git -y
   git clone https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
   cd realworld-cicd-pipeline-project
   git checkout prometheus-and-grafana

Install Node Exporter:

bash   chmod +x install-node-exporter.sh
   ./install-node-exporter.sh

Verify:

bash   sudo systemctl status node_exporter
   # Should show "active (running)"

Test in browser:

http://<Server-Public-IP>:9100/metrics
You should see metrics data


Repeat for all three servers (Dev, Stage, Prod)

Step 14: Install Node Exporter on Pipeline Infrastructure
Perform on Jenkins-Maven-Ansible, Nexus, and SonarQube servers:

SSH into each server
For Amazon Linux 2 (Jenkins, Nexus):

bash   sudo yum install git -y
   git clone https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
   cd realworld-cicd-pipeline-project
   git checkout prometheus-and-grafana
   chmod +x install-node-exporter.sh
   ./install-node-exporter.sh
   sudo systemctl status node_exporter

For Ubuntu (SonarQube):

bash   # Git should already be installed
   git clone https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
   cd realworld-cicd-pipeline-project
   git checkout prometheus-and-grafana
   chmod +x install-node-exporter.sh
   ./install-node-exporter.sh
   sudo systemctl status node_exporter

Verify each in browser:

http://<Each-Server-Public-IP>:9100/metrics



Step 15: Configure Prometheus Targets

SSH into Prometheus server:

bash   ssh -i your-key.pem ubuntu@<Prometheus-Public-IP>

Edit Prometheus config:

bash   sudo vi /etc/prometheus/prometheus.yml

Find the scrape_configs section and update targets:

yaml   scrape_configs:
     - job_name: 'prometheus'
       static_configs:
         - targets: ['localhost:9090']
     
     - job_name: 'node_exporters'
       static_configs:
         - targets: 
           - '<Dev-Env-Private-IP>:9100'
           - '<Stage-Env-Private-IP>:9100'
           - '<Prod-Env-Private-IP>:9100'
           - '<Jenkins-Private-IP>:9100'
           - '<Nexus-Private-IP>:9100'
           - '<SonarQube-Private-IP>:9100'

Save and exit (:wq in vi)
Restart Prometheus:

bash   sudo systemctl restart prometheus
   sudo systemctl status prometheus

Verify targets:

Go to http://<Prometheus-Public-IP>:9090
Click Status → Targets
All targets should show UP (in green)



Step 16: Configure Grafana Dashboard

Access Grafana: http://<Grafana-Public-IP>:3000
Add Prometheus as Data Source:

Click Configuration (gear icon) → Data Sources
Click Add data source
Select Prometheus
URL: http://<Prometheus-Private-IP>:9090
Click Save & Test (should show "Data source is working")


Import Dashboard:

Click + (Create) → Import
Dashboard ID: 1860
Click Load
Select Prometheus data source
Click Import


View Metrics:

Select different hosts from dropdown
Verify you see CPU, memory, disk metrics




Phase 4: Log Management (Splunk Setup)
Step 17: Install Splunk Server

SSH into Splunk server:

bash   ssh -i your-key.pem ec2-user@<Splunk-Public-IP>

Download Splunk:

bash   wget -O splunk-9.0.4.1-419ad9369127-linux-2.6-x86_64.rpm \
   "https://download.splunk.com/products/splunk/releases/9.0.4.1/linux/splunk-9.0.4.1-419ad9369127-linux-2.6-x86_64.rpm"

Install Splunk:

bash   sudo yum install ./splunk-9.0.4.1-419ad9369127-linux-2.6-x86_64.rpm -y

Start Splunk:

bash   sudo bash
   cd /opt/splunk/bin
   ./splunk start --accept-license --answer-yes

Create admin credentials:

Username: admin
Password: Choose a password (min 8 characters, e.g., Admin@123)


Configure disk space settings:

Access: http://<Splunk-Public-IP>:8000
Login with admin credentials
Go to Settings → Server Settings → General Settings
Change "Pause indexing if free disk space" from 5000 to 50
Click Save


Enable listening port:

bash   cd /opt/splunk/bin
   ./splunk enable listen 9997
   ./splunk restart
Step 18: Install Splunk Forwarder on Application Servers
Perform on Dev-Env, Stage-Env, and Prod-Env:

SSH into each server:

bash   ssh -i your-key.pem ec2-user@<Server-Public-IP>

Download Splunk Forwarder:

bash   wget -O splunkforwarder-9.0.4-de405f4a7979-linux-2.6-x86_64.rpm \
   "https://download.splunk.com/products/universalforwarder/releases/9.0.4/linux/splunkforwarder-9.0.4-de405f4a7979-linux-2.6-x86_64.rpm"

Install Forwarder:

bash   sudo yum install ./splunkforwarder-9.0.4-de405f4a7979-linux-2.6-x86_64.rpm -y

Start and configure:

bash   sudo bash
   cd /opt/splunkforwarder/bin
   ./splunk start --accept-license --answer-yes

Set credentials (same as Splunk server):

Username: admin
Password: Same password as Splunk server


Configure forward server:

bash   ./splunk add forward-server <Splunk-Server-Public-IP>:9997

Enter username: admin
Enter password: your password


Add monitoring directory:

bash   ./splunk add monitor /var/log/tomcat/
   ./splunk restart

Repeat for all three application servers

Step 19: Verify Splunk Setup

Access Splunk: http://<Splunk-Public-IP>:8000
Click Search & Reporting
Click Data Summary
Verify you see hosts (Dev-Env, Stage-Env, Prod-Env)
Click on a host to see logs


Phase 5: Slack Integration for Notifications
Step 20: Join Slack Workspace

Join the workspace:

Click this link: https://join.slack.com/t/realworldcicdproject/shared_invite/zt-1tryd7x1v-g8a~zEJBKKchVvvK87jkeQ
Sign up or log in to Slack


Create your private channel:

Click + next to Channels
Select Create a channel
Name: yourname-jenkins-cicd-alerts (e.g., john-jenkins-cicd-alerts)
Make it Private
Click Create



Step 21: Configure Jenkins App for Slack

In your Slack channel:

Click channel name → Integrations → Add apps
Search for Jenkins CI
Click Add to Slack


Configure Jenkins integration:

Post to Channel: Select your channel (yourname-jenkins-cicd-alerts)
Click Add Jenkins CI Integration


Save these details:

Team Subdomain: (e.g., realworldcicdproject)
Integration Token Credential ID: Copy this token (starts with something like T0xxxxx/B0xxxxx/xxxxxxxxx)
Keep this page open for later



Step 22: Update Your Jenkinsfile

On your local machine, open your forked repository
Open Jenkinsfile in VS Code or any editor
Find line ~97 (in the post section):

groovy   slackSend channel: '#cicd-project-alerts',

Update with YOUR channel name:

groovy   slackSend channel: '#yourname-jenkins-cicd-alerts',

Save, commit, and push to GitHub:

bash   git add Jenkinsfile
   git commit -m "Updated Slack channel name"
   git push origin main

Phase 6: Jenkins Configuration
Step 23: Initial Jenkins Access

Access Jenkins:

Open browser: http://<Jenkins-Public-IP>:8080


Get admin password:

bash   ssh -i your-key.pem ec2-user@<Jenkins-Public-IP>
   sudo cat /var/lib/jenkins/secrets/initialAdminPassword

Copy password and paste in Jenkins
Install suggested plugins (click the option)
Create admin user:

Username: admin
Password: admin
Full name: Admin
Email: admin@admin.com


Click "Save and Continue" → "Start using Jenkins"

Step 24: Install Required Jenkins Plugins

Go to: Manage Jenkins → Manage Plugins
Click "Available" tab
Search and install these plugins (check boxes):

SonarQube Scanner
Maven Integration
Pipeline Maven Integration
Maven Release Plug-In
Slack Notification
Nexus Artifact Uploader
Build Timestamp


Click "Install without restart"
Check "Restart Jenkins when no jobs are running"
Wait for Jenkins to restart (refresh page after 1-2 minutes)

Step 25: Configure Global Tools

Go to: Manage Jenkins → Global Tool Configuration
Configure JDK:

Click Add JDK
Name: localJdk
Uncheck "Install automatically"
JAVA_HOME: /usr/lib/jvm/java-11-openjdk

OR if using automatic installation:

Check "Install automatically"
Click Add Installer → Extract .zip/.tar.gz
Label: Leave empty
Download URL: https://download.java.net/java/GA/jdk11/13/GPL/openjdk-11.0.1_linux-x64_bin.tar.gz
Subdirectory: jdk-11.0.1


Configure Git:

Git installations → Add Git
Name: Default
Check "Install automatically" (or provide path: /usr/bin/git)


Configure Maven:

Click Add Maven
Name: localMaven
Check "Install automatically"
Version: Keep default (latest)


Configure SonarQube Scanner:

Click Add SonarQube Scanner
Name: SonarQube-Scanner
Check "Install automatically"
Version: Keep default


Click "Save"

Step 26: Configure Jenkins Credentials
Go to: Manage Jenkins → Manage Credentials → (global) → Add Credentials
A) SonarQube Token

First, generate token in SonarQube:

Access: http://<SonarQube-Public-IP>:9000
Login: Username: admin, Password: admin
Click profile icon → My Account → Security → Generate Tokens
Name: Jenkins-Token
Click Generate
Copy the token (you won't see it again!)


Add to Jenkins:

Kind: Secret text
Secret: Paste the SonarQube token
ID: SonarQube-Token
Description: SonarQube-Token
Click Create



B) Slack Token

Kind: Secret text
Secret: Paste your Slack Integration Token
ID: Slack-Token
Description: Slack-Token
Click Create

C) Nexus Credentials

First, get Nexus password:

bash   ssh -i your-key.pem ec2-user@<Nexus-Public-IP>
   sudo cat /opt/nexus/sonatype-work/nexus3/admin.password

Login to Nexus and set password:

Access: http://<Nexus-Public-IP>:8081
Username: admin
Password: Use the password from above
Click Sign In
Set new password: admin
Enable anonymous access
Click Finish


Add to Jenkins:

Kind: Username with password
Username: admin
Password: admin
ID: Nexus-Credential
Description: Nexus-Credential
Click Create



D) Ansible Credentials

Kind: Username with password
Username: ansibleadmin
Password: ansibleadmin
ID: Ansible-Credential
Description: Ansible-Credential
Click Create

Step 27: Configure SonarQube Server in Jenkins

Go to: Manage Jenkins → Configure System
Scroll to "SonarQube servers" section:

Check "Environment variables"
Click Add SonarQube
Name: SonarQube
Server URL: http://<SonarQube-Private-IP>:9000
Server authentication token: Select SonarQube-Token


Click "Save"

Step 28: Configure Slack in Jenkins

Still in Configure System, scroll to "Slack":

Workspace: realworldcicdproject (or your team subdomain)
Credential: Select Slack-Token
Default channel: #yourname-jenkins-cicd-alerts
Click Test Connection (should show "Success")


Click "Save"


Phase 7: SonarQube Configuration
Step 29: Configure Quality Gate in SonarQube

Access SonarQube: http://<SonarQube-Public-IP>:9000
Create Quality Gate:

Click Quality Gates → Create
Name: Jenkins-Quality-Gate
Click Save


Add Condition:

Click Add Condition
On: Overall Code
Quality Gate fails when: Bugs
Operator: is greater than
Value: 10
Click Add Condition


Add another condition (optional):

On: Overall Code
Quality Gate fails when: Code Smells
Operator: is greater than
Value: 10



Step 30: Configure SonarQube Webhook

In SonarQube, go to:

Administration (top menu) → Configuration → Webhooks


Create webhook:

Click Create
Name: Jenkins-Webhook
URL: http://<Jenkins-Private-IP>:8080/sonarqube-webhook/
Click Create




Phase 8: Nexus Repository Configuration
Step 31: Create Maven Repositories in Nexus

Access Nexus: http://<Nexus-Public-IP>:8081
Login: admin / admin
Create Repository #1 - Releases:

Click ⚙️ (Settings) → Repositories → Create repository
Select maven2 (hosted)
Name: maven-project-releases
Version policy: Release
Click Create repository


Create Repository #2 - Snapshots:

Click Create repository → maven2 (hosted)
Name: maven-project-snapshots
Version policy: Snapshot
Click Create repository


Create Repository #3 - Proxy:

Click Create repository → maven2 (proxy)
Name: maven-project-central
Remote storage: https://repo.maven.apache.org/maven2
Click Create repository


Create Repository #4 - Group:

Click Create repository → maven2 (group)
Name: maven-project-group
Version policy: Mixed
Member repositories: Move all three repos above to Members
Click Create repository



Step 32: Update Application Configuration Files

On your local machine, open your repository
Edit pom.xml (find the distributionManagement section around line 30):

xml   <distributionManagement>
       <repository>
           <id>maven-project-releases</id>
           <url>http://<Nexus-Private-IP>:8081/repository/maven-project-releases/</url>
       </repository>
       <snapshotRepository>
           <id>maven-project-snapshots</id>
           <url>http://<Nexus-Private-IP>:8081/repository/maven-project-snapshots/</url>
       </snapshotRepository>
   </distributionManagement>

Edit Jenkinsfile - Update the following sections:
Find the Nexus Artifact Uploader stage (around line 70):

groovy   stage("Nexus Artifact Uploader"){
       steps{
           nexusArtifactUploader(
             nexusVersion: 'nexus3',
             protocol: 'http',
             nexusUrl: '<Nexus-Private-IP>:8081',
             groupId: 'webapp',
             version: "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}",
             repository: 'maven-project-releases',
             credentialsId: 'Nexus-Credential',
             artifacts: [
                 [artifactId: 'webapp',
                 classifier: '',
                 file: '/var/lib/jenkins/workspace/jenkins-complete-cicd-pipeline/webapp/target/webapp.war',
                 type: 'war']
             ]
           )
       }
   }
Update SonarQube stage (around line 50):
groovy   environment {
       scannerHome = tool 'SonarQube-Scanner'
   }
   steps {
       withSonarQubeEnv('SonarQube') {
           sh """${scannerHome}/bin/sonar-scanner \
           -Dsonar.projectKey=maven-project \
           -Dsonar.projectName=maven-project \
           -Dsonar.projectVersion=1.0 \
           -Dsonar.sources=src/ \
           -Dsonar.java.binaries=target/classes/ \
           -Dsonar.junit.reportsPath=target/surefire-reports/ \
           -Dsonar.jacoco.reportsPath=target/jacoco.exec \
           -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml"""
       }
   }

Update deployment stages with your Private IPs:

Find Deploy to Dev (around line 90)
Find Deploy to Stage (around line 100)
Find Deploy to Prod (around line 110)

Update each with correct private IP:

groovy   sshagent(['Ansible-Credential']) {
       sh "scp -o StrictHostKeyChecking=no webapp/target/webapp.war ansibleadmin@<Dev-Private-IP>:/opt/apache-tomcat-8.5.82/webapps"
   }

Commit and push changes:

bash   git add .
   git commit -m "Updated configuration with server IPs"
   git push origin main

Phase 9: Ansible Configuration
Step 33: Prepare Ansible on Jenkins Server

SSH into Jenkins server:

bash   ssh -i your-key.pem ec2-user@<Jenkins-Public-IP>

Switch to Jenkins user:

bash   sudo su - jenkins

Generate SSH key:

bash   ssh-keygen -t rsa
   # Press Enter for all prompts (no passphrase)

View public key:

bash   cat ~/.ssh/id_rsa.pub
   # Copy this entire key
Step 34: Configure SSH Access to App Servers
Perform on Dev-Env, Stage-Env, and Prod-Env:

SSH into each server:

bash   ssh -i your-key.pem ec2-user@<Server-Public-IP>

Switch to ansibleadmin:

bash   sudo su - ansibleadmin

Add Jenkins public key:

bash   mkdir -p ~/.ssh
   vi ~/.ssh/authorized_keys
   # Paste the Jenkins public key
   # Save and exit (:wq)

Set permissions:

bash   chmod 700 ~/.ssh
   chmod 600 ~/.ssh/authorized_keys

Test from Jenkins server:

bash   # On Jenkins server (as jenkins user)RetryEContinuebash   # On Jenkins server (as jenkins user)
   ssh ansibleadmin@<Dev-Private-IP>
   # Should connect without password
   exit
   
   ssh ansibleadmin@<Stage-Private-IP>
   exit
   
   ssh ansibleadmin@<Prod-Private-IP>
   exit

Verify Tomcat is running on each server:

bash   sudo systemctl status tomcat
   # Should show "active (running)"

Phase 10: Create and Configure Jenkins Pipeline
Step 35: Create Jenkins Pipeline Job

In Jenkins, click "New Item"
Configure job:

Enter name: jenkins-complete-cicd-pipeline
Select: Pipeline
Click OK


Configure Pipeline:
General Section:

Description: Complete CI/CD Pipeline for Java Web Application
Check ✅ GitHub project
Project url: https://github.com/YOUR-USERNAME/Jenkins-CICD-Project/

Build Triggers:

Check ✅ GitHub hook trigger for GITScm polling

Pipeline Section:

Definition: Pipeline script from SCM
SCM: Git
Repository URL: https://github.com/YOUR-USERNAME/Jenkins-CICD-Project.git
Credentials: Leave as - none - (public repo)
Branch Specifier: */main
Script Path: Jenkinsfile


Click "Save"

Step 36: Configure GitHub Webhook

Go to your GitHub repository
Navigate to: Settings → Webhooks → Add webhook
Configure webhook:

Payload URL: http://<Jenkins-Public-IP>:8080/github-webhook/
Content type: application/json
Which events: Just the push event
Check ✅ Active
Click Add webhook


Verify: Green checkmark should appear after a few seconds


Phase 11: First Pipeline Run & Testing
Step 37: Initial Pipeline Execution

In Jenkins, open your pipeline
Click "Build Now"
Monitor the build:

Click on the build number (e.g., #1)
Click Console Output
Watch the logs


Expected Results (First Run):

✅ Git Checkout - SUCCESS
✅ Build - SUCCESS
✅ Unit Tests - SUCCESS
✅ Checkstyle Analysis - SUCCESS
✅ SonarQube Analysis - SUCCESS
⏳ SonarQube GateKeeper - May WAIT or TIMEOUT initially
❌ Nexus Artifact Upload - May FAIL (we'll fix this)



Step 38: Verify SonarQube Quality Gate

Check SonarQube Dashboard:

Open: http://<SonarQube-Public-IP>:9000
Click Projects
You should see maven-project
Click on it to see analysis results


Assign Quality Gate to Project:

In SonarQube, open your project
Click Project Settings → Quality Gate
Select: Jenkins-Quality-Gate
Click Save


Verify Webhook:

Go to Project Settings → Webhooks
Verify webhook exists
If not, create:

Name: Jenkins
URL: http://<Jenkins-Private-IP>:8080/sonarqube-webhook/




Run pipeline again - Quality Gate should now PASS

Step 39: Fix Nexus Upload Issues (if any)

Verify Nexus is accessible:

bash   curl http://<Nexus-Private-IP>:8081
   # Should return HTML

Check Jenkinsfile has correct Nexus IP
Verify Nexus credential in Jenkins:

Manage Jenkins → Manage Credentials
Verify Nexus-Credential exists with correct username/password


Run pipeline again - Nexus upload should succeed
Verify artifact in Nexus:

Open: http://<Nexus-Public-IP>:8081
Browse → maven-project-releases
You should see your webapp artifact




Phase 12: Testing Deployments
Step 40: Verify Dev Environment Deployment

Pipeline should complete successfully
Check deployment:

SSH into Dev-Env



bash   ssh -i your-key.pem ec2-user@<Dev-Public-IP>
   ls -l /opt/apache-tomcat-8.5.82/webapps/
   # Should see webapp.war

Access application:

Browser: http://<Dev-Public-IP>:8080/webapp/
Should see your Java web application


Check Tomcat logs:

bash   sudo tail -f /var/log/tomcat/catalina.out
   # Should show successful deployment
Step 41: Deploy to Stage Environment

In Jenkins Pipeline, the Stage deployment should run automatically after Dev
Verify Stage deployment:

bash   ssh -i your-key.pem ec2-user@<Stage-Public-IP>
   ls -l /opt/apache-tomcat-8.5.82/webapps/webapp.war

Access Stage application:

Browser: http://<Stage-Public-IP>:8080/webapp/



Step 42: Manual Approval for Production

Pipeline will PAUSE at "Deploy to Production" stage
In Jenkins:

You'll see a prompt: "Deploy to Production?"
Click Proceed to deploy
Or click Abort to stop


After approval, verify Prod deployment:

bash   ssh -i your-key.pem ec2-user@<Prod-Public-IP>
   ls -l /opt/apache-tomcat-8.5.82/webapps/webapp.war

Access Production application:

Browser: http://<Prod-Public-IP>:8080/webapp/




Phase 13: Verify Monitoring & Logging
Step 43: Check Prometheus Metrics

Access Prometheus: http://<Prometheus-Public-IP>:9090
Verify targets:

Status → Targets
All should be UP


Run some queries:

promql   # CPU usage
   100 - (avg by (instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)
   
   # Memory usage
   (node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes) / node_memory_MemTotal_bytes * 100
Step 44: Check Grafana Dashboards

Access Grafana: http://<Grafana-Public-IP>:3000
View imported dashboard:

Click Dashboards → Browse
Select the Node Exporter dashboard
Select different hosts from dropdown
Verify metrics are displaying


Customize dashboard (optional):

Click ⚙️ → Settings
Adjust time ranges
Add panels
Click Save dashboard



Step 45: Check Splunk Logs

Access Splunk: http://<Splunk-Public-IP>:8000
Search for logs:

Click Search & Reporting
Search: index=* source="/var/log/tomcat/*"
Set time range: Last 15 minutes
Click Search


View logs by host:

Click Data Summary
Click Hosts
Select Dev-Env, Stage-Env, or Prod-Env
View application logs


Create a simple dashboard (optional):

Save your search
Click Save As → Dashboard Panel
Choose visualization type
Click Save



Step 46: Verify Slack Notifications

Check your Slack channel: #yourname-jenkins-cicd-alerts
You should see notifications for:

Pipeline started
Each stage completion
Build success/failure
Deployment notifications


Message format should include:

Job name
Build number
Stage name
Status (Success/Failed)
Link to Jenkins build




Phase 14: Testing the Complete CI/CD Flow
Step 47: Trigger Automated Build

Make a code change:

bash   # On your local machine
   cd Jenkins-CICD-Project
   
   # Edit a file (e.g., README.md)
   echo "Testing CI/CD Pipeline" >> README.md
   
   # Commit and push
   git add .
   git commit -m "Testing automated pipeline trigger"
   git push origin main

Watch Jenkins:

Pipeline should automatically start within 1 minute
Triggered by GitHub webhook


Verify complete flow:

All stages execute automatically
Dev deployment happens automatically
Stage deployment happens automatically
Prod deployment waits for approval
Slack notifications at each stage



Step 48: Test Quality Gate Failure

Temporarily modify Quality Gate:

In SonarQube: Quality Gates → Jenkins-Quality-Gate
Edit condition: Bugs > 0 (set to 0)
Save


Trigger pipeline:

Make another code change and push
Pipeline should FAIL at Quality Gate stage


Verify failure handling:

Pipeline stops at Quality Gate
Slack notification shows failure
No deployment happens
Console output shows quality gate failure reason


Restore Quality Gate:

Change back to Bugs > 10
Save



Step 49: Test Slack Notifications

Verify you received Slack messages for:

✅ Pipeline Started
✅ Build Stage Success
✅ Unit Test Success
✅ Code Analysis Success
✅ SonarQube Scan Success
✅ Quality Gate Pass/Fail
✅ Nexus Upload Success
✅ Dev Deployment Success
✅ Stage Deployment Success
✅ Prod Deployment Success/Pending
✅ Pipeline Complete


Test failure notifications:

Create a syntax error in code
Push to trigger build
Should receive failure notification




Phase 15: Advanced Configuration & Optimization
Step 50: Configure Build Retention

In Jenkins Pipeline → Configure:

General section
Check ✅ Discard old builds
Strategy: Log Rotation
Days to keep builds: 7
Max # of builds to keep: 10
Click Save



Step 51: Add Pipeline Parameters

Edit Jenkinsfile - Add at the top:

groovy   pipeline {
       agent any
       
       parameters {
           choice(name: 'ENVIRONMENT', choices: ['Dev', 'Stage', 'Prod'], description: 'Select deployment environment')
           booleanParam(name: 'SKIP_TESTS', defaultValue: false, description: 'Skip unit tests')
           string(name: 'BRANCH', defaultValue: 'main', description: 'Branch to build')
       }
       
       // ... rest of pipeline
   }

Use parameters in stages:

groovy   stage('Unit Tests') {
       when {
           expression { return !params.SKIP_TESTS }
       }
       steps {
           sh 'mvn test'
       }
   }
Step 52: Configure Email Notifications (Optional)

In Jenkins: Manage Jenkins → Configure System
Scroll to "Extended E-mail Notification":

SMTP server: smtp.gmail.com
SMTP Port: 465
Use SSL: ✅
Credentials: Add your Gmail credentials
Default recipients: your email


Update Jenkinsfile post section:

groovy   post {
       success {
           emailext (
               subject: "SUCCESS: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
               body: "Good news! Build succeeded.",
               to: "your-email@gmail.com"
           )
       }
       failure {
           emailext (
               subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
               body: "Build failed. Check console output.",
               to: "your-email@gmail.com"
           )
       }
   }
Step 53: Set Up Prometheus Alerts (Optional)

SSH into Prometheus server
Create alert rules:

bash   sudo vi /etc/prometheus/alert_rules.yml

Add rules:

yaml   groups:
   - name: instance_alerts
     rules:
     - alert: InstanceDown
       expr: up == 0
       for: 1m
       labels:
         severity: critical
       annotations:
         summary: "Instance {{ $labels.instance }} down"
         description: "{{ $labels.instance }} has been down for more than 1 minute."
     
     - alert: HighCPU
       expr: 100 - (avg by(instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100) > 80
       for: 2m
       labels:
         severity: warning
       annotations:
         summary: "High CPU on {{ $labels.instance }}"
         description: "CPU usage is above 80%"

Update prometheus.yml:

bash   sudo vi /etc/prometheus/prometheus.yml
Add:
yaml   rule_files:
     - "alert_rules.yml"

Restart Prometheus:

bash   sudo systemctl restart prometheus

Phase 16: Security Hardening
Step 54: Secure Jenkins

Configure Security Realm:

Manage Jenkins → Configure Global Security
Security Realm: Jenkins' own user database
Authorization: Matrix-based security
Add user admin with all permissions
Check ✅ Allow users to sign up (uncheck for production)


Install security plugins:

OWASP Dependency-Check Plugin
Credentials Binding Plugin (should be installed)


Enable CSRF Protection:

Configure Global Security
Check ✅ Prevent Cross Site Request Forgery exploits



Step 55: Secure SonarQube

Change default password:

Already done (admin/admin → new password)


Disable anonymous access:

Administration → Configuration → Security
Uncheck Allow anonymous access
Force authentication: On


Create project-specific tokens:

Use different tokens for different projects



Step 56: Secure Nexus

Disable anonymous access for production:

⚙️ → Security → Anonymous Access
Uncheck Allow anonymous users to access the server


Create role-based access:

Security → Roles
Create role: Developer (read-only)
Create role: CI-Pipeline (read/write to specific repos)


Use deployment users:

Create user: jenkins-deployer
Assign role: CI-Pipeline
Update Jenkins credentials



Step 57: Secure EC2 Security Groups

Review and restrict Security Groups:
Jenkins Server:

Port 22: Your IP only (not 0.0.0.0/0)
Port 8080: Your IP + GitHub webhook IPs
Port 9100: Prometheus server IP only

Application Servers:

Port 22: Jenkins server IP only
Port 8080: Load balancer or your IP
Port 9100: Prometheus server IP only

SonarQube/Nexus:

Port 22: Your IP only
Ports 9000/8081: Jenkins server IP + your IP
Port 9100: Prometheus server IP only




Phase 17: Backup and Disaster Recovery
Step 58: Backup Jenkins Configuration

Install ThinBackup Plugin:

Manage Jenkins → Manage Plugins
Available → Search "ThinBackup"
Install without restart


Configure ThinBackup:

Manage Jenkins → ThinBackup → Settings
Backup directory: /var/lib/jenkins/backups
Backup schedule: H 2 * * * (daily at 2 AM)
Max backups: 7
Click Save


Create manual backup:

bash   ssh -i your-key.pem ec2-user@<Jenkins-Public-IP>
   sudo su - jenkins
   cd /var/lib/jenkins
   tar -czf jenkins-backup-$(date +%Y%m%d).tar.gz \
     jobs/ plugins/ config.xml credentials.xml
Step 59: Create AMI Snapshots

In AWS Console → EC2 → Instances
For each critical instance:

Select instance
Actions → Image and templates → Create image
Name: jenkins-backup-YYYYMMDD
Create image


Automate with AWS Backup (Optional):

AWS Backup → Create backup plan
Select instances
Schedule: Daily
Retention: 7 days



Step 60: Document Your Setup

Create documentation file:

bash   # On your local machine
   cd Jenkins-CICD-Project
   touch DEPLOYMENT_GUIDE.md

Document critical information:

markdown   # Deployment Guide
   
   ## Server Information
   - Jenkins: <IP> | admin/admin
   - SonarQube: <IP> | admin/<password>
   - Nexus: <IP> | admin/admin
   - Splunk: <IP> | admin/<password>
   - Prometheus: <IP>
   - Grafana: <IP> | admin/admin
   
   ## Credentials
   - Slack Token: <stored in Jenkins>
   - SonarQube Token: <stored in Jenkins>
   - Ansible User: ansibleadmin/ansibleadmin
   
   ## URLs
   - GitHub Repo: <your-repo>
   - Slack Channel: #yourname-jenkins-cicd-alerts
   
   ## Recovery Steps
   1. Launch new instances from AMIs
   2. Update IP addresses in configurations
   3. Restore Jenkins from backup
   4. Test pipeline

Commit documentation:

bash   git add DEPLOYMENT_GUIDE.md
   git commit -m "Added deployment documentation"
   git push origin main

Phase 18: Testing and Validation
Step 61: Comprehensive System Test
Create a test checklist and verify each component:
markdown## System Validation Checklist

### Infrastructure
- [ ] All 8 EC2 instances running
- [ ] All security groups configured correctly
- [ ] SSH access working to all instances

### Monitoring
- [ ] Prometheus showing all 6 targets as UP
- [ ] Grafana dashboard displaying metrics
- [ ] Node exporters accessible on all servers

### Logging
- [ ] Splunk receiving logs from all app servers
- [ ] Logs searchable in Splunk
- [ ] Forwarders connected to Splunk server

### CI/CD Pipeline
- [ ] Jenkins accessible and plugins installed
- [ ] Pipeline job created and configured
- [ ] GitHub webhook triggering builds
- [ ] Maven build succeeding
- [ ] Unit tests passing
- [ ] Checkstyle analysis completing

### Code Quality
- [ ] SonarQube analysis running
- [ ] Quality gate configured
- [ ] Quality gate webhook working
- [ ] Project visible in SonarQube

### Artifact Management
- [ ] Nexus repositories created
- [ ] Artifacts uploading to Nexus
- [ ] Artifacts versioned correctly

### Deployment
- [ ] Dev deployment successful
- [ ] Stage deployment successful
- [ ] Prod deployment with approval
- [ ] Applications accessible on all environments

### Notifications
- [ ] Slack notifications for all stages
- [ ] Success notifications received
- [ ] Failure notifications received

### Security
- [ ] Default passwords changed
- [ ] SSH keys configured
- [ ] Credentials stored in Jenkins
- [ ] Security groups restricted

### Documentation
- [ ] IP addresses documented
- [ ] Credentials documented
- [ ] Recovery procedures documented
Step 62: Perform End-to-End Test

Make a significant code change:

bash   cd Jenkins-CICD-Project
   # Edit application code
   vi src/main/webapp/index.jsp
   # Add: <h2>Version 2.0 - CI/CD Pipeline Test</h2>
   
   git add .
   git commit -m "Version 2.0 - Full pipeline test"
   git push origin main

Monitor entire flow:

Jenkins builds automatically
All stages complete successfully
Application deployed to all environments
New version visible in browser
Metrics updating in Grafana
Logs appearing in Splunk
Slack notifications received


Verify application access:

Dev: http://<Dev-IP>:8080/webapp/
Stage: http://<Stage-IP>:8080/webapp/
Prod: http://<Prod-IP>:8080/webapp/
All should show "Version 2.0"



Step 63: Load Testing (Optional)

Install Apache Bench on your local machine:

bash   # MacOS
   brew install apache2
   
   # Linux
   sudo yum install httpd-tools

Run load test:

bash   ab -n 1000 -c 10 http://<Prod-IP>:8080/webapp/

Monitor in Grafana:

Watch CPU, memory, network metrics
Verify alerting works if thresholds exceeded




Phase 19: Troubleshooting Common Issues
Issue 1: Pipeline Hangs at SonarQube Quality Gate
Symptoms:

Stage shows "Checking status of SonarQube task"
Waits indefinitely

Solutions:

Check SonarQube webhook:

bash   # In SonarQube
   Administration → Configuration → Webhooks
   # Verify URL is correct: http://<Jenkins-Private-IP>:8080/sonarqube-webhook/

Verify webhook is assigned to project:

Project Settings → Webhooks
Should see webhook listed


Check Jenkins logs:

bash   sudo tail -f /var/lib/jenkins/logs/jenkins.log
Issue 2: Nexus Upload Fails
Symptoms:

"Error uploading to Nexus"
Connection refused

Solutions:

Verify Nexus is running:

bash   ssh -i your-key.pem ec2-user@<Nexus-IP>
   sudo systemctl status nexus

Check Nexus URL in Jenkinsfile:

Should use Private IP, not Public
Port should be 8081


Verify credentials:

Manage Jenkins → Credentials
Test Nexus login manually



Issue 3: Deployment Fails - Permission Denied
Symptoms:

"Permission denied (publickey)"
SSH connection fails

Solutions:

Verify SSH key exchange:

bash   # On Jenkins server
   sudo su - jenkins
   ssh ansibleadmin@<Target-Private-IP>

Check ansibleadmin user exists:

bash   # On target server
   cat /etc/passwd | grep ansibleadmin

Verify authorized_keys:

bash   # On target server
   sudo su - ansibleadmin
   cat ~/.ssh/authorized_keys
   # Should contain Jenkins public key
Issue 4: Grafana Shows No Data
Symptoms:

Dashboard loads but shows "No data"
Prometheus data source shows as connected

Solutions:

Verify Prometheus targets:

Prometheus UI → Status → Targets
All should be UP


Check time range in Grafana:

Try "Last 5 minutes" instead of "Last 24 hours"


Verify data source URL:

Should use Private IP
Port should be 9090
Click "Save & Test"



Issue 5: Application Not Accessible
Symptoms:

Browser shows "Unable to connect"
curl timeout

Solutions:

Check Tomcat is running:

bash   sudo systemctl status tomcat

Verify security group:

Port 8080 should be open
Check from AWS Console


Check webapp deployment:

bash   ls -l /opt/apache-tomcat-8.5.82/webapps/
   # Should see webapp.war and webapp directory
   
   # Check logs
   sudo tail -f /var/log/tomcat/catalina.out

Phase 20: Cleanup and Cost Optimization
Step 64: Stop Non-Essential Services
When not actively using the pipeline:

Stop EC2 instances:

bash   # AWS Console → EC2 → Instances
   # Select instances → Instance State → Stop
   
   # Or using AWS CLI
   aws ec2 stop-instances --instance-ids i-xxxxx i-yyyyy

Stop specific services:

Can stop Stage and Prod environments when not testing
Keep Dev, Jenkins, SonarQube, Nexus running



Step 65: Resource Cleanup (After Project Completion)
WARNING: Only do this if you're completely done with the project

Terminate EC2 instances:

Select all instances
Actions → Instance State → Terminate


Delete EBS volumes:

EC2 → Volumes
Select volumes with state "available"
Actions → Delete


Delete snapshots/AMIs:

EC2 → Snapshots → Delete
EC2 → AMIs → Deregister


Delete security groups:

EC2 → Security Groups
Select custom groups
Actions → Delete


Clean up local files:

bash   # Keep your repository for future reference
   # But can remove large log files
   cd Jenkins-CICD-Project
   rm -rf target/ logs/
```

---

## **Congratulations! 🎉**

You've successfully built and deployed a **complete enterprise-grade CI/CD pipeline** including:

### ✅ What You've Accomplished:

1. **Infrastructure as Code** - 8 EC2 instances configured
2. **Source Control** - GitHub integration with webhooks
3. **Continuous Integration** - Jenkins automated builds
4. **Code Quality** - SonarQube analysis and quality gates
5. **Artifact Management** - Nexus repository
6. **Automated Testing** - Unit tests and static code analysis
7. **Continuous Deployment** - Multi-environment deployments
8. **Monitoring** - Prometheus + Grafana metrics
9. **Logging** - Centralized Splunk logging
10. **Notifications** - Slack integration
11. **Security** - SSH keys, credentials management
12. **Approval Workflows** - Manual production approvals

### 📊 Your Pipeline Flow:
```
Developer Push → GitHub → Webhook → Jenkins
    ↓
Maven Build → Unit Tests → Checkstyle
    ↓
SonarQube Analysis → Quality Gate
    ↓
Nexus Artifact Upload
    ↓
Deploy to Dev → Deploy to Stage → [Approval] → Deploy to Prod
    ↓
Slack Notifications + Monitoring + Logging
🎯 Interview Talking Points:

Designed and implemented end-to-end CI/CD pipeline
Automated deployment to multiple environments
Integrated code quality gates and security scanning
Implemented infrastructure monitoring with Prometheus/Grafana
Centralized logging with Splunk
Managed artifacts with Nexus Repository
Configured automated notifications and approval workflows

📚 Next Steps to Enhance:

Add Docker containerization
Implement Kubernetes orchestration
Add infrastructure as code (Terraform)
Implement blue-green deployments
Add performance testing (JMeter)
Implement database migrations
Add API testing
Configure disaster recovery


You now have a production-ready DevOps skillset! Keep this project in your portfolio and be ready to explain every component in interviews. Good luck! 🚀RetryEBring in Ansible and trivyIntegrating Ansible and Trivy into the CI/CD Pipeline
I'll show you how to properly integrate Ansible for deployment automation and Trivy for container/vulnerability scanning into your existing pipeline.

Part 1: Ansible Integration for Deployment Automation
Step 1: Install and Configure Ansible on Jenkins Server

SSH into Jenkins-Maven-Ansible server:

bash   ssh -i your-key.pem ec2-user@<Jenkins-Public-IP>

Install Ansible:

bash   sudo amazon-linux-extras install ansible2 -y
   
   # Verify installation
   ansible --version

Create Ansible directory structure:

bash   sudo mkdir -p /opt/ansible/{playbooks,inventory,roles}
   sudo chown -R jenkins:jenkins /opt/ansible

Switch to Jenkins user:

bash   sudo su - jenkins
   cd /opt/ansible
Step 2: Create Ansible Inventory Files

Create inventory for all environments:

bash   vi /opt/ansible/inventory/hosts

Add the following content:

ini   # /opt/ansible/inventory/hosts
   
   [dev]
   dev-server ansible_host=<Dev-Private-IP> ansible_user=ansibleadmin
   
   [stage]
   stage-server ansible_host=<Stage-Private-IP> ansible_user=ansibleadmin
   
   [prod]
   prod-server ansible_host=<Prod-Private-IP> ansible_user=ansibleadmin
   
   [all:vars]
   ansible_ssh_private_key_file=/var/lib/jenkins/.ssh/id_rsa
   ansible_ssh_common_args='-o StrictHostKeyChecking=no'
   tomcat_home=/opt/apache-tomcat-8.5.82
   tomcat_user=tomcat
   app_name=webapp

Test connectivity:

bash   ansible all -i /opt/ansible/inventory/hosts -m ping
```

   Expected output:
```
   dev-server | SUCCESS => {
       "changed": false,
       "ping": "pong"
   }
   stage-server | SUCCESS => ...
   prod-server | SUCCESS => ...
Step 3: Create Ansible Playbooks
A) Main Deployment Playbook
bashvi /opt/ansible/playbooks/deploy-webapp.yml
yaml---
# /opt/ansible/playbooks/deploy-webapp.yml
- name: Deploy Java Web Application
  hosts: "{{ target_env }}"
  become: yes
  vars:
    artifact_path: "{{ workspace }}/webapp/target/webapp.war"
    backup_dir: "{{ tomcat_home }}/backup"
    deployment_timestamp: "{{ ansible_date_time.epoch }}"
    
  tasks:
    - name: Display deployment information
      debug:
        msg: "Deploying {{ app_name }} to {{ target_env }} environment"
    
    - name: Create backup directory if not exists
      file:
        path: "{{ backup_dir }}"
        state: directory
        owner: "{{ tomcat_user }}"
        group: "{{ tomcat_user }}"
        mode: '0755'
    
    - name: Check if old webapp exists
      stat:
        path: "{{ tomcat_home }}/webapps/{{ app_name }}.war"
      register: old_webapp
    
    - name: Backup existing application
      copy:
        src: "{{ tomcat_home }}/webapps/{{ app_name }}.war"
        dest: "{{ backup_dir }}/{{ app_name }}-{{ deployment_timestamp }}.war"
        remote_src: yes
      when: old_webapp.stat.exists
      ignore_errors: yes
    
    - name: Stop Tomcat service
      systemd:
        name: tomcat
        state: stopped
      register: tomcat_stopped
    
    - name: Wait for Tomcat to stop
      wait_for:
        port: 8080
        state: stopped
        timeout: 60
      when: tomcat_stopped is changed
    
    - name: Remove old application directory
      file:
        path: "{{ tomcat_home }}/webapps/{{ app_name }}"
        state: absent
    
    - name: Remove old WAR file
      file:
        path: "{{ tomcat_home }}/webapps/{{ app_name }}.war"
        state: absent
    
    - name: Copy new application WAR file
      copy:
        src: "{{ artifact_path }}"
        dest: "{{ tomcat_home }}/webapps/{{ app_name }}.war"
        owner: "{{ tomcat_user }}"
        group: "{{ tomcat_user }}"
        mode: '0644'
    
    - name: Start Tomcat service
      systemd:
        name: tomcat
        state: started
        enabled: yes
    
    - name: Wait for Tomcat to start
      wait_for:
        port: 8080
        state: started
        timeout: 60
        delay: 5
    
    - name: Wait for application deployment
      uri:
        url: "http://localhost:8080/{{ app_name }}/"
        status_code: 200
        timeout: 120
      register: app_status
      until: app_status.status == 200
      retries: 10
      delay: 10
    
    - name: Display deployment success message
      debug:
        msg: "Application successfully deployed to {{ target_env }}"
    
    - name: Clean old backups (keep last 5)
      shell: |
        cd {{ backup_dir }}
        ls -t {{ app_name }}-*.war | tail -n +6 | xargs -r rm --
      ignore_errors: yes
B) Rollback Playbook
bashvi /opt/ansible/playbooks/rollback-webapp.yml
yaml---
# /opt/ansible/playbooks/rollback-webapp.yml
- name: Rollback Java Web Application
  hosts: "{{ target_env }}"
  become: yes
  
  tasks:
    - name: Get latest backup
      shell: ls -t {{ backup_dir }}/{{ app_name }}-*.war | head -n 1
      register: latest_backup
      failed_when: latest_backup.rc != 0
    
    - name: Display rollback information
      debug:
        msg: "Rolling back to {{ latest_backup.stdout }}"
    
    - name: Stop Tomcat
      systemd:
        name: tomcat
        state: stopped
    
    - name: Remove current application
      file:
        path: "{{ tomcat_home }}/webapps/{{ app_name }}.war"
        state: absent
    
    - name: Remove application directory
      file:
        path: "{{ tomcat_home }}/webapps/{{ app_name }}"
        state: absent
    
    - name: Restore backup
      copy:
        src: "{{ latest_backup.stdout }}"
        dest: "{{ tomcat_home }}/webapps/{{ app_name }}.war"
        remote_src: yes
        owner: "{{ tomcat_user }}"
        group: "{{ tomcat_user }}"
    
    - name: Start Tomcat
      systemd:
        name: tomcat
        state: started
    
    - name: Wait for application
      wait_for:
        port: 8080
        state: started
        timeout: 60
C) Health Check Playbook
bashvi /opt/ansible/playbooks/health-check.yml
yaml---
# /opt/ansible/playbooks/health-check.yml
- name: Application Health Check
  hosts: "{{ target_env }}"
  become: yes
  
  tasks:
    - name: Check Tomcat service status
      systemd:
        name: tomcat
      register: tomcat_status
    
    - name: Check if Tomcat is listening
      wait_for:
        port: 8080
        state: started
        timeout: 5
      register: tomcat_port
    
    - name: Check application endpoint
      uri:
        url: "http://localhost:8080/{{ app_name }}/"
        status_code: 200
      register: app_response
    
    - name: Check disk space
      shell: df -h {{ tomcat_home }} | tail -1 | awk '{print $5}' | sed 's/%//'
      register: disk_usage
    
    - name: Display health status
      debug:
        msg:
          - "Tomcat Status: {{ tomcat_status.status.ActiveState }}"
          - "Application Status: {{ app_response.status }}"
          - "Disk Usage: {{ disk_usage.stdout }}%"
    
    - name: Fail if disk usage too high
      fail:
        msg: "Disk usage is {{ disk_usage.stdout }}%, exceeds 85%"
      when: disk_usage.stdout | int > 85
Step 4: Create Ansible Role for Tomcat Management
bashmkdir -p /opt/ansible/roles/tomcat/{tasks,handlers,templates,files}

Create tasks:

bash   vi /opt/ansible/roles/tomcat/tasks/main.yml
yaml   ---
   # /opt/ansible/roles/tomcat/tasks/main.yml
   - name: Ensure Tomcat is installed
     yum:
       name: tomcat
       state: present
   
   - name: Configure Tomcat memory settings
     template:
       src: setenv.sh.j2
       dest: "{{ tomcat_home }}/bin/setenv.sh"
       mode: '0755'
     notify: restart tomcat
   
   - name: Ensure Tomcat is running
     systemd:
       name: tomcat
       state: started
       enabled: yes

Create handler:

bash   vi /opt/ansible/roles/tomcat/handlers/main.yml
yaml   ---
   # /opt/ansible/roles/tomcat/handlers/main.yml
   - name: restart tomcat
     systemd:
       name: tomcat
       state: restarted

Create template:

bash   vi /opt/ansible/roles/tomcat/templates/setenv.sh.j2
bash   #!/bin/bash
   # Tomcat Memory Settings
   export CATALINA_OPTS="-Xms512M -Xmx1024M -XX:MaxPermSize=256M"
   export JAVA_OPTS="-Djava.security.egd=file:/dev/./urandom"
Step 5: Update Jenkinsfile with Ansible Integration

Open your Jenkinsfile on local machine:

bash   vi Jenkinsfile

Replace deployment stages with Ansible:

groovy// ... previous stages remain the same ...

stage("Deploy To Dev Environment") {
    steps {
        echo "Deploying to Dev Environment..."
        script {
            sshagent(['Ansible-Credential']) {
                sh """
                    ansible-playbook /opt/ansible/playbooks/deploy-webapp.yml \
                    -i /opt/ansible/inventory/hosts \
                    -e "target_env=dev" \
                    -e "workspace=${WORKSPACE}" \
                    -vv
                """
            }
        }
        echo "Application deployed to Dev Environment successfully!"
    }
}

stage("Deploy To Stage Environment") {
    steps {
        echo "Deploying to Stage Environment..."
        script {
            sshagent(['Ansible-Credential']) {
                sh """
                    ansible-playbook /opt/ansible/playbooks/deploy-webapp.yml \
                    -i /opt/ansible/inventory/hosts \
                    -e "target_env=stage" \
                    -e "workspace=${WORKSPACE}" \
                    -vv
                """
            }
        }
        echo "Application deployed to Stage Environment successfully!"
    }
}

stage('Approval For Production') {
    steps {
        input message: 'Deploy to Production?', ok: 'Deploy'
    }
}

stage("Deploy To Production Environment") {
    steps {
        echo "Deploying to Production Environment..."
        script {
            sshagent(['Ansible-Credential']) {
                sh """
                    ansible-playbook /opt/ansible/playbooks/deploy-webapp.yml \
                    -i /opt/ansible/inventory/hosts \
                    -e "target_env=prod" \
                    -e "workspace=${WORKSPACE}" \
                    -vv
                """
            }
        }
        echo "Application deployed to Production Environment successfully!"
    }
}

stage("Production Health Check") {
    steps {
        script {
            sh """
                ansible-playbook /opt/ansible/playbooks/health-check.yml \
                -i /opt/ansible/inventory/hosts \
                -e "target_env=prod" \
                -vv
            """
        }
    }
}

Part 2: Trivy Integration for Vulnerability Scanning
Step 6: Install Trivy on Jenkins Server

SSH into Jenkins server:

bash   ssh -i your-key.pem ec2-user@<Jenkins-Public-IP>

Install Trivy:

bash   # Add Trivy repository
   sudo rpm -ivh https://github.com/aquasecurity/trivy/releases/download/v0.48.0/trivy_0.48.0_Linux-64bit.rpm
   
   # Or use the install script
   curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sudo sh -s -- -b /usr/local/bin
   
   # Verify installation
   trivy --version

Update Trivy database:

bash   trivy image --download-db-only
Step 7: Create Trivy Scanning Scripts

Create Trivy scan directory:

bash   sudo mkdir -p /opt/trivy/{reports,configs}
   sudo chown -R jenkins:jenkins /opt/trivy

Create configuration file:

bash   sudo vi /opt/trivy/configs/trivy.yaml
yaml   # /opt/trivy/configs/trivy.yaml
   cache:
     dir: /var/lib/jenkins/.cache/trivy
   
   db:
     repository: ghcr.io/aquasecurity/trivy-db
   
   severity:
     - CRITICAL
     - HIGH
     - MEDIUM
   
   vulnerability:
     type:
       - os
       - library
   
   format: json
   output: /opt/trivy/reports/scan-report.json

Create filesystem scan script:

bash   sudo vi /opt/trivy/scan-filesystem.sh
bash   #!/bin/bash
   # /opt/trivy/scan-filesystem.sh
   
   WORKSPACE=$1
   REPORT_DIR="/opt/trivy/reports"
   TIMESTAMP=$(date +%Y%m%d_%H%M%S)
   
   echo "Starting Trivy filesystem scan..."
   
   # Scan the workspace for vulnerabilities
   trivy fs \
     --severity HIGH,CRITICAL \
     --format json \
     --output ${REPORT_DIR}/fs-scan-${TIMESTAMP}.json \
     ${WORKSPACE}
   
   # Generate HTML report
   trivy fs \
     --severity HIGH,CRITICAL \
     --format template \
     --template "@/usr/local/share/trivy/templates/html.tpl" \
     --output ${REPORT_DIR}/fs-scan-${TIMESTAMP}.html \
     ${WORKSPACE}
   
   # Check exit code
   if [ $? -eq 0 ]; then
     echo "Trivy scan completed successfully"
     
     # Count vulnerabilities
     CRITICAL=$(jq '[.Results[].Vulnerabilities[]? | select(.Severity=="CRITICAL")] | length' ${REPORT_DIR}/fs-scan-${TIMESTAMP}.json)
     HIGH=$(jq '[.Results[].Vulnerabilities[]? | select(.Severity=="HIGH")] | length' ${REPORT_DIR}/fs-scan-${TIMESTAMP}.json)
     
     echo "Found ${CRITICAL} CRITICAL and ${HIGH} HIGH vulnerabilities"
     
     # Fail build if critical vulnerabilities found
     if [ ${CRITICAL} -gt 0 ]; then
       echo "ERROR: Critical vulnerabilities found!"
       exit 1
     fi
     
     exit 0
   else
     echo "Trivy scan failed"
     exit 1
   fi

Create dependency scan script:

bash   sudo vi /opt/trivy/scan-dependencies.sh
bash   #!/bin/bash
   # /opt/trivy/scan-dependencies.sh
   
   POM_FILE=$1
   REPORT_DIR="/opt/trivy/reports"
   TIMESTAMP=$(date +%Y%m%d_%H%M%S)
   
   echo "Starting Trivy dependency scan..."
   
   # Scan Maven dependencies
   trivy fs \
     --scanners vuln \
     --severity HIGH,CRITICAL \
     --format json \
     --output ${REPORT_DIR}/dep-scan-${TIMESTAMP}.json \
     --skip-dirs "target" \
     $(dirname ${POM_FILE})
   
   # Generate table format for console
   trivy fs \
     --scanners vuln \
     --severity HIGH,CRITICAL \
     --format table \
     --skip-dirs "target" \
     $(dirname ${POM_FILE})
   
   exit 0

Create WAR file scan script:

bash   sudo vi /opt/trivy/scan-artifact.sh
bash   #!/bin/bash
   # /opt/trivy/scan-artifact.sh
   
   ARTIFACT_PATH=$1
   REPORT_DIR="/opt/trivy/reports"
   TIMESTAMP=$(date +%Y%m%d_%H%M%S)
   ARTIFACT_NAME=$(basename ${ARTIFACT_PATH})
   
   echo "Starting Trivy artifact scan for ${ARTIFACT_NAME}..."
   
   # Create temp directory for extraction
   TEMP_DIR="/tmp/trivy-scan-${TIMESTAMP}"
   mkdir -p ${TEMP_DIR}
   
   # Extract WAR file
   cd ${TEMP_DIR}
   unzip -q ${ARTIFACT_PATH}
   
   # Scan extracted contents
   trivy fs \
     --severity HIGH,CRITICAL \
     --format json \
     --output ${REPORT_DIR}/artifact-scan-${TIMESTAMP}.json \
     ${TEMP_DIR}
   
   # Generate HTML report
   trivy fs \
     --severity HIGH,CRITICAL \
     --format template \
     --template "@/usr/local/share/trivy/templates/html.tpl" \
     --output ${REPORT_DIR}/artifact-scan-${TIMESTAMP}.html \
     ${TEMP_DIR}
   
   # Scan for secrets
   trivy fs \
     --scanners secret \
     --format table \
     ${TEMP_DIR}
   
   # Cleanup
   rm -rf ${TEMP_DIR}
   
   # Parse results
   CRITICAL=$(jq '[.Results[].Vulnerabilities[]? | select(.Severity=="CRITICAL")] | length' ${REPORT_DIR}/artifact-scan-${TIMESTAMP}.json)
   HIGH=$(jq '[.Results[].Vulnerabilities[]? | select(.Severity=="HIGH")] | length' ${REPORT_DIR}/artifact-scan-${TIMESTAMP}.json)
   
   echo "Artifact scan completed: ${CRITICAL} CRITICAL, ${HIGH} HIGH vulnerabilities"
   
   # Fail if critical vulnerabilities
   if [ ${CRITICAL} -gt 5 ]; then
     echo "ERROR: Too many critical vulnerabilities (${CRITICAL})"
     exit 1
   fi
   
   exit 0

Make scripts executable:

bash   sudo chmod +x /opt/trivy/*.sh
   sudo chown jenkins:jenkins /opt/trivy/*.sh
Step 8: Install Required Tools
bash# Install jq for JSON parsing
sudo yum install jq -y

# Install unzip for WAR extraction
sudo yum install unzip -y
Step 9: Update Jenkinsfile with Trivy Scanning
Add Trivy stages to your Jenkinsfile:
groovypipeline {
    agent any
    
    tools {
        maven "localMaven"
        jdk "localJdk"
    }
    
    environment {
        WORKSPACE = "${env.WORKSPACE}"
        NEXUS_CREDENTIAL_ID = 'Nexus-Credential'
    }
    
    stages {
        
        // ... existing stages ...
        
        stage('Trivy Filesystem Scan') {
            steps {
                echo "Running Trivy filesystem vulnerability scan..."
                script {
                    sh """
                        /opt/trivy/scan-filesystem.sh ${WORKSPACE}
                    """
                }
            }
            post {
                always {
                    archiveArtifacts artifacts: '/opt/trivy/reports/fs-scan-*.html', 
                                   fingerprint: true, 
                                   allowEmptyArchive: true
                }
            }
        }
        
        stage('Maven Build & Test') {
            steps {
                sh 'mvn clean install'
            }
        }
        
        stage('Trivy Dependency Scan') {
            steps {
                echo "Scanning Maven dependencies for vulnerabilities..."
                script {
                    sh """
                        /opt/trivy/scan-dependencies.sh ${WORKSPACE}/pom.xml
                    """
                }
            }
        }
        
        // ... Checkstyle, SonarQube stages ...
        
        stage('Trivy Artifact Scan') {
            steps {
                echo "Scanning WAR artifact for vulnerabilities..."
                script {
                    sh """
                        /opt/trivy/scan-artifact.sh ${WORKSPACE}/webapp/target/webapp.war
                    """
                }
            }
            post {
                always {
                    archiveArtifacts artifacts: '/opt/trivy/reports/artifact-scan-*.html',
                                   fingerprint: true,
                                   allowEmptyArchive: true
                    
                    // Publish HTML report
                    publishHTML([
                        allowMissing: false,
                        alwaysLinkToLastBuild: true,
                        keepAll: true,
                        reportDir: '/opt/trivy/reports',
                        reportFiles: 'artifact-scan-*.html',
                        reportName: 'Trivy Security Report'
                    ])
                }
            }
        }
        
        stage("Nexus Artifact Uploader") {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '<Nexus-Private-IP>:8081',
                    groupId: 'webapp',
                    version: "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}",
                    repository: 'maven-project-releases',
                    credentialsId: "${NEXUS_CREDENTIAL_ID}",
                    artifacts: [
                        [artifactId: 'webapp',
                        classifier: '',
                        file: 'webapp/target/webapp.war',
                        type: 'war']
                    ]
                )
            }
        }
        
        stage("Deploy To Dev Environment") {
            steps {
                echo "Deploying to Dev Environment with Ansible..."
                script {
                    sshagent(['Ansible-Credential']) {
                        sh """
                            ansible-playbook /opt/ansible/playbooks/deploy-webapp.yml \
                            -i /opt/ansible/inventory/hosts \
                            -e "target_env=dev" \
                            -e "workspace=${WORKSPACE}" \
                            -vv
                        """
                    }
                }
            }
        }
        
        stage("Dev Health Check") {
            steps {
                script {
                    sh """
                        ansible-playbook /opt/ansible/playbooks/health-check.yml \
                        -i /opt/ansible/inventory/hosts \
                        -e "target_env=dev"
                    """
                }
            }
        }
        
        stage("Deploy To Stage Environment") {
            steps {
                echo "Deploying to Stage Environment with Ansible..."
                script {
                    sshagent(['Ansible-Credential']) {
                        sh """
                            ansible-playbook /opt/ansible/playbooks/deploy-webapp.yml \
                            -i /opt/ansible/inventory/hosts \
                            -e "target_env=stage" \
                            -e "workspace=${WORKSPACE}" \
                            -vv
                        """
                    }
                }
            }
        }
        
        stage("Stage Health Check") {
            steps {
                script {
                    sh """
                        ansible-playbook /opt/ansible/playbooks/health-check.yml \
                        -i /opt/ansible/inventory/hosts \
                        -e "target_env=stage"
                    """
                }
            }
        }
        
        stage('Approval For Production') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    input message: 'Deploy to Production?', 
                          ok: 'Deploy',
                          submitter: 'admin'
                }
            }
        }
        
        stage("Deploy To Production Environment") {
            steps {
                echo "Deploying to Production Environment with Ansible..."
                script {
                    sshagent(['Ansible-Credential']) {
                        sh """
                            ansible-playbook /opt/ansible/playbooks/deploy-webapp.yml \
                            -i /opt/ansible/inventory/hosts \
                            -e "target_env=prod" \
                            -e "workspace=${WORKSPACE}" \
                            -vv
                        """
                    }
                }
            }
        }
        
        stage("Production Health Check") {
            steps {
                script {
                    sh """
                        ansible-playbook /opt/ansible/playbooks/health-check.yml \
                        -i /opt/ansible/inventory/hosts \
                        -e "target_env=prod"
                    """
                }
            }
        }
    }
    
    post {
        success {
            slackSend channel: '#yourname-jenkins-cicd-alerts',
                     color: 'good',
                     message: """
                     *${currentBuild.currentResult}:* Job ${env.JOB_NAME} 
                     Build ${env.BUILD_NUMBER}
                     Trivy Scan: PASSED
                     More info at: ${env.BUILD_URL}
                     """
        }
        failure {
            slackSend channel: '#yourname-jenkins-cicd-alerts',
                     color: 'danger',
                     message: """
                     *${currentBuild.currentResult}:* Job ${env.JOB_NAME} 
                     Build ${env.BUILD_NUMBER}
                     Check Trivy reports and logs
                     More info at: ${env.BUILD_URL}
                     """
        }
    }
}
Step 10: Install HTML Publisher Plugin

In Jenkins:

Manage Jenkins → Manage Plugins
Available → Search "HTML Publisher"
Install without restart



Step 11: Configure Trivy Report Viewing

In Jenkins Pipeline Configuration:

Configure → Post-build Actions
Add post-build action → Publish HTML reports
HTML directory to archive: /opt/trivy/reports
Index page: artifact-scan-*.html
Report title: Trivy Security Scan Report



Step 12: Create Ansible Playbook for Trivy Scanning
bashvi /opt/ansible/playbooks/security-scan.yml
yaml---
# /opt/ansible/playbooks/security-scan.yml
- name: Run Security Scans on Deployed Applications
  hosts: "{{ target_env }}"
  become: yes
  
  tasks:
    - name: Install Trivy on target hosts
      shell: |
        curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin
      args:
        creates: /usr/local/bin/trivy
    
    - name: Scan deployed application
      shell: |
        trivy rootfs \
          --severity HIGH,CRITICAL \
          --format json \
          --output /tmp/trivy-scan-{{ ansible_hostname }}.json \
          {{ tomcat_home }}/webapps/{{ app_name }}
      register: scan_result
    
    - name: Fetch scan results
      fetch:
        src: /tmp/trivy-scan-{{ ansible_hostname }}.json
        dest: /opt/trivy/reports/
        flat: yes
    
    - name: Display scan summary
      shell: |
        trivy rootfs \
          --severity HIGH,CRITICAL \
          --format table \
          {{ tomcat_home }}/webapps/{{ app_name }}
Step 13: Test Ansible Deployment

Test deployment to Dev manually:

bash   sudo su - jenkins
   cd /opt/ansible
   
   ansible-playbook playbooks/deploy-webapp.yml \
     -i inventory/hosts \
     -e "target_env=dev" \
     -e "workspace=/var/lib/jenkins/workspace/jenkins-complete-cicd-pipeline" \
     -vv

Test health check:

bash   ansible-playbook playbooks/health-check.yml \
     -i inventory/hosts \
     -e "target_env=dev"

Test rollback (if needed):

bash   ansible-playbook playbooks/rollback-webapp.yml \
     -i inventory/hosts \
     -e "target_env=dev"
Step 14: Test Trivy Scanning

Test filesystem scan:

bash   sudo su - jenkins
   /opt/trivy/scan-filesystem.sh /var/lib/jenkins/workspace/jenkins-complete-cicd-pipeline

Test artifact scan:

bash   /opt/trivy/scan-artifact.sh /var/lib/jenkins/workspace/jenkins-complete-cicd-pipeline/webapp/target/webapp.war

View reports:

bash   ls -lh /opt/trivy/reports/
Step 15: Commit and Push Changes
bash# On your local machine
cd Jenkins-CICD-Project

# Add all changes
git add Jenkinsfile

# Commit
git commit -m "Integrated Ansible for deployment automation and Trivy for security scanning"

# Push to GitHub
git push origin main
Step 16: Run Complete Pipeline

Go to Jenkins → Your Pipeline
Click "Build Now"
Monitor stages:

✅ Trivy Filesystem Scan
✅ Maven Build
✅ Trivy Dependency Scan
✅ Checkstyle
✅ SonarQube Analysis
✅ SonarQube Quality Gate
✅ Trivy Artifact Scan
✅ Nexus Upload
✅ Ansible Deploy to Dev
✅ Dev Health Check
✅ Ansible Deploy to Stage
✅ Stage Health Check
⏸️ Approval for Production
✅ Ansible Deploy to Prod
✅ Production Health Check


View Trivy Reports:

In Jenkins build → Click "Trivy Security Report"
Review vulnerabilities
Check severity levels



Step 17: Create Automated Security Report
bashvi /opt/ansible/playbooks/generate-security-report.yml
yaml---
# Generate comprehensive security report
- name: Generate Security Report
  hosts: localhost
  gather_facts: noRetryEContinueyaml---
# Generate comprehensive security report
- name: Generate Security Report
  hosts: localhost
  gather_facts: no
  
  vars:
    report_dir: "/opt/trivy/reports"
    output_file: "{{ report_dir }}/security-summary-{{ ansible_date_time.date }}.html"
  
  tasks:
    - name: Find all Trivy scan reports
      find:
        paths: "{{ report_dir }}"
        patterns: "*-scan-*.json"
        age: "-1d"
      register: scan_files
    
    - name: Create consolidated report
      template:
        src: /opt/ansible/templates/security-report.html.j2
        dest: "{{ output_file }}"
    
    - name: Display report location
      debug:
        msg: "Security report generated at {{ output_file }}"
Create the template:
bashmkdir -p /opt/ansible/templates
vi /opt/ansible/templates/security-report.html.j2
html<!DOCTYPE html>
<html>
<head>
    <title>Security Scan Report - {{ ansible_date_time.date }}</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 20px; }
        h1 { color: #333; }
        .critical { color: #d9534f; font-weight: bold; }
        .high { color: #f0ad4e; font-weight: bold; }
        .medium { color: #5bc0de; }
        table { border-collapse: collapse; width: 100%; margin: 20px 0; }
        th, td { border: 1px solid #ddd; padding: 12px; text-align: left; }
        th { background-color: #4CAF50; color: white; }
        tr:nth-child(even) { background-color: #f2f2f2; }
        .summary { background-color: #e7f3fe; padding: 15px; border-radius: 5px; margin: 20px 0; }
    </style>
</head>
<body>
    <h1>Security Scan Summary Report</h1>
    <p>Generated: {{ ansible_date_time.iso8601 }}</p>
    
    <div class="summary">
        <h2>Scan Overview</h2>
        <p>Total scans performed: {{ scan_files.matched }}</p>
    </div>
    
    <h2>Scan Results</h2>
    <table>
        <tr>
            <th>Scan Type</th>
            <th>Critical</th>
            <th>High</th>
            <th>Medium</th>
            <th>Status</th>
        </tr>
        {% for file in scan_files.files %}
        <tr>
            <td>{{ file.path | basename }}</td>
            <td class="critical">{{ lookup('pipe', 'jq "[.Results[].Vulnerabilities[]? | select(.Severity==\"CRITICAL\")] | length" ' + file.path) }}</td>
            <td class="high">{{ lookup('pipe', 'jq "[.Results[].Vulnerabilities[]? | select(.Severity==\"HIGH\")] | length" ' + file.path) }}</td>
            <td class="medium">{{ lookup('pipe', 'jq "[.Results[].Vulnerabilities[]? | select(.Severity==\"MEDIUM\")] | length" ' + file.path) }}</td>
            <td>Completed</td>
        </tr>
        {% endfor %}
    </table>
</body>
</html>

Part 3: Advanced Ansible Features
Step 18: Create Dynamic Inventory Script
bashvi /opt/ansible/inventory/ec2_inventory.sh
bash#!/bin/bash
# Dynamic inventory script for AWS EC2

cat <<EOF
{
  "dev": {
    "hosts": ["$(aws ec2 describe-instances --filters "Name=tag:Name,Values=Dev-Env" "Name=instance-state-name,Values=running" --query 'Reservations[0].Instances[0].PrivateIpAddress' --output text)"],
    "vars": {
      "ansible_user": "ansibleadmin",
      "env_type": "development"
    }
  },
  "stage": {
    "hosts": ["$(aws ec2 describe-instances --filters "Name=tag:Name,Values=Stage-Env" "Name=instance-state-name,Values=running" --query 'Reservations[0].Instances[0].PrivateIpAddress' --output text)"],
    "vars": {
      "ansible_user": "ansibleadmin",
      "env_type": "staging"
    }
  },
  "prod": {
    "hosts": ["$(aws ec2 describe-instances --filters "Name=tag:Name,Values=Prod-Env" "Name=instance-state-name,Values=running" --query 'Reservations[0].Instances[0].PrivateIpAddress' --output text)"],
    "vars": {
      "ansible_user": "ansibleadmin",
      "env_type": "production"
    }
  },
  "_meta": {
    "hostvars": {}
  }
}
EOF
bashchmod +x /opt/ansible/inventory/ec2_inventory.sh
Step 19: Create Advanced Deployment Playbook with Blue-Green Strategy
bashvi /opt/ansible/playbooks/blue-green-deploy.yml
yaml---
# Blue-Green Deployment Strategy
- name: Blue-Green Deployment
  hosts: "{{ target_env }}"
  become: yes
  serial: 1
  
  vars:
    blue_port: 8080
    green_port: 8081
    health_check_retries: 5
    health_check_delay: 10
  
  tasks:
    - name: Check current active version
      shell: netstat -tuln | grep :{{ blue_port }} | wc -l
      register: blue_active
      changed_when: false
    
    - name: Determine deployment target
      set_fact:
        deploy_port: "{{ green_port if blue_active.stdout|int > 0 else blue_port }}"
        current_port: "{{ blue_port if blue_active.stdout|int > 0 else green_port }}"
    
    - name: Install secondary Tomcat instance
      yum:
        name: tomcat
        state: present
      when: green_port == deploy_port
    
    - name: Configure secondary Tomcat on port {{ green_port }}
      template:
        src: /opt/ansible/templates/server.xml.j2
        dest: /opt/tomcat-green/conf/server.xml
      vars:
        tomcat_port: "{{ green_port }}"
      when: green_port == deploy_port
    
    - name: Deploy application to {{ deploy_port }}
      copy:
        src: "{{ workspace }}/webapp/target/webapp.war"
        dest: "/opt/apache-tomcat-8.5.82/webapps/webapp.war"
    
    - name: Start new version
      systemd:
        name: tomcat
        state: started
    
    - name: Wait for new version health check
      uri:
        url: "http://localhost:{{ deploy_port }}/{{ app_name }}/"
        status_code: 200
      register: health_check
      until: health_check.status == 200
      retries: "{{ health_check_retries }}"
      delay: "{{ health_check_delay }}"
    
    - name: Run smoke tests
      uri:
        url: "http://localhost:{{ deploy_port }}/{{ app_name }}/health"
        return_content: yes
      register: smoke_test
      failed_when: "'OK' not in smoke_test.content"
    
    - name: Switch traffic to new version (update load balancer)
      debug:
        msg: "Switching traffic from port {{ current_port }} to {{ deploy_port }}"
    
    - name: Stop old version
      systemd:
        name: tomcat-old
        state: stopped
      when: current_port != deploy_port
      ignore_errors: yes
    
    - name: Mark deployment successful
      file:
        path: "/var/log/deployments/success-{{ ansible_date_time.epoch }}"
        state: touch
Step 20: Create Canary Deployment Playbook
bashvi /opt/ansible/playbooks/canary-deploy.yml
yaml---
# Canary Deployment - Gradual Rollout
- name: Canary Deployment
  hosts: "{{ target_env }}"
  become: yes
  
  vars:
    canary_percentage: 10
    monitoring_duration: 300  # 5 minutes
    error_threshold: 5  # percentage
  
  tasks:
    - name: Deploy to canary instance
      copy:
        src: "{{ workspace }}/webapp/target/webapp.war"
        dest: "{{ tomcat_home }}/webapps/webapp.war"
      when: inventory_hostname == groups[target_env][0]
    
    - name: Restart canary instance
      systemd:
        name: tomcat
        state: restarted
      when: inventory_hostname == groups[target_env][0]
    
    - name: Wait for canary to stabilize
      wait_for:
        port: 8080
        state: started
        timeout: 60
      when: inventory_hostname == groups[target_env][0]
    
    - name: Monitor canary for {{ monitoring_duration }} seconds
      pause:
        seconds: "{{ monitoring_duration }}"
      when: inventory_hostname == groups[target_env][0]
    
    - name: Check canary error rate
      shell: |
        grep -c "ERROR" {{ tomcat_home }}/logs/catalina.out | tail -100
      register: error_count
      when: inventory_hostname == groups[target_env][0]
    
    - name: Rollback if error rate too high
      include_tasks: /opt/ansible/playbooks/rollback-webapp.yml
      when: 
        - inventory_hostname == groups[target_env][0]
        - error_count.stdout|int > error_threshold
    
    - name: Deploy to remaining instances
      copy:
        src: "{{ workspace }}/webapp/target/webapp.war"
        dest: "{{ tomcat_home }}/webapps/webapp.war"
      when: inventory_hostname != groups[target_env][0]
    
    - name: Rolling restart of remaining instances
      systemd:
        name: tomcat
        state: restarted
      when: inventory_hostname != groups[target_env][0]
      throttle: 1
Step 21: Create Monitoring Integration Playbook
bashvi /opt/ansible/playbooks/setup-monitoring.yml
yaml---
# Setup monitoring agents on deployed servers
- name: Configure Application Monitoring
  hosts: "{{ target_env }}"
  become: yes
  
  tasks:
    - name: Install Node Exporter
      get_url:
        url: https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.linux-amd64.tar.gz
        dest: /tmp/node_exporter.tar.gz
    
    - name: Extract Node Exporter
      unarchive:
        src: /tmp/node_exporter.tar.gz
        dest: /opt/
        remote_src: yes
        creates: /opt/node_exporter-1.7.0.linux-amd64
    
    - name: Create Node Exporter systemd service
      copy:
        dest: /etc/systemd/system/node_exporter.service
        content: |
          [Unit]
          Description=Node Exporter
          After=network.target
          
          [Service]
          Type=simple
          User=root
          ExecStart=/opt/node_exporter-1.7.0.linux-amd64/node_exporter
          
          [Install]
          WantedBy=multi-user.target
    
    - name: Start Node Exporter
      systemd:
        name: node_exporter
        state: started
        enabled: yes
        daemon_reload: yes
    
    - name: Configure Tomcat JMX for Prometheus
      blockinfile:
        path: "{{ tomcat_home }}/bin/setenv.sh"
        create: yes
        block: |
          export CATALINA_OPTS="$CATALINA_OPTS -Dcom.sun.management.jmxremote"
          export CATALINA_OPTS="$CATALINA_OPTS -Dcom.sun.management.jmxremote.port=9090"
          export CATALINA_OPTS="$CATALINA_OPTS -Dcom.sun.management.jmxremote.ssl=false"
          export CATALINA_OPTS="$CATALINA_OPTS -Dcom.sun.management.jmxremote.authenticate=false"
    
    - name: Restart Tomcat to apply JMX config
      systemd:
        name: tomcat
        state: restarted

Part 4: Enhanced Trivy Integration
Step 22: Create Comprehensive Trivy Scan Script
bashvi /opt/trivy/comprehensive-scan.sh
bash#!/bin/bash
# Comprehensive security scanning with Trivy

set -e

WORKSPACE=$1
REPORT_DIR="/opt/trivy/reports"
TIMESTAMP=$(date +%Y%m%d_%H%M%S)
BUILD_ID=${2:-"unknown"}

echo "======================================"
echo "Trivy Comprehensive Security Scan"
echo "Build ID: ${BUILD_ID}"
echo "Timestamp: ${TIMESTAMP}"
echo "======================================"

# Create report directory
mkdir -p ${REPORT_DIR}/{html,json,sarif}

# 1. Scan source code for secrets
echo "
[1/6] Scanning for secrets in source code..."
trivy fs \
  --scanners secret \
  --severity HIGH,CRITICAL \
  --format json \
  --output ${REPORT_DIR}/json/secrets-${TIMESTAMP}.json \
  ${WORKSPACE}

SECRET_COUNT=$(jq '.Results[].Secrets? | length' ${REPORT_DIR}/json/secrets-${TIMESTAMP}.json 2>/dev/null | awk '{s+=$1} END {print s}')
echo "Found ${SECRET_COUNT:-0} secrets"

if [ "${SECRET_COUNT:-0}" -gt 0 ]; then
  echo "ERROR: Secrets found in source code!"
  trivy fs --scanners secret --format table ${WORKSPACE}
  exit 1
fi

# 2. Scan for misconfigurations
echo "
[2/6] Scanning for misconfigurations..."
trivy config \
  --severity HIGH,CRITICAL \
  --format json \
  --output ${REPORT_DIR}/json/config-${TIMESTAMP}.json \
  ${WORKSPACE}

# 3. Scan dependencies (pom.xml)
echo "
[3/6] Scanning Maven dependencies..."
trivy fs \
  --scanners vuln \
  --severity HIGH,CRITICAL \
  --format json \
  --output ${REPORT_DIR}/json/dependencies-${TIMESTAMP}.json \
  --skip-dirs target \
  ${WORKSPACE}

# 4. Scan built artifact
echo "
[4/6] Scanning WAR artifact..."
if [ -f "${WORKSPACE}/webapp/target/webapp.war" ]; then
  TEMP_DIR="/tmp/trivy-war-scan-${TIMESTAMP}"
  mkdir -p ${TEMP_DIR}
  
  cd ${TEMP_DIR}
  unzip -q ${WORKSPACE}/webapp/target/webapp.war
  
  trivy fs \
    --severity HIGH,CRITICAL \
    --format json \
    --output ${REPORT_DIR}/json/artifact-${TIMESTAMP}.json \
    ${TEMP_DIR}
  
  # Generate SARIF for GitHub integration
  trivy fs \
    --severity HIGH,CRITICAL \
    --format sarif \
    --output ${REPORT_DIR}/sarif/artifact-${TIMESTAMP}.sarif \
    ${TEMP_DIR}
  
  rm -rf ${TEMP_DIR}
else
  echo "WARNING: WAR file not found, skipping artifact scan"
fi

# 5. Check for license compliance
echo "
[5/6] Checking license compliance..."
trivy fs \
  --scanners license \
  --severity HIGH,CRITICAL \
  --format json \
  --output ${REPORT_DIR}/json/licenses-${TIMESTAMP}.json \
  ${WORKSPACE}

# 6. Generate consolidated HTML report
echo "
[6/6] Generating consolidated report..."

# Merge all JSON reports
jq -s '{
  "Build": "'${BUILD_ID}'",
  "Timestamp": "'${TIMESTAMP}'",
  "Secrets": .[0],
  "Misconfigurations": .[1],
  "Dependencies": .[2],
  "Artifact": .[3],
  "Licenses": .[4]
}' \
  ${REPORT_DIR}/json/secrets-${TIMESTAMP}.json \
  ${REPORT_DIR}/json/config-${TIMESTAMP}.json \
  ${REPORT_DIR}/json/dependencies-${TIMESTAMP}.json \
  ${REPORT_DIR}/json/artifact-${TIMESTAMP}.json \
  ${REPORT_DIR}/json/licenses-${TIMESTAMP}.json \
  > ${REPORT_DIR}/json/consolidated-${TIMESTAMP}.json

# Generate HTML report
cat > ${REPORT_DIR}/html/report-${TIMESTAMP}.html <<EOF
<!DOCTYPE html>
<html>
<head>
    <title>Trivy Security Report - Build ${BUILD_ID}</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; margin: 0; padding: 20px; background: #f5f5f5; }
        .container { max-width: 1200px; margin: 0 auto; background: white; padding: 30px; border-radius: 8px; box-shadow: 0 2px 4px rgba(0,0,0,0.1); }
        h1 { color: #2c3e50; border-bottom: 3px solid #3498db; padding-bottom: 10px; }
        h2 { color: #34495e; margin-top: 30px; }
        .metric { display: inline-block; margin: 10px 20px 10px 0; padding: 15px 25px; border-radius: 5px; }
        .critical { background: #e74c3c; color: white; }
        .high { background: #e67e22; color: white; }
        .medium { background: #f39c12; color: white; }
        .low { background: #95a5a6; color: white; }
        .pass { background: #27ae60; color: white; }
        table { width: 100%; border-collapse: collapse; margin: 20px 0; }
        th, td { padding: 12px; text-align: left; border-bottom: 1px solid #ddd; }
        th { background: #34495e; color: white; }
        tr:hover { background: #f8f9fa; }
        .timestamp { color: #7f8c8d; font-size: 14px; }
        .summary { background: #ecf0f1; padding: 20px; border-radius: 5px; margin: 20px 0; }
    </style>
</head>
<body>
    <div class="container">
        <h1>🛡️ Trivy Security Scan Report</h1>
        <p class="timestamp">Build: ${BUILD_ID} | Generated: $(date)</p>
        
        <div class="summary">
            <h2>Executive Summary</h2>
            <div class="metric critical">Critical: $(jq '[.Artifact.Results[]?.Vulnerabilities[]? | select(.Severity=="CRITICAL")] | length' ${REPORT_DIR}/json/consolidated-${TIMESTAMP}.json)</div>
            <div class="metric high">High: $(jq '[.Artifact.Results[]?.Vulnerabilities[]? | select(.Severity=="HIGH")] | length' ${REPORT_DIR}/json/consolidated-${TIMESTAMP}.json)</div>
            <div class="metric medium">Medium: $(jq '[.Artifact.Results[]?.Vulnerabilities[]? | select(.Severity=="MEDIUM")] | length' ${REPORT_DIR}/json/consolidated-${TIMESTAMP}.json)</div>
            <div class="metric low">Low: $(jq '[.Artifact.Results[]?.Vulnerabilities[]? | select(.Severity=="LOW")] | length' ${REPORT_DIR}/json/consolidated-${TIMESTAMP}.json)</div>
        </div>
        
        <h2>📊 Scan Details</h2>
        <table>
            <tr>
                <th>Scan Type</th>
                <th>Status</th>
                <th>Findings</th>
            </tr>
            <tr>
                <td>🔐 Secret Scanning</td>
                <td>$([ "${SECRET_COUNT:-0}" -eq 0 ] && echo "✅ Pass" || echo "❌ Fail")</td>
                <td>${SECRET_COUNT:-0} secrets found</td>
            </tr>
            <tr>
                <td>⚙️ Configuration</td>
                <td>✅ Completed</td>
                <td>$(jq '[.Misconfigurations.Results[]?.Misconfigurations[]?] | length' ${REPORT_DIR}/json/consolidated-${TIMESTAMP}.json) issues</td>
            </tr>
            <tr>
                <td>📦 Dependencies</td>
                <td>✅ Completed</td>
                <td>$(jq '[.Dependencies.Results[]?.Vulnerabilities[]?] | length' ${REPORT_DIR}/json/consolidated-${TIMESTAMP}.json) vulnerabilities</td>
            </tr>
            <tr>
                <td>🎯 Artifact</td>
                <td>✅ Completed</td>
                <td>$(jq '[.Artifact.Results[]?.Vulnerabilities[]?] | length' ${REPORT_DIR}/json/consolidated-${TIMESTAMP}.json) vulnerabilities</td>
            </tr>
            <tr>
                <td>⚖️ License</td>
                <td>✅ Completed</td>
                <td>$(jq '[.Licenses.Results[]?.Licenses[]?] | length' ${REPORT_DIR}/json/consolidated-${TIMESTAMP}.json) licenses checked</td>
            </tr>
        </table>
        
        <h2>🔴 Critical Vulnerabilities</h2>
        <div id="critical-vulns">
EOF

# Add critical vulnerabilities to HTML
jq -r '.Artifact.Results[]?.Vulnerabilities[]? | select(.Severity=="CRITICAL") | 
  "<p><strong>" + .VulnerabilityID + "</strong>: " + .Title + 
  " (CVSS: " + (.CVSS.nvd.V3Score // "N/A" | tostring) + ")" +
  "<br>Package: " + .PkgName + " " + .InstalledVersion + 
  " → Fix: " + (.FixedVersion // "No fix available") + "</p>"' \
  ${REPORT_DIR}/json/consolidated-${TIMESTAMP}.json >> ${REPORT_DIR}/html/report-${TIMESTAMP}.html

cat >> ${REPORT_DIR}/html/report-${TIMESTAMP}.html <<EOF
        </div>
        
        <h2>📋 Recommendations</h2>
        <ul>
            <li>Update vulnerable dependencies to fixed versions</li>
            <li>Review and remediate configuration issues</li>
            <li>Implement security headers and best practices</li>
            <li>Schedule regular security scans</li>
            <li>Monitor CVE databases for new vulnerabilities</li>
        </ul>
    </div>
</body>
</html>
EOF

echo "
======================================"
echo "Scan Complete!"
echo "HTML Report: ${REPORT_DIR}/html/report-${TIMESTAMP}.html"
echo "JSON Report: ${REPORT_DIR}/json/consolidated-${TIMESTAMP}.json"
echo "SARIF Report: ${REPORT_DIR}/sarif/artifact-${TIMESTAMP}.sarif"
echo "======================================"

# Calculate totals
CRITICAL=$(jq '[.Artifact.Results[]?.Vulnerabilities[]? | select(.Severity=="CRITICAL")] | length' ${REPORT_DIR}/json/consolidated-${TIMESTAMP}.json)
HIGH=$(jq '[.Artifact.Results[]?.Vulnerabilities[]? | select(.Severity=="HIGH")] | length' ${REPORT_DIR}/json/consolidated-${TIMESTAMP}.json)

echo "
Summary:"
echo "  Critical: ${CRITICAL}"
echo "  High: ${HIGH}"

# Fail build if critical vulnerabilities exceed threshold
if [ "${CRITICAL}" -gt 10 ]; then
  echo "
ERROR: Too many critical vulnerabilities (${CRITICAL})"
  echo "Build failed security scan"
  exit 1
fi

if [ "${HIGH}" -gt 20 ]; then
  echo "
WARNING: High number of HIGH severity vulnerabilities (${HIGH})"
fi

echo "
✅ Security scan passed"
exit 0
bashchmod +x /opt/trivy/comprehensive-scan.sh
Step 23: Create Trivy Database Update Script
bashvi /opt/trivy/update-db.sh
bash#!/bin/bash
# Update Trivy vulnerability database

echo "Updating Trivy vulnerability database..."

trivy image --download-db-only

if [ $? -eq 0 ]; then
  echo "✅ Database updated successfully"
  echo "Last updated: $(date)" > /opt/trivy/.last-update
else
  echo "❌ Database update failed"
  exit 1
fi
bashchmod +x /opt/trivy/update-db.sh
Setup cron job to update daily:
bashsudo crontab -e -u jenkins
```

Add:
```
0 2 * * * /opt/trivy/update-db.sh >> /opt/trivy/logs/db-update.log 2>&1
Step 24: Update Jenkinsfile with Comprehensive Trivy Integration
Replace the Trivy stages in your Jenkinsfile:
groovystage('Update Trivy Database') {
    steps {
        echo "Updating Trivy vulnerability database..."
        sh '/opt/trivy/update-db.sh'
    }
}

stage('Comprehensive Security Scan') {
    steps {
        echo "Running comprehensive security scan with Trivy..."
        script {
            sh """
                /opt/trivy/comprehensive-scan.sh ${WORKSPACE} ${BUILD_ID}
            """
        }
    }
    post {
        always {
            // Archive all reports
            archiveArtifacts artifacts: '/opt/trivy/reports/**/*',
                           fingerprint: true,
                           allowEmptyArchive: true
            
            // Publish HTML report
            publishHTML([
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: '/opt/trivy/reports/html',
                reportFiles: 'report-*.html',
                reportName: 'Trivy Comprehensive Security Report',
                reportTitles: 'Security Scan Results'
            ])
            
            // Publish SARIF report (for GitHub integration)
            recordIssues(
                tools: [sarif(pattern: '/opt/trivy/reports/sarif/*.sarif')],
                qualityGates: [[threshold: 1, type: 'TOTAL', criticality: 'CRITICAL']]
            )
        }
        failure {
            echo "Security scan failed - check reports for details"
        }
    }
}
Step 25: Create Ansible Playbook to Run Trivy on Remote Servers
bashvi /opt/ansible/playbooks/remote-security-scan.yml
yaml---
# Run Trivy scans on deployed applications
- name: Remote Security Scanning
  hosts: "{{ target_env }}"
  become: yes
  
  vars:
    trivy_version: "0.48.0"
    scan_path: "{{ tomcat_home }}/webapps/{{ app_name }}"
    report_path: "/tmp/trivy-remote-scan-{{ ansible_date_time.epoch }}.json"
  
  tasks:
    - name: Check if Trivy is installed
      stat:
        path: /usr/local/bin/trivy
      register: trivy_installed
    
    - name: Install Trivy
      shell: |
        curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin v{{ trivy_version }}
      when: not trivy_installed.stat.exists
    
    - name: Update Trivy database
      command: trivy image --download-db-only
      changed_when: false
    
    - name: Scan deployed application
      shell: |
        trivy rootfs \
          --severity HIGH,CRITICAL \
          --format json \
          --output {{ report_path }} \
          {{ scan_path }}
      register: scan_result
    
    - name: Fetch scan results
      fetch:
        src: "{{ report_path }}"
        dest: "/opt/trivy/reports/remote-{{ inventory_hostname }}-{{ ansible_date_time.epoch }}.json"
        flat: yes
    
    - name: Display scan summary
      shell: |
        trivy rootfs \
          --severity HIGH,CRITICAL \
          --format table \
          {{ scan_path }}
      register: scan_summary
    
    - name: Show results
      debug:
        var: scan_summary.stdout_lines
    
    - name: Cleanup report
      file:
        path: "{{ report_path }}"
        state: absent

Part 5: Testing the Complete Integrated Pipeline
Step 26: Complete Integration Test

Update your repository:

bash   git add .
   git commit -m "Integrated Ansible and Trivy into CI/CD pipeline"
   git push origin main

Verify Ansible playbooks:

bash   # On Jenkins server
   sudo su - jenkins
   cd /opt/ansible
   
   # Test syntax
   ansible-playbook playbooks/deploy-webapp.yml --syntax-check
   ansible-playbook playbooks/health-check.yml --syntax-check
   ansible-playbook playbooks/rollback-webapp.yml --syntax-check

Test Trivy scripts:

bash   # Test database update
   /opt/trivy/update-db.sh
   
   # Test comprehensive scan (will fail without WAR file, but tests script)
   /opt/trivy/comprehensive-scan.sh /tmp test-build

Run the complete pipeline in Jenkins
Verify each stage:

✅ Update Trivy Database
✅ Checkout Code
✅ Comprehensive Security Scan
✅ Maven Build
✅ Checkstyle Analysis
✅ SonarQube Scan
✅ Quality Gate
✅ Nexus Upload
✅ Ansible Deploy to Dev
✅ Dev Health Check
✅ Ansible Deploy to Stage
✅ Stage Health Check
⏸️ Production Approval
✅ Ansible Deploy to Prod
✅ Production Health Check
✅ Remote Security Scan



Step 27: View Reports

In Jenkins Build:

Click on build number
Click "Trivy Comprehensive Security Report"
Review vulnerabilities
Check severity distribution


Check Ansible logs:

In Jenkins console output
Look for detailed Ansible playbook execution
Verify health checks passed


Verify deployments:

bash   # Check each environment
   curl http://<Dev-IP>RetryEContinuebash   # Check each environment
   curl http://<Dev-IP>:8080/webapp/
   curl http://<Stage-IP>:8080/webapp/
   curl http://<Prod-IP>:8080/webapp/

Part 6: Advanced Monitoring and Alerting
Step 28: Create Ansible Playbook for Post-Deployment Monitoring
bashvi /opt/ansible/playbooks/post-deployment-monitoring.yml
yaml---
# Post-deployment monitoring and validation
- name: Post-Deployment Monitoring
  hosts: "{{ target_env }}"
  become: yes
  gather_facts: yes
  
  vars:
    monitoring_duration: 300  # 5 minutes
    check_interval: 30        # 30 seconds
    alert_threshold:
      cpu: 80
      memory: 85
      disk: 90
      error_rate: 5
  
  tasks:
    - name: Create monitoring results directory
      file:
        path: /tmp/monitoring-results
        state: directory
    
    - name: Monitor application for {{ monitoring_duration }} seconds
      shell: |
        END_TIME=$(($(date +%s) + {{ monitoring_duration }}))
        
        while [ $(date +%s) -lt $END_TIME ]; do
          TIMESTAMP=$(date '+%Y-%m-%d %H:%M:%S')
          
          # CPU Usage
          CPU=$(top -bn1 | grep "Cpu(s)" | awk '{print $2}' | cut -d'%' -f1)
          
          # Memory Usage
          MEM=$(free | grep Mem | awk '{print ($3/$2) * 100.0}')
          
          # Disk Usage
          DISK=$(df -h {{ tomcat_home }} | tail -1 | awk '{print $5}' | sed 's/%//')
          
          # Application Response Time
          RESPONSE_TIME=$(curl -o /dev/null -s -w '%{time_total}\n' http://localhost:8080/{{ app_name }}/)
          
          # HTTP Status
          HTTP_STATUS=$(curl -o /dev/null -s -w '%{http_code}\n' http://localhost:8080/{{ app_name }}/)
          
          # Error Count (last minute)
          ERRORS=$(grep -c "ERROR\|Exception" {{ tomcat_home }}/logs/catalina.out 2>/dev/null | tail -100 || echo 0)
          
          # Log metrics
          echo "${TIMESTAMP},${CPU},${MEM},${DISK},${RESPONSE_TIME},${HTTP_STATUS},${ERRORS}" >> /tmp/monitoring-results/metrics.csv
          
          sleep {{ check_interval }}
        done
      register: monitoring_task
      async: 400
      poll: 0
    
    - name: Wait for monitoring to complete
      async_status:
        jid: "{{ monitoring_task.ansible_job_id }}"
      register: job_result
      until: job_result.finished
      retries: 15
      delay: 30
    
    - name: Fetch monitoring results
      fetch:
        src: /tmp/monitoring-results/metrics.csv
        dest: "/opt/ansible/monitoring-results/{{ target_env }}-{{ ansible_hostname }}-{{ ansible_date_time.epoch }}.csv"
        flat: yes
    
    - name: Analyze monitoring results
      shell: |
        # Check for threshold violations
        MAX_CPU=$(awk -F',' '{print $2}' /tmp/monitoring-results/metrics.csv | sort -rn | head -1)
        MAX_MEM=$(awk -F',' '{print $3}' /tmp/monitoring-results/metrics.csv | sort -rn | head -1 | cut -d'.' -f1)
        MAX_DISK=$(awk -F',' '{print $4}' /tmp/monitoring-results/metrics.csv | sort -rn | head -1)
        AVG_RESPONSE=$(awk -F',' '{sum+=$5; count++} END {print sum/count}' /tmp/monitoring-results/metrics.csv)
        ERROR_COUNT=$(awk -F',' '{sum+=$7} END {print sum}' /tmp/monitoring-results/metrics.csv)
        
        echo "Max CPU: ${MAX_CPU}%"
        echo "Max Memory: ${MAX_MEM}%"
        echo "Max Disk: ${MAX_DISK}%"
        echo "Avg Response Time: ${AVG_RESPONSE}s"
        echo "Total Errors: ${ERROR_COUNT}"
        
        # Check thresholds
        if (( $(echo "${MAX_CPU} > {{ alert_threshold.cpu }}" | bc -l) )); then
          echo "ALERT: CPU exceeded threshold"
          exit 1
        fi
        
        if [ "${MAX_MEM}" -gt "{{ alert_threshold.memory }}" ]; then
          echo "ALERT: Memory exceeded threshold"
          exit 1
        fi
        
        if [ "${MAX_DISK}" -gt "{{ alert_threshold.disk }}" ]; then
          echo "ALERT: Disk usage exceeded threshold"
          exit 1
        fi
        
        if [ "${ERROR_COUNT}" -gt "{{ alert_threshold.error_rate }}" ]; then
          echo "WARNING: Error rate elevated"
        fi
      register: analysis_result
    
    - name: Display monitoring summary
      debug:
        var: analysis_result.stdout_lines
    
    - name: Cleanup monitoring data
      file:
        path: /tmp/monitoring-results
        state: absent
Step 29: Create Performance Testing Playbook
bashvi /opt/ansible/playbooks/performance-test.yml
yaml---
# Performance and Load Testing
- name: Performance Testing
  hosts: localhost
  gather_facts: no
  
  vars:
    target_url: "http://{{ target_host }}:8080/{{ app_name }}/"
    concurrent_users: 10
    total_requests: 1000
    ramp_up_time: 60
  
  tasks:
    - name: Install Apache Bench if not present
      package:
        name: httpd-tools
        state: present
      become: yes
    
    - name: Run performance test
      shell: |
        ab -n {{ total_requests }} \
           -c {{ concurrent_users }} \
           -g /tmp/performance-results.tsv \
           {{ target_url }}
      register: perf_test
    
    - name: Display performance results
      debug:
        var: perf_test.stdout_lines
    
    - name: Parse performance metrics
      shell: |
        echo "{{ perf_test.stdout }}" | grep -E "Requests per second|Time per request|Transfer rate"
      register: key_metrics
    
    - name: Show key metrics
      debug:
        var: key_metrics.stdout_lines
    
    - name: Generate performance report
      copy:
        content: |
          Performance Test Report
          ======================
          Target: {{ target_url }}
          Date: {{ ansible_date_time.iso8601 }}
          
          Configuration:
          - Concurrent Users: {{ concurrent_users }}
          - Total Requests: {{ total_requests }}
          
          Results:
          {{ perf_test.stdout }}
        dest: "/opt/ansible/reports/performance-{{ ansible_date_time.epoch }}.txt"
Step 30: Create Automated Rollback Playbook with Decision Logic
bashvi /opt/ansible/playbooks/intelligent-rollback.yml
yaml---
# Intelligent rollback with automated decision making
- name: Intelligent Rollback System
  hosts: "{{ target_env }}"
  become: yes
  serial: 1
  
  vars:
    health_check_retries: 3
    rollback_threshold:
      error_rate: 10        # errors per minute
      response_time: 5      # seconds
      http_errors: 5        # 5xx errors
  
  tasks:
    - name: Check application health
      uri:
        url: "http://localhost:8080/{{ app_name }}/"
        status_code: 200
        timeout: 10
      register: health_check
      failed_when: false
      retries: "{{ health_check_retries }}"
      delay: 5
    
    - name: Analyze error logs
      shell: |
        # Count errors in last 5 minutes
        ERRORS=$(grep -c "ERROR\|SEVERE\|FATAL" {{ tomcat_home }}/logs/catalina.out | tail -500 || echo 0)
        echo $ERRORS
      register: error_count
    
    - name: Check HTTP 5xx errors
      shell: |
        # Check access logs for 5xx errors
        HTTP_ERRORS=$(grep -c " 5[0-9][0-9] " {{ tomcat_home }}/logs/localhost_access_log.*.txt 2>/dev/null | tail -100 || echo 0)
        echo $HTTP_ERRORS
      register: http_error_count
    
    - name: Measure response time
      shell: |
        RESPONSE_TIME=$(curl -o /dev/null -s -w '%{time_total}\n' http://localhost:8080/{{ app_name }}/)
        echo $RESPONSE_TIME
      register: response_time
    
    - name: Decide if rollback needed
      set_fact:
        needs_rollback: >-
          {{
            (health_check.status | default(0) != 200) or
            (error_count.stdout | int > rollback_threshold.error_rate) or
            (http_error_count.stdout | int > rollback_threshold.http_errors) or
            (response_time.stdout | float > rollback_threshold.response_time)
          }}
    
    - name: Display rollback decision
      debug:
        msg: |
          Rollback Decision Analysis:
          - Health Check: {{ health_check.status | default('FAILED') }}
          - Error Count: {{ error_count.stdout }}
          - HTTP 5xx Errors: {{ http_error_count.stdout }}
          - Response Time: {{ response_time.stdout }}s
          - Rollback Needed: {{ needs_rollback }}
    
    - name: Send alert before rollback
      uri:
        url: "{{ slack_webhook_url }}"
        method: POST
        body_format: json
        body:
          text: |
            🚨 ALERT: Automated rollback initiated on {{ inventory_hostname }}
            Environment: {{ target_env }}
            Reason: Health checks failed
            - Error count: {{ error_count.stdout }}
            - HTTP errors: {{ http_error_count.stdout }}
            - Response time: {{ response_time.stdout }}s
      when: needs_rollback | bool
      delegate_to: localhost
      vars:
        slack_webhook_url: "{{ lookup('env', 'SLACK_WEBHOOK_URL') }}"
    
    - name: Execute rollback
      include_tasks: rollback-webapp.yml
      when: needs_rollback | bool
    
    - name: Verify rollback success
      uri:
        url: "http://localhost:8080/{{ app_name }}/"
        status_code: 200
      register: rollback_verify
      when: needs_rollback | bool
      retries: 5
      delay: 10
    
    - name: Send rollback success notification
      debug:
        msg: "Rollback completed successfully on {{ inventory_hostname }}"
      when: 
        - needs_rollback | bool
        - rollback_verify.status == 200
Step 31: Create Trivy Integration with Prometheus
bashvi /opt/trivy/export-metrics.sh
bash#!/bin/bash
# Export Trivy scan results to Prometheus format

REPORT_DIR="/opt/trivy/reports/json"
METRICS_FILE="/opt/trivy/metrics/trivy_metrics.prom"
LATEST_REPORT=$(ls -t ${REPORT_DIR}/consolidated-*.json 2>/dev/null | head -1)

mkdir -p /opt/trivy/metrics

if [ ! -f "${LATEST_REPORT}" ]; then
  echo "No Trivy reports found"
  exit 1
fi

# Extract metrics
CRITICAL=$(jq '[.Artifact.Results[]?.Vulnerabilities[]? | select(.Severity=="CRITICAL")] | length' ${LATEST_REPORT})
HIGH=$(jq '[.Artifact.Results[]?.Vulnerabilities[]? | select(.Severity=="HIGH")] | length' ${LATEST_REPORT})
MEDIUM=$(jq '[.Artifact.Results[]?.Vulnerabilities[]? | select(.Severity=="MEDIUM")] | length' ${LATEST_REPORT})
LOW=$(jq '[.Artifact.Results[]?.Vulnerabilities[]? | select(.Severity=="LOW")] | length' ${LATEST_REPORT})
SECRETS=$(jq '[.Secrets.Results[]?.Secrets[]?] | length' ${LATEST_REPORT})

# Generate Prometheus metrics
cat > ${METRICS_FILE} <<EOF
# HELP trivy_vulnerabilities_critical Number of critical vulnerabilities
# TYPE trivy_vulnerabilities_critical gauge
trivy_vulnerabilities_critical ${CRITICAL}

# HELP trivy_vulnerabilities_high Number of high severity vulnerabilities
# TYPE trivy_vulnerabilities_high gauge
trivy_vulnerabilities_high ${HIGH}

# HELP trivy_vulnerabilities_medium Number of medium severity vulnerabilities
# TYPE trivy_vulnerabilities_medium gauge
trivy_vulnerabilities_medium ${MEDIUM}

# HELP trivy_vulnerabilities_low Number of low severity vulnerabilities
# TYPE trivy_vulnerabilities_low gauge
trivy_vulnerabilities_low ${LOW}

# HELP trivy_secrets_detected Number of secrets detected
# TYPE trivy_secrets_detected gauge
trivy_secrets_detected ${SECRETS}

# HELP trivy_last_scan_timestamp Last scan timestamp
# TYPE trivy_last_scan_timestamp gauge
trivy_last_scan_timestamp $(date +%s)
EOF

echo "Metrics exported to ${METRICS_FILE}"
bashchmod +x /opt/trivy/export-metrics.sh
Create metrics endpoint:
bashsudo yum install nginx -y

sudo vi /etc/nginx/conf.d/trivy-metrics.conf
nginxserver {
    listen 9101;
    server_name _;
    
    location /metrics {
        root /opt/trivy;
        default_type text/plain;
        try_files /metrics/trivy_metrics.prom =404;
    }
}
bashsudo systemctl restart nginx
sudo systemctl enable nginx
Step 32: Update Prometheus to Scrape Trivy Metrics
On Prometheus server:
bashssh -i your-key.pem ubuntu@<Prometheus-Public-IP>

sudo vi /etc/prometheus/prometheus.yml
Add new job:
yaml  - job_name: 'trivy_security'
    static_configs:
      - targets: ['<Jenkins-Private-IP>:9101']
        labels:
          service: 'security_scan'
bashsudo systemctl restart prometheus
Step 33: Create Grafana Dashboard for Security Metrics

Access Grafana: http://<Grafana-Public-IP>:3000
Create new dashboard:

Click + → Dashboard → Add new panel


Add Trivy Vulnerabilities Panel:

Query: trivy_vulnerabilities_critical
Visualization: Stat
Title: "Critical Vulnerabilities"
Color: Red


Add more panels:

promql   # High Vulnerabilities
   trivy_vulnerabilities_high
   
   # Total Vulnerabilities
   sum(trivy_vulnerabilities_critical + trivy_vulnerabilities_high + trivy_vulnerabilities_medium)
   
   # Vulnerability Trend
   rate(trivy_vulnerabilities_critical[1h])

Save dashboard as "Security Metrics"


Part 7: Complete Pipeline Documentation
Step 34: Create Complete Pipeline Documentation
bash# On your local machine
cd Jenkins-CICD-Project

vi CICD-PIPELINE-DOCUMENTATION.md
markdown# Complete CI/CD Pipeline Documentation

## Architecture Overview
```
Developer → GitHub → Jenkins → Build → Test → Scan → Deploy
                ↓         ↓       ↓      ↓       ↓
              Webhook  Maven  SonarQube Trivy  Ansible
                              Checkstyle        ↓
                                             Dev → Stage → Prod
                                             ↓      ↓       ↓
                                          Tomcat Tomcat Tomcat
                                             ↓      ↓       ↓
                                          Monitor Monitor Monitor
                                             ↓      ↓       ↓
                                          Prometheus + Grafana
                                             ↓
                                          Splunk (Logs)
```

## Pipeline Stages

### 1. Source Control Management
- **Tool**: GitHub
- **Trigger**: Webhook on push
- **Branch**: main

### 2. Trivy Database Update
- Updates vulnerability database
- Ensures latest CVE information
- Runs: Every build

### 3. Comprehensive Security Scan
- **Scans**:
  - Secrets detection
  - Configuration issues
  - Dependency vulnerabilities
  - License compliance
- **Reports**: HTML, JSON, SARIF
- **Threshold**: Fails on >10 CRITICAL

### 4. Build
- **Tool**: Maven 3.x
- **Command**: `mvn clean install`
- **Output**: webapp.war

### 5. Unit Tests
- **Framework**: JUnit
- **Coverage**: Jacoco
- **Reports**: target/surefire-reports

### 6. Code Quality Analysis
- **Checkstyle**: Java coding standards
- **SonarQube**: Code smells, bugs, vulnerabilities
- **Quality Gate**: Blocks on >10 bugs

### 7. Artifact Management
- **Tool**: Nexus Repository
- **Version**: Build ID + Timestamp
- **Repository**: maven-project-releases

### 8. Deployment (Ansible)

#### Dev Environment
- **Method**: Ansible playbook
- **Playbook**: deploy-webapp.yml
- **Health Check**: Automated
- **Rollback**: Automatic on failure

#### Stage Environment
- **Method**: Ansible playbook
- **Smoke Tests**: Automated
- **Performance Test**: Optional

#### Production Environment
- **Approval**: Manual (timeout: 1 hour)
- **Method**: Ansible playbook
- **Strategy**: Blue-Green or Canary
- **Monitoring**: 5-minute observation
- **Rollback**: Automated on health check failure

### 9. Post-Deployment
- Health checks on all environments
- Performance monitoring
- Log aggregation (Splunk)
- Metrics collection (Prometheus)
- Alerts (Slack)

## Security Features

### Trivy Scanning
```bash
# Filesystem scan
trivy fs --severity HIGH,CRITICAL .

# Dependency scan
trivy fs --scanners vuln .

# Secret detection
trivy fs --scanners secret .

# Artifact scan
trivy fs webapp.war
```

### Quality Gates
- SonarQube: Max 10 bugs
- Trivy: Max 10 critical vulnerabilities
- Code Coverage: Min 80%
- Checkstyle: Max 100 violations

## Ansible Playbooks

### deploy-webapp.yml
```yaml
Purpose: Deploy application to target environment
Steps:
  1. Backup existing application
  2. Stop Tomcat
  3. Remove old WAR
  4. Copy new WAR
  5. Start Tomcat
  6. Health check
  7. Cleanup old backups
```

### rollback-webapp.yml
```yaml
Purpose: Rollback to previous version
Steps:
  1. Identify latest backup
  2. Stop Tomcat
  3. Restore backup
  4. Start Tomcat
  5. Verify health
```

### health-check.yml
```yaml
Purpose: Validate deployment
Checks:
  - Tomcat service status
  - Port 8080 listening
  - HTTP 200 response
  - Disk space usage
```

### intelligent-rollback.yml
```yaml
Purpose: Automated rollback on failure
Thresholds:
  - Error rate: 10/minute
  - Response time: >5 seconds
  - HTTP 5xx errors: >5
  - Health check failures
```

## Monitoring & Alerting

### Prometheus Metrics
- Node Exporter (system metrics)
- JMX Exporter (Tomcat metrics)
- Trivy security metrics
- Custom application metrics

### Grafana Dashboards
1. Infrastructure Overview
2. Application Performance
3. Security Metrics
4. Deployment History

### Splunk Logs
- Application logs: /var/log/tomcat/
- Indexed by: host, environment
- Retention: 30 days
- Search: index=* source="/var/log/tomcat/*"

### Slack Notifications
- Build started
- Build succeeded/failed
- Each stage completion
- Security scan results
- Deployment status
- Rollback alerts

## Rollback Procedures

### Manual Rollback
```bash
ansible-playbook /opt/ansible/playbooks/rollback-webapp.yml \
  -i /opt/ansible/inventory/hosts \
  -e "target_env=prod"
```

### Automated Rollback Triggers
- Health check fails (3 retries)
- Error rate >10/min
- Response time >5s
- HTTP 5xx errors >5

## Troubleshooting

### Pipeline Fails at Security Scan
```bash
# Check Trivy reports
cat /opt/trivy/reports/json/consolidated-*.json | jq

# Update Trivy database
/opt/trivy/update-db.sh

# Re-run scan
/opt/trivy/comprehensive-scan.sh ${WORKSPACE} ${BUILD_ID}
```

### Deployment Fails
```bash
# Check Ansible logs
cat /var/lib/jenkins/jobs/*/builds/*/log

# Test connectivity
ansible all -i /opt/ansible/inventory/hosts -m ping

# Check Tomcat status
ssh ansibleadmin@ sudo systemctl status tomcat
```

### Health Check Fails
```bash
# Check application logs
ssh ansibleadmin@ sudo tail -f /var/log/tomcat/catalina.out

# Check disk space
ansible  -i /opt/ansible/inventory/hosts -a "df -h"

# Manual health check
curl http://:8080/webapp/
```

## Environment Variables
```bash
WORKSPACE              # Jenkins workspace path
BUILD_ID              # Jenkins build number
BUILD_TIMESTAMP       # Build timestamp
NEXUS_CREDENTIAL_ID   # Nexus credentials
SLACK_WEBHOOK_URL     # Slack webhook for notifications
```

## File Locations
```
Jenkins Server:
/var/lib/jenkins/workspace/          - Build workspace
/opt/ansible/playbooks/              - Ansible playbooks
/opt/ansible/inventory/              - Inventory files
/opt/trivy/reports/                  - Trivy scan reports
/opt/trivy/metrics/                  - Prometheus metrics

Application Servers:
/opt/apache-tomcat-8.5.82/           - Tomcat installation
/opt/apache-tomcat-8.5.82/webapps/   - Deployed applications
/var/log/tomcat/                     - Application logs
/opt/apache-tomcat-8.5.82/backup/    - Application backups
```

## Performance Benchmarks
```
Build Time: ~5 minutes
Security Scan: ~2 minutes
Deployment: ~30 seconds per environment
Health Check: ~1 minute
Total Pipeline: ~15 minutes (excluding approval)
```

## Success Criteria

✅ All unit tests pass (100%)
✅ Code coverage >80%
✅ Checkstyle violations <100
✅ SonarQube quality gate passes
✅ Zero secrets detected
✅ Critical vulnerabilities <10
✅ All deployments succeed
✅ All health checks pass
✅ Zero rollbacks
✅ Slack notifications sent

## Contacts

- DevOps Team: devops@company.com
- Security Team: security@company.com
- On-Call: oncall@company.com
Step 35: Create Quick Reference Guide
bashvi QUICK-REFERENCE.md
markdown# CI/CD Pipeline Quick Reference

## Common Commands

### Jenkins
```bash
# Trigger build
curl -X POST http://:8080/job/jenkins-complete-cicd-pipeline/build \
  --user admin:admin

# Check build status
curl http://:8080/job/jenkins-complete-cicd-pipeline/lastBuild/api/json
```

### Ansible
```bash
# Deploy to Dev
ansible-playbook /opt/ansible/playbooks/deploy-webapp.yml \
  -i /opt/ansible/inventory/hosts \
  -e "target_env=dev" \
  -e "workspace=/var/lib/jenkins/workspace/jenkins-complete-cicd-pipeline"

# Health check
ansible-playbook /opt/ansible/playbooks/health-check.yml \
  -i /opt/ansible/inventory/hosts \
  -e "target_env=prod"

# Rollback
ansible-playbook /opt/ansible/playbooks/rollback-webapp.yml \
  -i /opt/ansible/inventory/hosts \
  -e "target_env=prod"

# Remote security scan
ansible-playbook /opt/ansible/playbooks/remote-security-scan.yml \
  -i /opt/ansible/inventory/hosts \
  -e "target_env=prod"
```

### Trivy
```bash
# Update database
/opt/trivy/update-db.sh

# Comprehensive scan
/opt/trivy/comprehensive-scan.sh /path/to/code build-123

# Export metrics
/opt/trivy/export-metrics.sh
```

### Application Access
```
Dev:   http://<dev-ip>:8080/webapp/
Stage: http://<stage-ip>:8080/webapp/
Prod:  http://<prod-ip>:8080/webapp/
```

### Monitoring
```
Jenkins:    http://<jenkins-ip>:8080
SonarQube:  http://<sonarqube-ip>:9000
Nexus:      http://<nexus-ip>:8081
Prometheus: http://<prometheus-ip>:9090
Grafana:    http://<grafana-ip>:3000
Splunk:     http://<splunk-ip>:8000
```

## Emergency Procedures

### Stop All Deployments
```bash
# Cancel running Jenkins job
curl -X POST http://:8080/job/jenkins-complete-cicd-pipeline//stop \
  --user admin:admin
```

### Emergency Rollback
```bash
ansible-playbook /opt/ansible/playbooks/rollback-webapp.yml \
  -i /opt/ansible/inventory/hosts \
  -e "target_env=prod" \
  -vv
```

### Check System Health
```bash
# All systems
ansible all -i /opt/ansible/inventory/hosts -m ping

# Check services
ansible all -i /opt/ansible/inventory/hosts -a "systemctl status tomcat"

# Check disk space
ansible all -i /opt/ansible/inventory/hosts -a "df -h"
```

## Log Locations
```
Jenkins:     /var/lib/jenkins/logs/jenkins.log
Tomcat:      /var/log/tomcat/catalina.out
Ansible:     /var/log/ansible.log
Trivy:       /opt/trivy/logs/
```

Part 8: Final Testing and Validation
Step 36: Complete End-to-End Test
bash# On your local machine
cd Jenkins-CICD-Project

# Add all documentation
git add .
git commit -m "Complete integration: Ansible + Trivy + comprehensive documentation"
git push origin main
Step 37: Execute Full Pipeline Test

Watch the pipeline execute all stages
Verify each component:

bash# Check Trivy reports
ssh -i your-key.pem ec2-user@<Jenkins-IP>
ls -lh /opt/trivy/reports/html/

# Check Ansible logs
tail -f /var/lib/jenkins/jobs/jenkins-complete-cicd-pipeline/builds/lastSuccessfulBuild/log

# Verify deployments
for ENV in dev stage prod; do
  IP=$(aws ec2 describe-instances \
    --filters "Name=tag:Name,Values=${ENV^}-Env" "Name=instance-state-name,Values=running" \
    --query 'Reservations[0].Instances[0].PublicIpAddress' \
    --output text)
  echo "Testing $ENV environment..."
  curl -I http://$IP:8080/webapp/
done
Step 38: Verify Monitoring Stack
bash# Check Prometheus targets
curl -s http://<Prometheus-IP>:9090/api/v1/targets | jq '.data.activeTargets[] | {job: .labels.job, health: .health}'

# Check Trivy metrics
curl http://<Jenkins-IP>:9101/metrics

# Query Grafana
curl -H "Authorization: Bearer <api-token>" \
  http://<Grafana-IP>:3000/api/search?query=Security
```

---

## **🎉 Congratulations! Complete Integration Achieved**

### **What You've Built:**
```
┌─────────────────────────────────────────────────────────────┐
│                     COMPLETE CI/CD PIPELINE                  │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  GitHub → Webhook → Jenkins                                 │
│     ↓                                                        │
│  Security Scan (Trivy)                                      │
│     ↓                                                        │
│  Build (Maven) → Test → Quality (SonarQube)                │
│     ↓                                                        │
│  Artifact Storage (Nexus)                                   │
│     ↓                                                        │
│  Deployment (Ansible)                                       │
│     ├→ Dev Environment                                      │
│     ├→ Stage Environment                                    │
│     └→ Production Environment (with approval)               │
│         ↓                                                    │
│  Health Checks & Monitoring                                 │
│     ├→ Prometheus (Metrics)                                 │
│     ├→ Grafana (Visualization)                             │
│     ├→ Splunk (Logs)                                        │
│     └→ Slack (Notifications)                                │
│         ↓                                                    │
│  Automated Rollback (on failure)                            │
│                                                              │
└─────────────────────────────────────────────────────────────┘
Key Features Implemented:
✅ Automated Security Scanning with Trivy

Filesystem scanning
Dependency vulnerability detection
Secret detection
Configuration scanning
License compliance
SARIF reports for GitHub integration

✅ Infrastructure as Code with Ansible

Idempotent deployments
Health checks
Automated rollbacks
Blue-green deployment support
Canary deployment capability
Performance testing
Post-deployment monitoring

✅ Complete Monitoring Stack

System metrics (Node Exporter)
Application metrics (JMX)
Security metrics (Trivy)
Log aggregation (Splunk)
Visualization (Grafana)
Real-time alerts (Slack + Prometheus)

✅ Quality Gates

SonarQube code analysis
Trivy security thresholds
Automated testing
Code coverage requirements

✅ Artifact Management

Versioned artifacts in Nexus
Automated backup retention
Rollback capabilities

Interview Talking Points:

"Integrated Trivy for comprehensive security scanning"

Scans code, dependencies, and artifacts
Exports metrics to Prometheus
Blocks deployment on critical vulnerabilities
Generates multiple report formats


"Implemented Ansible for zero-downtime deployments"

Automated deployment across multiple environments
Health checks and automated rollbacks
Blue-green and canary deployment strategies
Infrastructure monitoring and alerting


"Built end-to-end observability"

Metrics


RetryEContinue
Metrics collection with Prometheus

Centralized logging with Splunk
Real-time visualization with Grafana
Proactive alerting via Slack




"Achieved complete pipeline automation"

Zero manual intervention for Dev/Stage
Approval-based production deployments
Automated security compliance checks
Self-healing with intelligent rollbacks


"Implemented security-first DevOps practices"

Shift-left security with early scanning
Vulnerability management and tracking
Secret detection and prevention
Compliance reporting (SARIF, JSON, HTML)




Part 9: Advanced Features and Optimization
Step 39: Create Pipeline Performance Metrics
bashvi /opt/ansible/playbooks/pipeline-metrics.yml
yaml---
# Collect and report pipeline performance metrics
- name: Pipeline Performance Metrics
  hosts: localhost
  gather_facts: no
  
  vars:
    jenkins_url: "http://{{ jenkins_host }}:8080"
    job_name: "jenkins-complete-cicd-pipeline"
    metrics_file: "/opt/ansible/metrics/pipeline-performance.json"
  
  tasks:
    - name: Get last 10 builds information
      uri:
        url: "{{ jenkins_url }}/job/{{ job_name }}/api/json?tree=builds[number,duration,result,timestamp]{0,10}"
        user: admin
        password: admin
        force_basic_auth: yes
      register: builds_info
    
    - name: Calculate average build time
      set_fact:
        avg_duration: "{{ (builds_info.json.builds | map(attribute='duration') | list | map('int') | sum / builds_info.json.builds | length / 1000 / 60) | round(2) }}"
        success_rate: "{{ ((builds_info.json.builds | selectattr('result', 'equalto', 'SUCCESS') | list | length) / (builds_info.json.builds | length) * 100) | round(2) }}"
    
    - name: Generate metrics report
      copy:
        content: |
          {
            "timestamp": "{{ ansible_date_time.iso8601 }}",
            "pipeline_name": "{{ job_name }}",
            "metrics": {
              "average_build_time_minutes": {{ avg_duration }},
              "success_rate_percent": {{ success_rate }},
              "total_builds_analyzed": {{ builds_info.json.builds | length }},
              "last_build_number": {{ builds_info.json.builds[0].number }},
              "last_build_result": "{{ builds_info.json.builds[0].result }}",
              "last_build_duration_minutes": {{ (builds_info.json.builds[0].duration / 1000 / 60) | round(2) }}
            }
          }
        dest: "{{ metrics_file }}"
    
    - name: Display metrics summary
      debug:
        msg:
          - "Average Build Time: {{ avg_duration }} minutes"
          - "Success Rate: {{ success_rate }}%"
          - "Total Builds Analyzed: {{ builds_info.json.builds | length }}"
Step 40: Create Automated Testing Suite
bashvi /opt/ansible/playbooks/integration-tests.yml
yaml---
# Automated integration testing suite
- name: Integration Testing Suite
  hosts: "{{ target_env }}"
  become: no
  
  vars:
    app_url: "http://{{ inventory_hostname }}:8080/{{ app_name }}"
    test_results_dir: "/tmp/test-results"
  
  tasks:
    - name: Create test results directory
      file:
        path: "{{ test_results_dir }}"
        state: directory
      delegate_to: localhost
    
    - name: Test 1 - Application Homepage
      uri:
        url: "{{ app_url }}/"
        return_content: yes
        status_code: 200
      register: homepage_test
      failed_when: false
    
    - name: Test 2 - API Health Endpoint
      uri:
        url: "{{ app_url }}/api/health"
        return_content: yes
        status_code: 200
      register: health_test
      failed_when: false
      ignore_errors: yes
    
    - name: Test 3 - Response Time Check
      shell: |
        for i in {1..5}; do
          curl -o /dev/null -s -w '%{time_total}\n' {{ app_url }}/
        done | awk '{sum+=$1; count++} END {print sum/count}'
      register: response_time
      delegate_to: localhost
    
    - name: Test 4 - Load Test (Concurrent Requests)
      shell: |
        seq 1 10 | xargs -I {} -P 10 curl -s -o /dev/null -w '%{http_code}\n' {{ app_url }}/
      register: load_test
      delegate_to: localhost
    
    - name: Test 5 - Memory Leak Check
      shell: |
        # Get initial memory
        INITIAL=$(free -m | grep Mem | awk '{print $3}')
        
        # Generate load
        for i in {1..100}; do
          curl -s {{ app_url }}/ > /dev/null
        done
        
        # Get final memory
        FINAL=$(free -m | grep Mem | awk '{print $3}')
        
        # Calculate difference
        echo "Memory increase: $((FINAL - INITIAL)) MB"
      register: memory_test
    
    - name: Generate test report
      copy:
        content: |
          Integration Test Report
          =======================
          Environment: {{ target_env }}
          Host: {{ inventory_hostname }}
          Timestamp: {{ ansible_date_time.iso8601 }}
          
          Test Results:
          -------------
          1. Homepage Test: {{ 'PASS' if homepage_test.status == 200 else 'FAIL' }}
             Status Code: {{ homepage_test.status | default('N/A') }}
          
          2. Health Endpoint: {{ 'PASS' if health_test.status == 200 else 'FAIL' }}
             Status Code: {{ health_test.status | default('N/A') }}
          
          3. Average Response Time: {{ response_time.stdout }} seconds
             Status: {{ 'PASS' if (response_time.stdout | float) < 2 else 'FAIL' }}
          
          4. Load Test (10 concurrent): 
             Results: {{ load_test.stdout_lines | join(', ') }}
             Status: {{ 'PASS' if '200' in load_test.stdout else 'FAIL' }}
          
          5. Memory Leak Check:
             {{ memory_test.stdout }}
             Status: {{ 'PASS' if 'increase: 0' in memory_test.stdout or 'increase: 1' in memory_test.stdout else 'WARNING' }}
          
          Overall Status: {{ 'PASS' if (homepage_test.status == 200 and (response_time.stdout | float) < 2) else 'FAIL' }}
        dest: "{{ test_results_dir }}/integration-test-{{ target_env }}-{{ ansible_date_time.epoch }}.txt"
      delegate_to: localhost
    
    - name: Fail if critical tests failed
      fail:
        msg: "Critical integration tests failed"
      when: homepage_test.status != 200 or (response_time.stdout | float) > 5
Step 41: Create Security Compliance Report Generator
bashvi /opt/trivy/generate-compliance-report.sh
bash#!/bin/bash
# Generate comprehensive security compliance report

set -e

REPORT_DIR="/opt/trivy/reports"
COMPLIANCE_DIR="${REPORT_DIR}/compliance"
TIMESTAMP=$(date +%Y%m%d_%H%M%S)
BUILD_ID=${1:-"latest"}

mkdir -p ${COMPLIANCE_DIR}

echo "Generating Security Compliance Report..."

# Find latest scan results
LATEST_SCAN=$(ls -t ${REPORT_DIR}/json/consolidated-*.json 2>/dev/null | head -1)

if [ ! -f "${LATEST_SCAN}" ]; then
  echo "ERROR: No scan results found"
  exit 1
fi

# Extract compliance metrics
TOTAL_VULNS=$(jq '[.Artifact.Results[]?.Vulnerabilities[]?] | length' ${LATEST_SCAN})
CRITICAL_VULNS=$(jq '[.Artifact.Results[]?.Vulnerabilities[]? | select(.Severity=="CRITICAL")] | length' ${LATEST_SCAN})
HIGH_VULNS=$(jq '[.Artifact.Results[]?.Vulnerabilities[]? | select(.Severity=="HIGH")] | length' ${LATEST_SCAN})
SECRETS_FOUND=$(jq '[.Secrets.Results[]?.Secrets[]?] | length' ${LATEST_SCAN})
CONFIG_ISSUES=$(jq '[.Misconfigurations.Results[]?.Misconfigurations[]?] | length' ${LATEST_SCAN})

# Calculate compliance score (0-100)
COMPLIANCE_SCORE=100

# Deduct points for findings
if [ ${CRITICAL_VULNS} -gt 0 ]; then
  COMPLIANCE_SCORE=$((COMPLIANCE_SCORE - (CRITICAL_VULNS * 5)))
fi

if [ ${HIGH_VULNS} -gt 0 ]; then
  COMPLIANCE_SCORE=$((COMPLIANCE_SCORE - (HIGH_VULNS * 2)))
fi

if [ ${SECRETS_FOUND} -gt 0 ]; then
  COMPLIANCE_SCORE=$((COMPLIANCE_SCORE - (SECRETS_FOUND * 10)))
fi

if [ ${CONFIG_ISSUES} -gt 0 ]; then
  COMPLIANCE_SCORE=$((COMPLIANCE_SCORE - (CONFIG_ISSUES * 1)))
fi

# Ensure score doesn't go negative
if [ ${COMPLIANCE_SCORE} -lt 0 ]; then
  COMPLIANCE_SCORE=0
fi

# Determine compliance level
if [ ${COMPLIANCE_SCORE} -ge 90 ]; then
  COMPLIANCE_LEVEL="EXCELLENT"
  LEVEL_COLOR="green"
elif [ ${COMPLIANCE_SCORE} -ge 75 ]; then
  COMPLIANCE_LEVEL="GOOD"
  LEVEL_COLOR="lightgreen"
elif [ ${COMPLIANCE_SCORE} -ge 60 ]; then
  COMPLIANCE_LEVEL="ACCEPTABLE"
  LEVEL_COLOR="orange"
else
  COMPLIANCE_LEVEL="NEEDS IMPROVEMENT"
  LEVEL_COLOR="red"
fi

# Generate HTML compliance report
cat > ${COMPLIANCE_DIR}/compliance-report-${TIMESTAMP}.html <<EOF
<!DOCTYPE html>
<html>
<head>
    <title>Security Compliance Report</title>
    <style>
        body { 
            font-family: Arial, sans-serif; 
            margin: 40px; 
            background: #f5f5f5; 
        }
        .container { 
            max-width: 1000px; 
            margin: 0 auto; 
            background: white; 
            padding: 30px; 
            border-radius: 10px; 
            box-shadow: 0 2px 10px rgba(0,0,0,0.1); 
        }
        h1 { 
            color: #2c3e50; 
            border-bottom: 3px solid #3498db; 
            padding-bottom: 10px; 
        }
        .score-container {
            text-align: center;
            padding: 30px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 10px;
            color: white;
            margin: 20px 0;
        }
        .score {
            font-size: 72px;
            font-weight: bold;
            margin: 20px 0;
        }
        .level {
            font-size: 24px;
            padding: 10px 20px;
            background: rgba(255,255,255,0.2);
            border-radius: 5px;
            display: inline-block;
        }
        .metrics {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin: 30px 0;
        }
        .metric-card {
            padding: 20px;
            border-radius: 8px;
            text-align: center;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .metric-value {
            font-size: 36px;
            font-weight: bold;
            margin: 10px 0;
        }
        .metric-label {
            font-size: 14px;
            color: #7f8c8d;
            text-transform: uppercase;
        }
        .critical { background: #e74c3c; color: white; }
        .high { background: #e67e22; color: white; }
        .medium { background: #f39c12; color: white; }
        .info { background: #3498db; color: white; }
        .recommendations {
            background: #ecf0f1;
            padding: 20px;
            border-radius: 8px;
            margin: 20px 0;
        }
        .recommendation {
            padding: 10px;
            margin: 10px 0;
            background: white;
            border-left: 4px solid #3498db;
            padding-left: 15px;
        }
        .footer {
            text-align: center;
            margin-top: 30px;
            padding-top: 20px;
            border-top: 1px solid #ddd;
            color: #7f8c8d;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
        }
        th, td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }
        th {
            background: #34495e;
            color: white;
        }
        tr:hover {
            background: #f8f9fa;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🛡️ Security Compliance Report</h1>
        <p style="color: #7f8c8d;">Build: ${BUILD_ID} | Generated: $(date '+%Y-%m-%d %H:%M:%S')</p>
        
        <div class="score-container">
            <div class="score">${COMPLIANCE_SCORE}</div>
            <div class="level">${COMPLIANCE_LEVEL}</div>
            <p style="margin-top: 20px; font-size: 16px;">Compliance Score (0-100)</p>
        </div>
        
        <h2>📊 Security Metrics</h2>
        <div class="metrics">
            <div class="metric-card critical">
                <div class="metric-value">${CRITICAL_VULNS}</div>
                <div class="metric-label">Critical Vulnerabilities</div>
            </div>
            <div class="metric-card high">
                <div class="metric-value">${HIGH_VULNS}</div>
                <div class="metric-label">High Vulnerabilities</div>
            </div>
            <div class="metric-card medium">
                <div class="metric-value">${SECRETS_FOUND}</div>
                <div class="metric-label">Secrets Detected</div>
            </div>
            <div class="metric-card info">
                <div class="metric-value">${CONFIG_ISSUES}</div>
                <div class="metric-label">Configuration Issues</div>
            </div>
        </div>
        
        <h2>📋 Compliance Standards</h2>
        <table>
            <tr>
                <th>Standard</th>
                <th>Requirement</th>
                <th>Status</th>
            </tr>
            <tr>
                <td>OWASP Top 10</td>
                <td>No critical vulnerabilities</td>
                <td style="color: $([ ${CRITICAL_VULNS} -eq 0 ] && echo 'green' || echo 'red');">
                    $([ ${CRITICAL_VULNS} -eq 0 ] && echo '✅ PASS' || echo '❌ FAIL')
                </td>
            </tr>
            <tr>
                <td>CIS Benchmarks</td>
                <td>Secure configuration</td>
                <td style="color: $([ ${CONFIG_ISSUES} -lt 5 ] && echo 'green' || echo 'orange');">
                    $([ ${CONFIG_ISSUES} -lt 5 ] && echo '✅ PASS' || echo '⚠️ WARNING')
                </td>
            </tr>
            <tr>
                <td>Secret Management</td>
                <td>No hardcoded secrets</td>
                <td style="color: $([ ${SECRETS_FOUND} -eq 0 ] && echo 'green' || echo 'red');">
                    $([ ${SECRETS_FOUND} -eq 0 ] && echo '✅ PASS' || echo '❌ FAIL')
                </td>
            </tr>
            <tr>
                <td>Dependency Management</td>
                <td>Up-to-date dependencies</td>
                <td style="color: $([ ${HIGH_VULNS} -lt 10 ] && echo 'green' || echo 'orange');">
                    $([ ${HIGH_VULNS} -lt 10 ] && echo '✅ PASS' || echo '⚠️ WARNING')
                </td>
            </tr>
        </table>
        
        <div class="recommendations">
            <h2>🎯 Recommendations</h2>
EOF

# Add specific recommendations based on findings
if [ ${CRITICAL_VULNS} -gt 0 ]; then
cat >> ${COMPLIANCE_DIR}/compliance-report-${TIMESTAMP}.html <<EOF
            <div class="recommendation">
                <strong>HIGH PRIORITY:</strong> ${CRITICAL_VULNS} critical vulnerabilities detected. 
                Update affected packages immediately.
            </div>
EOF
fi

if [ ${SECRETS_FOUND} -gt 0 ]; then
cat >> ${COMPLIANCE_DIR}/compliance-report-${TIMESTAMP}.html <<EOF
            <div class="recommendation">
                <strong>URGENT:</strong> ${SECRETS_FOUND} secrets found in code. 
                Remove hardcoded credentials and use secret management tools.
            </div>
EOF
fi

if [ ${HIGH_VULNS} -gt 20 ]; then
cat >> ${COMPLIANCE_DIR}/compliance-report-${TIMESTAMP}.html <<EOF
            <div class="recommendation">
                <strong>IMPORTANT:</strong> High number of HIGH severity vulnerabilities (${HIGH_VULNS}). 
                Schedule dependency updates.
            </div>
EOF
fi

cat >> ${COMPLIANCE_DIR}/compliance-report-${TIMESTAMP}.html <<EOF
            <div class="recommendation">
                Implement regular security scanning in CI/CD pipeline
            </div>
            <div class="recommendation">
                Conduct periodic security training for development team
            </div>
            <div class="recommendation">
                Establish vulnerability management process with SLAs
            </div>
            <div class="recommendation">
                Enable automated dependency updates with Dependabot or Renovate
            </div>
        </div>
        
        <h2>📈 Trend Analysis</h2>
        <p>Compare with previous scans to track improvement over time.</p>
        
        <div class="footer">
            <p>Generated by Trivy Security Scanner</p>
            <p>For questions, contact: security@company.com</p>
        </div>
    </div>
</body>
</html>
EOF

# Generate JSON summary for metrics
cat > ${COMPLIANCE_DIR}/compliance-summary-${TIMESTAMP}.json <<EOF
{
  "timestamp": "$(date -u +%Y-%m-%dT%H:%M:%SZ)",
  "build_id": "${BUILD_ID}",
  "compliance_score": ${COMPLIANCE_SCORE},
  "compliance_level": "${COMPLIANCE_LEVEL}",
  "findings": {
    "critical_vulnerabilities": ${CRITICAL_VULNS},
    "high_vulnerabilities": ${HIGH_VULNS},
    "secrets_found": ${SECRETS_FOUND},
    "configuration_issues": ${CONFIG_ISSUES},
    "total_vulnerabilities": ${TOTAL_VULNS}
  },
  "standards_compliance": {
    "owasp_top_10": $([ ${CRITICAL_VULNS} -eq 0 ] && echo 'true' || echo 'false'),
    "cis_benchmarks": $([ ${CONFIG_ISSUES} -lt 5 ] && echo 'true' || echo 'false'),
    "secret_management": $([ ${SECRETS_FOUND} -eq 0 ] && echo 'true' || echo 'false'),
    "dependency_management": $([ ${HIGH_VULNS} -lt 10 ] && echo 'true' || echo 'false')
  }
}
EOF

echo ""
echo "========================================="
echo "Security Compliance Report Generated"
echo "========================================="
echo "Compliance Score: ${COMPLIANCE_SCORE}/100"
echo "Compliance Level: ${COMPLIANCE_LEVEL}"
echo ""
echo "Reports:"
echo "  HTML: ${COMPLIANCE_DIR}/compliance-report-${TIMESTAMP}.html"
echo "  JSON: ${COMPLIANCE_DIR}/compliance-summary-${TIMESTAMP}.json"
echo "========================================="

# Exit with error if compliance score is too low
if [ ${COMPLIANCE_SCORE} -lt 60 ]; then
  echo ""
  echo "ERROR: Compliance score below acceptable threshold (60)"
  exit 1
fi

exit 0
bashchmod +x /opt/trivy/generate-compliance-report.sh
Step 42: Update Jenkinsfile with Complete Integration
groovypipeline {
    agent any
    
    tools {
        maven "localMaven"
        jdk "localJdk"
    }
    
    environment {
        WORKSPACE = "${env.WORKSPACE}"
        NEXUS_CREDENTIAL_ID = 'Nexus-Credential'
        BUILD_TIMESTAMP = new Date().format('yyyyMMdd-HHmmss')
    }
    
    stages {
        
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/YOUR-USERNAME/Jenkins-CICD-Project.git'
            }
        }
        
        stage('Update Trivy Database') {
            steps {
                echo "Updating Trivy vulnerability database..."
                sh '/opt/trivy/update-db.sh'
            }
        }
        
        stage('Comprehensive Security Scan') {
            steps {
                echo "Running comprehensive security scan..."
                script {
                    sh """
                        /opt/trivy/comprehensive-scan.sh ${WORKSPACE} ${BUILD_ID}
                    """
                }
            }
            post {
                always {
                    archiveArtifacts artifacts: '/opt/trivy/reports/**/*',
                                   fingerprint: true,
                                   allowEmptyArchive: true
                    
                    publishHTML([
                        allowMissing: false,
                        alwaysLinkToLastBuild: true,
                        keepAll: true,
                        reportDir: '/opt/trivy/reports/html',
                        reportFiles: 'report-*.html',
                        reportName: 'Trivy Security Report'
                    ])
                }
            }
        }
        
        stage('Generate Compliance Report') {
            steps {
                echo "Generating security compliance report..."
                sh "/opt/trivy/generate-compliance-report.sh ${BUILD_ID}"
            }
            post {
                always {
                    publishHTML([
                        allowMissing: false,
                        alwaysLinkToLastBuild: true,
                        keepAll: true,
                        reportDir: '/opt/trivy/reports/compliance',
                        reportFiles: 'compliance-report-*.html',
                        reportName: 'Compliance Report'
                    ])
                }
            }
        }
        
        stage('Maven Build & Test') {
            steps {
                sh 'mvn clean install'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
        
        stage('Checkstyle Analysis') {
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
            post {
                always {
                    recordIssues(
                        tools: [checkStyle(pattern: '**/target/checkstyle-result.xml')],
                        qualityGates: [[threshold: 100, type: 'TOTAL', unstable: true]]
                    )
                }
            }
        }
        
        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool 'SonarQube-Scanner'
            }
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh """${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=maven-project \
                        -Dsonar.projectName=maven-project \
                        -Dsonar.projectVersion=1.0 \
                        -Dsonar.sources=src/ \
                        -Dsonar.java.binaries=target/classes/ \
                        -Dsonar.junit.reportsPath=target/surefire-reports/ \
                        -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                        -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml"""
                }
            }
        }
        
        stage('SonarQube Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        
        stage('Upload to Nexus') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '<Nexus-Private-IP>:8081',
                    groupId: 'webapp',
                    version: "${env.BUILD_ID}-${BUILD_TIMESTAMP}",
                    repository: 'maven-project-releases',
                    credentialsId: "${NEXUS_CREDENTIAL_ID}",
                    artifacts: [
                        [artifactId: 'webapp',
                        classifier: '',
                        file: 'webapp/target/webapp.war',
                        type: 'war']
                    ]
                )
            }
        }
        
        stage('Deploy to Dev') {
            steps {
                echo "Deploying to Dev Environment..."
                script {
                    sshagent(['Ansible-Credential']) {
                        sh """
                            ansible-playbook /opt/ansible/playbooks/deploy-webapp.yml \
                            -i /opt/ansible/inventory/hosts \
                            -e "target_env=dev" \
                            -e "workspace=${WORKSPACE}" \
                            -vv
                        """
                    }
                }
            }
        }
        
        stage('Dev Integration Tests') {
            steps {
                echo "Running integration tests on Dev..."
                sh """
                    ansible-playbook /opt/ansible/playbooks/integration-tests.yml \
                    -i /opt/ansible/inventory/hosts \
                    -e "target_env=dev"
                """
            }
        }
        
        stage('Deploy to Stage') {
            steps {
                echo "Deploying to Stage Environment..."
                script {
                    sshagent(['Ansible-Credential']) {
                        sh """
                            ansible-playbook /opt/ansible/playbooks/deploy-webapp.yml \
                            -i /opt/ansible/inventory/hosts \
                            -e "target_env=stage" \
                            -e "workspace=${WORKSPACE}" \
                            -vv
                        """
                    }
                }
            }
        }
        
        stage('Stage Integration Tests') {
            steps {
                echo "Running integration tests on Stage..."
                sh """
                    ansible-playbook /opt/ansible/playbooks/integration-tests.yml \
                    -i /opt/ansible/inventory/hosts \
                    -e "target_env=stage"
                """
            }
        }
        
        stage('Post-Deployment Monitoring') {
            steps {
                echo "Monitoring Stage environment..."
                sh """
                    ansible-playbook /opt/ansible/playbooks/post-deployment-monitoring.yml \
                    -i /opt/ansible/inventory/hosts \
                    -e "target_env=stage"
                """
            }
        }
        
        stage('Approval for Production') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    input message: 'Deploy to Production?',
                          ok: 'Deploy',
                          submitter: 'admin'
                }
            }
        }
        
        stage('Deploy to Production') {
            steps {
                echo "Deploying to Production Environment..."
                script {
                    sshagent(['Ansible-Credential']) {
                        sh """
                            ansible-playbook /opt/ansible/playbooks/deploy-webapp.yml \
                            -i /opt/ansible/inventory/hosts \
                            -e "target_env=prod" \
                            -e "workspace=${WORKSPACE}" \
                            -vv
                        """
                    }
                }
            }
        }
        
        stage('Production Validation') {
            steps {
                parallel(
                    "Health Check": {
                        sh """
                            ansible-playbook /opt/ansible/playbooks/health-check.yml \
                            -i /opt/ansible/inventory/hosts \
                            -e "target_env=prod"
                        """
                    },
                    "Integration Tests": {
                        sh """
                            ansible-playbook /opt/ansible/playbooks/integration-tests.yml \
                            -i /opt/ansible/inventory/hosts \
                            -e "target_env=prod"
                        """
                    },
                    "Performance Test": {
                        sh """
                            ansible-playbook /opt/ansible/playbooks/performance-test.yml \
                            -e "target_host=\$(aws ec2 describe-instances --filters 'Name=tag:Name,Values=Prod-Env' --query 'Reservations[0].Instances[0].PrivateIpAddress' --output text)"
                        """
                    }
                )
            }
        }
        
        stage('Production Monitoring') {
            steps {
                echo "Monitoring Production for 5 minutes..."
                sh """
                    ansible-playbook /opt/ansible/playbooks/post-deployment-monitoring.yml \
                    -i /opt/ansible/inventory/hosts \
                    -e "target_env=prod"
                """
            }
        }
        
        stage('Remote Security Scan') {
            steps {
                echo "Running security scan on deployed applications..."
                sh """
                    ansible-playbook /opt/ansible/playbooks/remote-security-scan.yml \
                    -i /opt/ansible/inventory/hosts \
                    -e "target_env=prod"
                """
            }
        }
        
        stage('Generate Pipeline Metrics') {
            steps {
                sh """
                    ansible-playbook /opt/ansible/playbooks/pipeline-metrics.yml \
                    -e "jenkins_host=\$(hostname -I | awk '{print \$1}')"
                """
            }
        }
    }
    
    post {
        always {
            // Export Trivy metrics
            sh '/opt/trivy/export-metrics.sh'
            
            // Archive all reports
            archiveArtifacts artifacts: '**/target/*.warRetryEContinue, /opt/trivy/reports//., /opt/ansible/reports//.',
fingerprint: true,
allowEmptyArchive: true
        // Clean workspace
        cleanWs()
    }
    
    success {
        slackSend channel: '#yourname-jenkins-cicd-alerts',
                 color: 'good',
                 message: """
                 ✅ *BUILD SUCCESS*
                 Job: ${env.JOB_NAME}
                 Build: #${env.BUILD_NUMBER}
                 Duration: ${currentBuild.durationString}
                 
                 📊 *Quality Metrics:*
                 • Security Scan: PASSED
                 • SonarQube: PASSED
                 • All Tests: PASSED
                 
                 🚀 *Deployment Status:*
                 • Dev: ✅ Deployed
                 • Stage: ✅ Deployed
                 • Prod: ✅ Deployed
                 
                 📈 *Reports:*
                 • Trivy: ${env.BUILD_URL}Trivy_20Security_20Report/
                 • Compliance: ${env.BUILD_URL}Compliance_20Report/
                 
                 👉 <${env.BUILD_URL}|View Details>
                 """
    }
    
    failure {
        slackSend channel: '#yourname-jenkins-cicd-alerts',
                 color: 'danger',
                 message: """
                 ❌ *BUILD FAILED*
                 Job: ${env.JOB_NAME}
                 Build: #${env.BUILD_NUMBER}
                 
                 💥 *Failure Stage:* ${env.STAGE_NAME}
                 
                 🔍 *Action Required:*
                 • Check console output
                 • Review security/quality reports
                 • Verify environment health
                 
                 👉 <${env.BUILD_URL}console|View Console Output>
                 """
        
        // Trigger rollback if deployment failed
        script {
            if (env.STAGE_NAME?.contains('Deploy')) {
                echo "Deployment failed - triggering rollback..."
                sh """
                    ansible-playbook /opt/ansible/playbooks/intelligent-rollback.yml \
                    -i /opt/ansible/inventory/hosts \
                    -e "target_env=\${FAILED_ENV}"
                """
            }
        }
    }
    
    unstable {
        slackSend channel: '#yourname-jenkins-cicd-alerts',
                 color: 'warning',
                 message: """
                 ⚠️ *BUILD UNSTABLE*
                 Job: ${env.JOB_NAME}
                 Build: #${env.BUILD_NUMBER}
                 
                 ⚠️ *Issues Found:*
                 • Quality gates may have warnings
                 • Review test results
                 
                 👉 <${env.BUILD_URL}|View Details>
                 """
    }
}
}

### Step 43: Create Dashboard Integration Script
````bash
vi /opt/ansible/scripts/update-dashboard-metrics.sh
````
````bash
#!/bin/bash
# Update dashboard metrics from pipeline results

JENKINS_URL="http://localhost:8080"
METRICS_DIR="/opt/ansible/metrics"
DASHBOARD_DATA="/var/www/html/dashboard/data"

mkdir -p ${DASHBOARD_DATA}

# Get latest pipeline metrics
LATEST_METRICS=$(ls -t ${METRICS_DIR}/pipeline-performance.json 2>/dev/null | head -1)

if [ -f "${LATEST_METRICS}" ]; then
  # Extract key metrics
  AVG_BUILD_TIME=$(jq -r '.metrics.average_build_time_minutes' ${LATEST_METRICS})
  SUCCESS_RATE=$(jq -r '.metrics.success_rate_percent' ${LATEST_METRICS})
  LAST_BUILD=$(jq -r '.metrics.last_build_result' ${LATEST_METRICS})
  
  # Get Trivy metrics
  TRIVY_METRICS="/opt/trivy/metrics/trivy_metrics.prom"
  if [ -f "${TRIVY_METRICS}" ]; then
    CRITICAL_VULNS=$(grep "trivy_vulnerabilities_critical" ${TRIVY_METRICS} | awk '{print $2}')
    HIGH_VULNS=$(grep "trivy_vulnerabilities_high" ${TRIVY_METRICS} | awk '{print $2}')
  else
    CRITICAL_VULNS=0
    HIGH_VULNS=0
  fi
  
  # Get deployment status
  DEV_STATUS=$(ansible dev -i /opt/ansible/inventory/hosts -m uri -a "url=http://localhost:8080/webapp/ return_content=no" 2>/dev/null | grep -q "SUCCESS" && echo "UP" || echo "DOWN")
  STAGE_STATUS=$(ansible stage -i /opt/ansible/inventory/hosts -m uri -a "url=http://localhost:8080/webapp/ return_content=no" 2>/dev/null | grep -q "SUCCESS" && echo "UP" || echo "DOWN")
  PROD_STATUS=$(ansible prod -i /opt/ansible/inventory/hosts -m uri -a "url=http://localhost:8080/webapp/ return_content=no" 2>/dev/null | grep -q "SUCCESS" && echo "UP" || echo "DOWN")
  
  # Generate dashboard JSON
  cat > ${DASHBOARD_DATA}/metrics.json <<EOF
{
  "timestamp": "$(date -u +%Y-%m-%dT%H:%M:%SZ)",
  "pipeline": {
    "average_build_time": ${AVG_BUILD_TIME},
    "success_rate": ${SUCCESS_RATE},
    "last_build_status": "${LAST_BUILD}"
  },
  "security": {
    "critical_vulnerabilities": ${CRITICAL_VULNS},
    "high_vulnerabilities": ${HIGH_VULNS}
  },
  "deployments": {
    "dev": "${DEV_STATUS}",
    "stage": "${STAGE_STATUS}",
    "production": "${PROD_STATUS}"
  }
}
EOF

  echo "Dashboard metrics updated successfully"
else
  echo "No pipeline metrics found"
fi
````
````bash
chmod +x /opt/ansible/scripts/update-dashboard-metrics.sh
````

### Step 44: Create Simple Web Dashboard
````bash
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd

sudo mkdir -p /var/www/html/dashboard
sudo chown -R jenkins:jenkins /var/www/html/dashboard

vi /var/www/html/dashboard/index.html
````
````html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CI/CD Pipeline Dashboard</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
        }
        
        header {
            background: white;
            padding: 30px;
            border-radius: 10px;
            margin-bottom: 30px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.1);
        }
        
        h1 {
            color: #2c3e50;
            margin-bottom: 10px;
        }
        
        .last-updated {
            color: #7f8c8d;
            font-size: 14px;
        }
        
        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .card {
            background: white;
            padding: 25px;
            border-radius: 10px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
        }
        
        .card:hover {
            transform: translateY(-5px);
        }
        
        .card-header {
            display: flex;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid #ecf0f1;
        }
        
        .card-icon {
            width: 50px;
            height: 50px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 24px;
            margin-right: 15px;
        }
        
        .icon-pipeline { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); }
        .icon-security { background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); }
        .icon-deploy { background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%); }
        
        .card-title {
            font-size: 18px;
            color: #2c3e50;
            font-weight: 600;
        }
        
        .metric {
            margin-bottom: 15px;
        }
        
        .metric-label {
            font-size: 14px;
            color: #7f8c8d;
            margin-bottom: 5px;
        }
        
        .metric-value {
            font-size: 32px;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .metric-value.success { color: #27ae60; }
        .metric-value.warning { color: #f39c12; }
        .metric-value.danger { color: #e74c3c; }
        
        .status-badge {
            display: inline-block;
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: bold;
            text-transform: uppercase;
        }
        
        .status-up {
            background: #27ae60;
            color: white;
        }
        
        .status-down {
            background: #e74c3c;
            color: white;
        }
        
        .environment {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 8px;
            margin-bottom: 10px;
        }
        
        .env-name {
            font-weight: 600;
            color: #2c3e50;
        }
        
        .progress-bar {
            width: 100%;
            height: 8px;
            background: #ecf0f1;
            border-radius: 4px;
            overflow: hidden;
            margin-top: 10px;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
            transition: width 0.3s ease;
        }
        
        .links {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 30px;
        }
        
        .link-card {
            background: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            text-decoration: none;
            color: #2c3e50;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
            transition: all 0.3s ease;
        }
        
        .link-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 20px rgba(0,0,0,0.15);
        }
        
        .link-icon {
            font-size: 32px;
            margin-bottom: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>🚀 CI/CD Pipeline Dashboard</h1>
            <p class="last-updated">Last updated: <span id="lastUpdate">Loading...</span></p>
        </header>
        
        <div class="grid">
            <!-- Pipeline Metrics -->
            <div class="card">
                <div class="card-header">
                    <div class="card-icon icon-pipeline">⚙️</div>
                    <div class="card-title">Pipeline Metrics</div>
                </div>
                <div class="metric">
                    <div class="metric-label">Average Build Time</div>
                    <div class="metric-value" id="buildTime">--</div>
                    <small>minutes</small>
                </div>
                <div class="metric">
                    <div class="metric-label">Success Rate</div>
                    <div class="metric-value success" id="successRate">--</div>
                    <div class="progress-bar">
                        <div class="progress-fill" id="successProgress" style="width: 0%"></div>
                    </div>
                </div>
                <div class="metric">
                    <div class="metric-label">Last Build Status</div>
                    <span class="status-badge" id="lastBuildStatus">UNKNOWN</span>
                </div>
            </div>
            
            <!-- Security Metrics -->
            <div class="card">
                <div class="card-header">
                    <div class="card-icon icon-security">🛡️</div>
                    <div class="card-title">Security Metrics</div>
                </div>
                <div class="metric">
                    <div class="metric-label">Critical Vulnerabilities</div>
                    <div class="metric-value danger" id="criticalVulns">--</div>
                </div>
                <div class="metric">
                    <div class="metric-label">High Vulnerabilities</div>
                    <div class="metric-value warning" id="highVulns">--</div>
                </div>
                <div class="metric">
                    <div class="metric-label">Security Status</div>
                    <span class="status-badge status-up" id="securityStatus">MONITORING</span>
                </div>
            </div>
            
            <!-- Deployment Status -->
            <div class="card">
                <div class="card-header">
                    <div class="card-icon icon-deploy">🌐</div>
                    <div class="card-title">Deployment Status</div>
                </div>
                
                <div class="environment">
                    <span class="env-name">Development</span>
                    <span class="status-badge" id="devStatus">--</span>
                </div>
                
                <div class="environment">
                    <span class="env-name">Staging</span>
                    <span class="status-badge" id="stageStatus">--</span>
                </div>
                
                <div class="environment">
                    <span class="env-name">Production</span>
                    <span class="status-badge" id="prodStatus">--</span>
                </div>
            </div>
        </div>
        
        <!-- Quick Links -->
        <div class="links">
            <a href="http://JENKINS-IP:8080" class="link-card" target="_blank">
                <div class="link-icon">🔧</div>
                <div>Jenkins</div>
            </a>
            <a href="http://SONARQUBE-IP:9000" class="link-card" target="_blank">
                <div class="link-icon">📊</div>
                <div>SonarQube</div>
            </a>
            <a href="http://NEXUS-IP:8081" class="link-card" target="_blank">
                <div class="link-icon">📦</div>
                <div>Nexus</div>
            </a>
            <a href="http://GRAFANA-IP:3000" class="link-card" target="_blank">
                <div class="link-icon">📈</div>
                <div>Grafana</div>
            </a>
            <a href="http://PROMETHEUS-IP:9090" class="link-card" target="_blank">
                <div class="link-icon">🔍</div>
                <div>Prometheus</div>
            </a>
            <a href="http://SPLUNK-IP:8000" class="link-card" target="_blank">
                <div class="link-icon">📝</div>
                <div>Splunk</div>
            </a>
        </div>
    </div>
    
    <script>
        // Fetch and update metrics
        async function updateMetrics() {
            try {
                const response = await fetch('/dashboard/data/metrics.json');
                const data = await response.json();
                
                // Update timestamp
                document.getElementById('lastUpdate').textContent = 
                    new Date(data.timestamp).toLocaleString();
                
                // Update pipeline metrics
                document.getElementById('buildTime').textContent = 
                    data.pipeline.average_build_time.toFixed(2);
                document.getElementById('successRate').textContent = 
                    data.pipeline.success_rate.toFixed(1) + '%';
                document.getElementById('successProgress').style.width = 
                    data.pipeline.success_rate + '%';
                
                const statusBadge = document.getElementById('lastBuildStatus');
                statusBadge.textContent = data.pipeline.last_build_status;
                statusBadge.className = 'status-badge ' + 
                    (data.pipeline.last_build_status === 'SUCCESS' ? 'status-up' : 'status-down');
                
                // Update security metrics
                document.getElementById('criticalVulns').textContent = 
                    data.security.critical_vulnerabilities;
                document.getElementById('highVulns').textContent = 
                    data.security.high_vulnerabilities;
                
                // Update security status
                const secStatus = document.getElementById('securityStatus');
                if (data.security.critical_vulnerabilities === 0) {
                    secStatus.className = 'status-badge status-up';
                    secStatus.textContent = 'SECURE';
                } else {
                    secStatus.className = 'status-badge status-down';
                    secStatus.textContent = 'AT RISK';
                }
                
                // Update deployment status
                updateDeploymentStatus('devStatus', data.deployments.dev);
                updateDeploymentStatus('stageStatus', data.deployments.stage);
                updateDeploymentStatus('prodStatus', data.deployments.production);
                
            } catch (error) {
                console.error('Error fetching metrics:', error);
            }
        }
        
        function updateDeploymentStatus(elementId, status) {
            const element = document.getElementById(elementId);
            element.textContent = status;
            element.className = 'status-badge ' + 
                (status === 'UP' ? 'status-up' : 'status-down');
        }
        
        // Update metrics every 30 seconds
        updateMetrics();
        setInterval(updateMetrics, 30000);
    </script>
</body>
</html>
````

**Update the Quick Links with your actual IPs:**
````bash
sudo sed -i "s|JENKINS-IP|<Your-Jenkins-IP>|g" /var/www/html/dashboard/index.html
sudo sed -i "s|SONARQUBE-IP|<Your-SonarQube-IP>|g" /var/www/html/dashboard/index.html
sudo sed -i "s|NEXUS-IP|<Your-Nexus-IP>|g" /var/www/html/dashboard/index.html
sudo sed -i "s|GRAFANA-IP|<Your-Grafana-IP>|g" /var/www/html/dashboard/index.html
sudo sed -i "s|PROMETHEUS-IP|<Your-Prometheus-IP>|g" /var/www/html/dashboard/index.html
sudo sed -i "s|SPLUNK-IP|<Your-Splunk-IP>|g" /var/www/html/dashboard/index.html
````

**Create dummy data directory:**
````bash
sudo mkdir -p /var/www/html/dashboard/data
sudo chown -R jenkins:jenkins /var/www/html/dashboard
````

**Add cron job to update dashboard:**
````bash
sudo crontab -e -u jenkins
````

Add:
*/5 * * * * /opt/ansible/scripts/update-dashboard-metrics.sh > /dev/null 2>&1

### Step 45: Final Testing Checklist

Create a comprehensive test plan:
````bash
vi /opt/ansible/TEST-PLAN.md
````
````markdown
# Complete CI/CD Pipeline Test Plan

## Pre-Deployment Tests

### 1. Infrastructure Validation
- [ ] All 8 EC2 instances running
- [ ] Security groups properly configured
- [ ] SSH access working to all servers
- [ ] All services started (Jenkins, Nexus, SonarQube, etc.)

### 2. Tool Verification
```bash
# Jenkins
curl -I http://<Jenkins-IP>:8080

# SonarQube
curl -I http://<SonarQube-IP>:9000

# Nexus
curl -I http://<Nexus-IP>:8081

# Prometheus
curl http://<Prometheus-IP>:9090/-/healthy

# Grafana
curl -I http://<Grafana-IP>:3000

# Splunk
curl -I http://<Splunk-IP>:8000
```

### 3. Ansible Connectivity
```bash
ansible all -i /opt/ansible/inventory/hosts -m ping
```

### 4. Trivy Installation
```bash
trivy --version
/opt/trivy/update-db.sh
```

## Pipeline Execution Tests

### 5. Trigger Build
- [ ] GitHub webhook triggers build automatically
- [ ] Manual build trigger works
- [ ] Build parameters accessible

### 6. Security Scanning
- [ ] Trivy database updates successfully
- [ ] Filesystem scan completes
- [ ] Dependency scan completes
- [ ] Secret detection runs
- [ ] Reports generated (HTML, JSON, SARIF)
- [ ] Compliance report generated

### 7. Build & Test
- [ ] Maven build succeeds
- [ ] Unit tests pass
- [ ] Test reports generated
- [ ] Code coverage calculated

### 8. Code Quality
- [ ] Checkstyle analysis completes
- [ ] SonarQube analysis runs
- [ ] Quality gate evaluation works
- [ ] Blocks on quality gate failure

### 9. Artifact Management
- [ ] Artifact uploaded to Nexus
- [ ] Correct version format
- [ ] Artifact browsable in Nexus UI

### 10. Deployment Tests

#### Dev Environment
```bash
# Check deployment
curl http://<Dev-IP>:8080/webapp/

# Check health
ansible-playbook /opt/ansible/playbooks/health-check.yml \
  -i /opt/ansible/inventory/hosts \
  -e "target_env=dev"

# Check logs
ssh ansibleadmin@<Dev-IP> "sudo tail -50 /var/log/tomcat/catalina.out"
```

#### Stage Environment
```bash
# Same checks as Dev
curl http://<Stage-IP>:8080/webapp/

# Integration tests
ansible-playbook /opt/ansible/playbooks/integration-tests.yml \
  -i /opt/ansible/inventory/hosts \
  -e "target_env=stage"
```

#### Production Environment
```bash
# Manual approval required
# After approval:
curl http://<Prod-IP>:8080/webapp/

# Post-deployment monitoring
# Should run for 5 minutes automatically
```

## Post-Deployment Tests

### 11. Monitoring Validation
```bash
# Check Prometheus targets
curl http://<Prometheus-IP>:9090/api/v1/targets | jq '.data.activeTargets[].health'

# Check Grafana dashboards
curl -H "Authorization: Bearer <token>" http://<Grafana-IP>:3000/api/dashboards/home

# Check Trivy metrics
curl http://<Jenkins-IP>:9101/metrics
```

### 12. Logging Validation
```bash
# Check Splunk
# Access http://<Splunk-IP>:8000
# Search: index=* source="/var/log/tomcat/*"
# Verify logs from all environments
```

### 13. Notification Tests
- [ ] Slack notifications received for all stages
- [ ] Success notification format correct
- [ ] Failure notification format correct
- [ ] Links in notifications work

### 14. Dashboard Tests
```bash
# Access dashboard
curl http://<Jenkins-IP>/dashboard/

# Verify metrics update
/opt/ansible/scripts/update-dashboard-metrics.sh
```

## Failure Scenario Tests

### 15. Security Scan Failure
```bash
# Inject a vulnerability
# Build should fail at security scan stage
# Verify:
- [ ] Build stops at Trivy stage
- [ ] Report shows vulnerabilities
- [ ] Slack notification sent
- [ ] No deployment occurs
```

### 16. Quality Gate Failure
```bash
# Temporarily set SonarQube quality gate to fail
# Verify:
- [ ] Build stops at Quality Gate stage
- [ ] SonarQube shows failure reason
- [ ] Slack notification sent
- [ ] No deployment occurs
```

### 17. Deployment Failure
```bash
# Stop Tomcat on Dev server
sudo systemctl stop tomcat

# Trigger build
# Verify:
- [ ] Deployment fails
- [ ] Health check catches failure
- [ ] Rollback triggered (if configured)
- [ ] Slack alert sent
```

### 18. Rollback Test
```bash
# Deploy version 1
# Deploy version 2
# Manually trigger rollback
ansible-playbook /opt/ansible/playbooks/rollback-webapp.yml \
  -i /opt/ansible/inventory/hosts \
  -e "target_env=dev"

# Verify:
- [ ] Previous version restored
- [ ] Application accessible
- [ ] No errors in logs
```

## Performance Tests

### 19. Build Performance
- [ ] Build completes in < 15 minutes
- [ ] Security scan < 3 minutes
- [ ] Deployment < 1 minute per environment

### 20. Application Performance
```bash
# Run performance test
ansible-playbook /opt/ansible/playbooks/performance-test.yml \
  -e "target_host=<Prod-IP>"

# Verify:
- [ ] Response time < 2 seconds
- [ ] No errors under load
- [ ] Memory stable
```

## Security Tests

### 21. Vulnerability Management
- [ ] Critical vulnerabilities blocked
- [ ] High vulnerabilities reported
- [ ] Compliance report generated
- [ ] Remediation recommendations provided

### 22. Secret Detection
- [ ] Hardcoded secrets detected
- [ ] Build fails if secrets found
- [ ] Report shows secret locations

### 23. Access Control
- [ ] Production requires approval
- [ ] Only authorized users can approve
- [ ] SSH keys properly configured
- [ ] Credentials encrypted in Jenkins

## Documentation Tests

### 24. Verify Documentation
- [ ] README.md complete
- [ ] CICD-PIPELINE-DOCUMENTATION.md accurate
- [ ] QUICK-REFERENCE.md helpful
- [ ] TEST-PLAN.md comprehensive

## Final Validation

### 25. End-to-End Test
```bash
# Make code change
echo "Test $(date)" >> README.md
git add README.md
git commit -m "E2E test"
git push origin main

# Monitor full pipeline execution
# Verify all stages pass
# Verify application deployed to all environments
# Verify all reports generated
# Verify all notifications sent
```

### 26. Disaster Recovery Test
```bash
# Simulate server failure
# Stop Jenkins
sudo systemctl stop jenkins

# Restart and verify
sudo systemctl start jenkins
# Check if jobs and configurations preserved
```

## Test Results Summary

| Test Category | Tests | Passed | Failed | Notes |
|--------------|-------|---------|--------|-------|
| Infrastructure | 4 | | | |
| Tools | 6 | | | |
| Security | 6 | | | |
| Build | 4 | | | |
| Deployment | 9 | | | |
| Monitoring | 3 | | | |
| Notifications | 3 | | | |
| Performance | 2 | | | |
| Documentation | 4 | | | |
| **TOTAL** | **41** | | | |

## Sign-off

- Tested by: _______________
- Date: _______________
- Pipeline Version: _______________
- Status: _______________
````

---

## **🎊 FINAL SUMMARY - Complete Integration**

### **What You've Accomplished:**
┌───────────────────────────────────────────────────────────────┐
│         🏆 ENTERPRISE-GRADE CI/CD PIPELINE COMPLETE 🏆        │
├───────────────────────────────────────────────────────────────┤
│                                                                │
│  ✅ Source Control Management (GitHub + Webhooks)             │
│  ✅ Continuous Integration (Jenkins)                          │
│  ✅ Automated Building (Maven)                                │
│  ✅ Comprehensive Testing (JUnit + Integration Tests)         │
│  ✅ Security Scanning (Trivy - Multi-layer)                   │
│  ✅ Code Quality Gates (SonarQube + Checkstyle)              │
│  ✅ Artifact Management (Nexus Repository)                    │
│  ✅ Infrastructure as Code (Ansible Playbooks)                │
│  ✅ Multi-Environment Deployment (Dev/Stage/Prod)             │
│  ✅ Health Checks & Validation                                │
│  ✅ Automated Rollback Mechanism                              │
│  ✅ Performance Testing                                        │
│  ✅ Metrics Collection (Prometheus)                           │
│  ✅ Visualization (Grafana Dashboards)                        │
│  ✅ Log Aggregation (Splunk)                                  │
│  ✅ Real-time Notifications (Slack)                           │
│  ✅ Compliance Reporting                                       │
│  ✅ Custom Web Dashboard                                       │
│  ✅ Complete Documentation                                     │
│                                                                │
└───────────────────────────────────────────────────────────────┘

### **Final Commands to Execute:**
````bash
# 1. Commit all changes
cd Jenkins-CICD-Project
git add .
git commit -m "Complete CI/CD pipeline with Ansible and Trivy integration"
git push origin main

# 2. Verify all services
ansible all -i /opt/ansible/inventory/hosts -m ping

# 3. Update Trivy database
/opt/trivy/update-db.sh

# 4. Test dashboard
curl http://<Jenkins-IP>/dashboard/

# 5. Trigger final test build
# Go to Jenkins UI and click "Build Now"

# 6. Access dashboard
firefox http://<Jenkins-IP>/dashboard/
````

### **Access URLs Summary:**
Jenkins:    http://<Jenkins-IP>:8080 (admin/admin)
Dashboard:  http://<Jenkins-IP>/dashboard/
SonarQube:  http://<SonarQube-IP>:9000 (admin/<password>)
Nexus:      http://<Nexus-IP>:8081 (admin/adminRetryEEnd-to-End Jenkins CI/CD Pipeline Project Architecture (Java Web Application)
CompleteCICDProject!Project ToolBox 🧰
Git Git will be used to manage our application source code.
Github Github is a free and open source distributed VCS designed to handle everything from small to very large projects with speed and efficiency
Jenkins Jenkins is an open source automation CI tool which enables developers around the world to reliably build, test, and deploy their software
Maven Maven will be used for the application packaging and building including running unit test cases
Checkstyle Checkstyle is a static code analysis tool used in software development for checking if Java source code is compliant with specified coding rules and practices.
SonarQube SonarQube Catches bugs and vulnerabilities in your app, with thousands of automated Static Code Analysis rules.
Nexus Nexus Manage Binaries and build artifacts across your software supply chain
Ansible Ansible will be used for the application deployment to both lower environments and production
EC2 EC2 allows users to rent virtual computers (EC2) to run their own workloads and applications.
Slack Slack is a communication platform designed for collaboration which can be leveraged to build and develop a very robust DevOps culture. Will be used for Continuous feedback loop.
Prometheus Prometheus is a free software application used for event/metric monitoring and alerting for both application and infrastructure.
Grafana Grafana is a multi-platform open source analytics and interactive visualization web application. It provides charts, graphs, and alerts for the web when connected to supported data sources.
Splunk Splunk is an innovative technology which searches and indexes application/system log files and helps organizations derive insights from the data.
Jenkins Complete CI/CD Pipeline Environment Setup Runbook
Create a GitHub Repository with the name Jenkins-CICD-Project and push the code in this branch(main) to your remote repository (your newly created repository).Go to GitHub (github.com)
Login to your GitHub Account
Open this page and click Fork.
My repo is going to be replicated on your Github Account
Confirm that the code exist on GitHub
Jenkins/Maven/AnsibleCreate an Amazon Linux 2 VM instance and call it "jenkins-maven-ansible"
Instance type: t2.medium
Security Group (Open): 8080, 9100 and 22 to 0.0.0.0/0
Key pair: Select or create a new keypair
User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/maven-nexus-sonarqube-jenkins-install/jenkins-install.sh
Launch Instance
SonarQubeCreate an Create an Ubuntu 20.04 VM instance and call it "SonarQube"
Instance type: t2.medium
Security Group (Open): 9000, 9100 and 22 to 0.0.0.0/0
Key pair: Select or create a new keypair
User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/maven-nexus-sonarqube-jenkins-install/sonarqube-install.sh
Launch Instance
NexusCreate an Amazon Linux 2 VM instance and call it "Nexus"
Instance type: t2.medium
Security Group (Open): 8081, 9100 and 22 to 0.0.0.0/0
Key pair: Select or create a new keypair
User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/maven-nexus-sonarqube-jenkins-install/nexus-install.sh
Launch Instance
EC2 (Dev/Stage/Prod)Create 3 Amazon Linux 2 VM instance and call them (Names: Dev-Env, Stage-Env and Prod-Env)
Instance type: t2.micro
Security Group (Open): 8080, 9100, 9997 and 22 to 0.0.0.0/0
Key pair: Select or create a new keypair
User data (Copy the following user data): https://github.com/awanmbandi/realworld-cicd-pipeline-project/blob/tomcat-splunk-installation/tomcat-ssh-configure.sh
Launch Instance
PrometheusCreate an Ubuntu 20.04 VM instance and call it "Prometheus"
Instance type: t2.micro
Security Group (Open): 9090 and 22 to 0.0.0.0/0
Key pair: Select or create a new keypair
Launch Instance
GrafanaCreate an Ubuntu 20.04 VM instance and call it "Grafana"
Instance type: t2.micro
Security Group (Open): 3000 and 22 to 0.0.0.0/0
Key pair: Select or create a new keypair
Launch Instance
EC2 (Splunk)Create an Amazon Linux 2 VM instance and call it (Names: Splunk-Server)
Instance type: t2.micro
Security Group (Open): 22, 8000, 9997, 9100 to 0.0.0.0/0
Key pair: Select or create a new keypair
Launch Instance
NOTE: Confirm and make sure you have a total of 8 VM instances
PipelineEnvSetup!SlackGo to the bellow Workspace and create a Private Slack Channel and name it "yourfirstname-jenkins-cicd-pipeline-alerts"
Link: https://join.slack.com/t/realworldcicdproject/shared_invite/zt-1tryd7x1v-g8a~zEJBKKchVvvK87jkeQ
You can either join through the browser or your local Slack App
Create a Private Channel using the naming convention cicd-pipeline-project-alerts
Click on the Drop down on the Channel and select Integrations and take Add an App
Search for Jenkins and click on View -->> Configuration/Install -->> Add to Slack
On Post to Channel: Click the Drop Down and select your channel above cicd-pipeline-project-alerts
Click Add Jenkins CI Integration
SAVE SETTINGS/CONFIGURATIONS
Leave this page open SlackConfig!
NOTE: Update Your Jenkins file with your Slack Channel Name
Go back to your local, open your "Jenkins-CICD-Project" repo/folder/directory on VSCODE
Open your "Jenkinsfile"
Update the slack channel name on line "97" (there about)
Change name from "cicd-project-alerts" (or whatever name thst's there) to yours
Add the changes to git, commit and push to GitHub
Confirm the changes are available on GitHub
Save and Push to GitHub
Configure All Systems
Configure Promitheus
Login/SSH to your Prometheus Server
Clone the following repository: https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
Change directory to "realworld-cicd-pipeline-project"
Swtitch to the "prometheus-and-grafana" git branch
Run: ./install-prometheus.sh
Confirm the status shows "Active (running)"
Exit
Configure Grafana
Login/SSH to your Grafana Server
Clone the following repository: https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
Change directory to "realworld-cicd-pipeline-project"
Swtitch to the "prometheus-and-grafana" git branch
Run: ls or ll (to confirm you have the branch files)
Run: ./install-grafana.sh
Confirm the status shows "Active (running)"
Exit
Configure The "Node Exporter" accross the "Dev", "Stage" and "Prod" instances including your "Pipeline Infra"
Login/SSH into the "Dev-Env", "Stage-Env" and "Prod-Env" VM instance
Perform the following operations on all of them
Install git by running: sudo yum install git -y
Clone the following repository: https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
Change directory to "realworld-cicd-pipeline-project"
Swtitch to the "prometheus-and-grafana" git branch
Run: ls or ll (to confirm you have the branch files)
Run: ./install-node-exporter.sh
Confirm the status shows "Active (running)"
Access the Node Exporters running on port "9100", open your browser and run the below
Dev-EnvPublicIPaddress:9100 (Confirm this page is accessible)
Stage-EnvPublicIPaddress:9100 (Confirm this page is accessible)
Prod-EnvPublicIPaddress:9100 (Confirm this page is accessible)
Exit
Configure The "Node Exporter" on the "Jenkins-Maven-Ansible", "Nexus" and "SonarQube" instances
Login/SSH into the "Jenkins-Maven-Ansible", "Nexus" and "SonarQube" VM instance
Perform the following operations on all of them
Install git by running: sudo yum install git -y (The SonarQube server already has git)
Clone the following repository: https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
Change directory to "realworld-cicd-pipeline-project"
Swtitch to the "prometheus-and-grafana" git branch
Run: ls or ll (to confirm you have the branch files including "install-node-exporter.sh")
Run: ./install-node-exporter.sh
Make sure the status shows "Active (running)"
Access the Node Exporters running on port "9100", open your browser and run the below
Jenkins-Maven-AnsiblePublicIPaddress:9100 (Confirm the pages are accessible)
NexusPublicIPaddress:9100
SonarQubePublicIPaddress:9100
Exit NodeExporter!
Update the Prometheus config file and include all the IP Addresses of the Pipeline Instances that are
running the Node Exporter API. That'll include ("Dev", "Stage", "Prod", "Jenkins-Maven-Ansible", "Nexus" and "SonarQube")SSH into the Prometheus instance either using your GitBash (Windows) or Terminal (macOS) or browser
Run the command: sudo vi /etc/prometheus/prometheus.yml
Navigate to "- targets: ['localhost:9090']" and add the "IPAddress:9100" for all the above Pipeline instances. Ecample "- targets: ['localhost:9090', 'DevIPAddress:9100', 'StageIPAddress:9100', 'ProdIPAddress:9100', 'Jenkins-Maven-AnsibleIPAddress:9100'] ETC..."
Save the Config File and Quit
Open a TAB on your choice browser
Copy the Prometheus PublicIP Addres and paste on the browser/tab with port 9100 e.g "PrometheusPublicIPAddres:9100"
Once you get to the Prometheus Dashboard Click on "Status" and Click on "Targets"
Confirm that Prometheus is able to reach everyone of your Nodes, do this by confirming the Status "UP" (green)
Done ConfigurePrometheus!
Open a New Tab on your browser for Grafana also if you've not done so already.
Copy your Grafana Instance Public IP and put on the browser with port 3000 e.g "GrafanaPublic:3000"
Once the UI Opens pass the following username and password
Username: admin
Password: admin
New Username: admin
New Password: admin
Save and Continue ConfigureGrafana!
Once you get into Grafana, follow the below steps to Import a Dashboard into Grafana to visualize your Infrastructure/App Metrics
Click on "Configuration/Settings" on your left
Click on "Data Sources"
Click on "Add Data Source"
Select Prometheus
Underneath HTTP URL: http://PrometheusPublicOrPrivateIPaddress:9090
Click on "SAVE and TEST"
Navigate to "Create" on your left (the + sign)
Click on "Import"
Copy the following link: https://grafana.com/grafana/dashboards/1860
Paste the above link where you have "Import Via Grafana.com"
Click on Load (The one right beside the link you just pasted)
Scrol down to "Prometheus" and select the "Data Source" you defined ealier which is "Prometheus"
CLICK on "Import"
Refresh your Grafana Dashbaord
Click on the "Drop Down" for "Host" and select any of the "Instances(IP)" GrafanaMetrics!
Setup Splunk Server and Configure Forwarders
A) SSH into your Splunk Server including Dev, Stage and Prod Instances to Configure Splunk
NOTE: Execute and Perform all operations across all your Dev, Stage and Prod EnvironmentsNOTE: Run all commands and queries across all your VMs (Dev, Stage and Prod)Download the Splunk RPM installer package for Linux
wget -O splunk-9.0.4.1-419ad9369127-linux-2.6-x86_64.rpm "https://download.splunk.com/products/splunk/releases/9.0.4.1/linux/splunk-9.0.4.1-419ad9369127-linux-2.6-x86_64.rpm"
Install Splunk
sudo yum install ./splunk-9.0.2-17e00c557dc1-linux-2.6-x86_64.rpm -y
Start the splunk server
sudo bash
cd /opt/splunk/bin
./splunk start --accept-license --answer-yes
Enter administrator username and password, remember this because you will need this to log into the applicationNOTE: The Password must be up to 8 characters. SplunkSetup1!Access your Splunk Installation at http://Splunk-Server-IP:8000 and log into splunkUsername: admin, Password: Same Password You Just Configured Above SplunkSetup2!
NOTE(MANDATORY): Once you login to the splunk IndexerClick on Settings -->> Click Server Settings -->> Click General Settings
Go ahead and Change the Pause indexing if free disk space from 5000 to 50
Click on Save SplunkSetup3!
Step 2: Install The Splunk Forwarder only on the Dev, Stage and Prod Servers
NOTE: Execute every command mentioned bellow across all application servers in all the enviroments
NOTE: Do Not install the Splunk Server in these resources/environments
SSH Into your instances, as normal user ec2-user or ubuntu or centos etc
exit
Download the Splunk forwarder RPM installer package
wget -O splunkforwarder-9.0.4-de405f4a7979-linux-2.6-x86_64.rpm "https://download.splunk.com/products/universalforwarder/releases/9.0.4/linux/splunkforwarder-9.0.4-de405f4a7979-linux-2.6-x86_64.rpm"
Install the Forwarder
ls -al
sudo yum install ./splunkforwarder-9.0.4-de405f4a7979-linux-2.6-x86_64.rpm -y
Change to the splunkforwarder bin directory and start the forwarder
NOTE: The Password must be at least 8 characters long.
Set the port for the forwarder to 9997, this is to keep splunk server from conflicting with the splunk forwarder
sudo bash
cd /opt/splunkforwarder/bin
./splunk start --accept-license --answer-yes
SplunkSetup2!Set the forwarder to forward to the splunk server on port 9997, and will need to enter username and password (change IP address with your own server IP address). When prompted for username and password, enter what you set above for username and password.
./splunk add forward-server SPLUNK-SERVER-Public-IP-Address:9997
Restart Splunk on the VM you are configuring the Forwarder
./splunk restart
Set the forwarder to monitor the /var/log/tomcat/ directory and restart
./splunk add monitor /var/log/tomcat/
Set the port for the splunk server to listen on 9997 and restart
cd /opt/splunk/bin
./splunk enable listen 9997
Step 3: View Application Logs in Splunk
Login to your Splunk Server at http://Splunk-Server-IP:8000Click on Search and Reporting -->> Data Summary -->> Select any of the displayed Environments Host to visualize App Logs SplunkSetup4!Application Log Indexed SplunkSetup3!Jenkins setup
Access Jenkins
Copy your Jenkins Public IP Address and paste on the browser = ExternalIP:8080Login to your Jenkins instance using your Shell (GitBash or your Mac Terminal)
Copy the Path from the Jenkins UI to get the Administrator Password
Run: sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Copy the password and login to Jenkins JenkinsSetup1!
Plugins: Choose Install Suggested Plugings
Provide
Username: admin
Password: admin
Name and Email can also be admin. You can use admin all, as its a poc.
Continue and Start using Jenkins JenkinsSetup2!
Plugin installations:
Click on "Manage Jenkins"
Click on "Plugin Manager"
Click "Available"
Search and Install the following Plugings "Install Without Restart"
SonarQube Scanner
Maven Integration
Pipeline Maven Integration
Maven Release Plug-In
Slack Notification
Nexus Artifact Uploader
Build Timestamp (Needed for Artifact versioning)
Once all plugins are installed, select Restart Jenkins when installation is complete and no jobs are running PluginInstallation!
Global tools configuration:
Click on Manage Jenkins -->> Global Tool Configuration JDKSetup!JDK -->> Add JDK -->> Make sure Install automatically is enabled -->>Note: By default the Install Oracle Java SE Development Kit from the website make sure to close that option by clicking on the image as shown below.JDKSetup!Click on Add installer
Select Extract .zip/.tar.gz -->> Fill the below values
Name: localJdk
Download URL for binary archive: https://download.java.net/java/GA/jdk11/13/GPL/openjdk-11.0.1_linux-x64_bin.tar.gz
Subdirectory of extracted archive: jdk-11.0.1
Git -->> Add Git -->> Install automatically(Optional) GitSetup!SonarQube Scanner -->> Add SonarQube Scanner -->> Install automatically(Optional) SonarQubeScanner!Maven -->> Add Maven -->> Make sure Install automatically is enabled -->> Install from Apache -->> Fill the below valuesName: localMaven
Version: Keep the default version as it is
Click on SAVE MavenSetup!Credentials setup(SonarQube, Nexus, Ansible and Slack):
Click on Manage Jenkins -->> Manage Credentials -->> Global credentials (unrestricted) -->> Add Credentials
SonarQube secret token (SonarQube-Token)
Generating SonarQube secret token:
Login to your SonarQube server (http://SonarServer-Sublic-IP:9000, with the credentials username: admin & password: admin)
Click on profile -->> My Account -->> Security -->> Tokens
Generate Tokens: Fill SonarQube-Token
Click on Generate
Copy the token
Store SonarQube Secret token in Jenkins:
Click on Add Credentials
Kind: Secret text!!
Secret: Fill the SonarQube token value that we have created on the SonarQube server
ID: SonarQube-Token
Description: SonarQube-Token
Click on Create
Slack secret token (slack-token)
Click on Add Credentials
Kind: Secret text
Secret: Place the Integration Token Credential ID (Note: Generate for slack setup)
ID: Slack-Token
Description: slack-token
Click on Create
Nexus Credentials (Username and Password)
Login to Nexus and Set Password
Access Nexus: http://Nexus-Pub-IP:8081/
Default Username: admin
NOTE: Login into your "Nexus" VM and "cat" the following file to get the password.
Command: sudo cat /opt/nexus/sonatype-work/nexus3/admin.password
Password: Fill In The Password and Click Sign In
Click Next -->> Provide New Password: "admin"
Configure Anonymous Access: "Enable anonymous access" -->> Finish
Nexus credentials (username & password)
Click on Add Credentials
Kind: Username with password
Username: admin
Enable Treat username as secret
Password: admin
ID: Nexus-Credential
Description: nexus-credential
Click on Create
Ansible deployment server credential (username & password)
Click on Add Credentials
Kind: Username with password
Username: ansibleadmin
Enable Treat username as secret
Password: ansibleadmin
ID: Ansible-Credential
Description: Ansible-Credential
Click on Create
SonarQubeServerSetup!
Configure system:
Click on Manage Jenkins -->> Configure System
SonarQube Servers SonarQubeServerSetup!
Click on Manage Jenkins -->> Configure System
Go to section Slack
Use new team subdomain & integration token credentials created in the above slack joining step
Workspace: Replace with Team Subdomain value (created above)
Credentials: select the slack-token credentials (created above)
Default channel / member id: #PROVIDE_YOUR_CHANNEL_NAME_HERE
Test Connection
Click on Save SlackSetup!
SonarQube Configuration
Setup SonarQube GateKeeper
Click on -->> Quality Gate SonarQubeSetup2!Click on -->> Create SonarQubeSetup2!Add a Quality Gate Condition to Validate the Code Against (Code Smells or Bugs) SonarQubeSetup3!Add Quality to SonarQube ProjectNOTE: Make sure to update the SonarQube stage in your Jenkinsfile and Test the Pipeline so your project will be visible on the SonarQube Project Dashboard.Click on Projects -->> Administration -->> Select Quality Gate SonarQubeSetup3!Setup SonarQube Webhook to Integrate Jenkins (To pass the results to Jenkins)
Still on AdministrationSelect WebhookClick on Create WebhookName: jenkinswebhook
URL: http://Jenkins-Server-Private-IP:8080/sonarqube-webhook SonarQubeSetup4!
Go ahead and Confirm in the Jenkinsfile you have the “Quality Gate Stage”. The stage code should look like the below;stage('SonarQube GateKeeper') {
    steps {
      timeout(time : 1, unit : 'HOURS'){
      waitForQualityGate abortPipeline: true
      }
   }
}
Run Your Pipeline To Test Your Quality Gate (It should PASS QG)
(OPTIONAL) FAIL Your Quality Gate: Go back to SonarQube -->> Open your Project -->> Click on Quality Gates at the top -->> Select your Project Quality Gate -->> Click EDIT -->> Change the Value to “0” -->> Update Condition
(OPTIONAL) Run/Test Your Pipeline Again and This Time Your Quality Gate Should Fail
(OPTIONAL) Go back and Update the Quality Gate value to 10. The Exercise was just to see how Quality Gate Works
Pipeline creation
Update The Jenkinsfile If NeccessaryUpdate SonarQube IP address in your JenkinsfileUpdate the SonarQube projectKey or name in your JenkinsfileUpdate your Slack Channel Name in the JenkinsfileLog into Jenkins: http://Jenkins-Public-IP:8080/
Click on New Item
Enter an item name: Jenkins-Complete-CICD-Pipeline & select the category as Pipeline
Now scroll-down and in the Pipeline section -->> Definition -->> Select Pipeline script from SCM
GitHub project: Provide Your Project Repo Git URL
GitHub hook trigger for GITScm polling: Check the box
NOTE: Make sure to also configure it on GitHub's side
SCM: Git
Repositories
Repository URL: FILL YOUR OWN REPO URL (that we created by importing in the first step)
Branch Specifier (blank for 'any'): */main
Script Path: Jenkinsfile
Save
NOTE: Make Sure Your Pipeline Succeeds Until SonarQube GateKeeper. Upload to Artifactory would fail.
TEST Pipeline
A. Pipeline Test Results
Jenkins Pipeline Job JenkinsJobResult!SonarQube Code Inspection Result SonarQubeResult!Slack Continuous Feedback Alert SlackResult!SonarQube GateKeeper Webhook Payload SonarQubeGateKeeper!B. Troubleshooting (Possible Issues You May Encounter and Suggested Solutions)
1st ISSUE: If you experience a long wait time at the level of GateKeeper, please check if your Sonar Webhook is associated with your SonarQube Project with SonarQube Results
If you check your jenkins Pipeline you'll most likely find the below message at the SonarQube GateKeper stage
JENKINS CONSOLE OUTPUTChecking status of SonarQube task 'AYfEB4IQ3rP3Y6VQ_yIa' on server 'SonarQube'
SonarQube task 'AYfEB4IQ3rP3Y6VQ_yIa' status is 'PENDING'
Nexus Configuration
Accessing Nexus:
The nexus service on port 8081. To access the nexus dashboard, visit http://Nexus-Pub-IP:8081. You will be able to see the nexus homepage as shown below.Default username: admin
Default Password: sudo cat /app/sonatype-work/nexus3/admin.password
NOTE: Once you login, you will be prompted to reset the password
Go ahead and create your Nexus Project Repositories
CREATE 1st REPO: Click on the Gear Icon -->> Repository -->> Create Repository -->> Select maven2(hosted) -->> Name: maven-project-releases -->> Create RepositoryCREATE 2nd REPO: Click Create Repository -->> Select maven2(hosted) -->> Name: maven-project-snapshots -->> Version Policy: Select Snapshot -->> Create RepositoryCREATE 3rd REPO: Click Create Repository -->> Select maven2(proxy) -->> Name: maven-project-central -->> Remote Storage: provide this link https://repo.maven.apache.org/maven2 -->> Create RepositoryCREATE 4th REPO: Click Create Repository -->> Select maven2(group) -->> Name: maven-project-group -->> Version Policy: Select Mixed -->> Assign All The Repos You Created to The Group -->> Create RepositoryOnce you select create repository and select maven2(group)NexusSetup!Update Maven POM and Integrate/Configure Nexus With Jenkins
A) Update Maven POM.xml fileUpdate the Following lines of Code (Line 32 and 36) in the maven POM file and save
<url>http://Nexus-Server-Private-IP:8081/repository/maven-project-snapshots/</url><url>http://Nexus-Server-Private-IP:8081/repository/maven-project-releases/</url>
Add the following Stage in your Jenkins pipeline config and Update the following Values (nexusUrl, repository, credentialsId, artifactId, file etc.). If necessaryThe following environment config represents the NEXUS CREDENTIAL stored in jenkins. we're pulling the credential with the use of the predefine NEXUS_CREDENTIAL_ID environment variable key. Which jenkins already understands.environment {
  WORKSPACE = "${env.WORKSPACE}"
  NEXUS_CREDENTIAL_ID = 'Nexus-Credential'
}
Here we're using the Nexus Artifact Uploader stage config to store the app artifactstage("Nexus Artifact Uploader"){
    steps{
        nexusArtifactUploader(
          nexusVersion: 'nexus3',
          protocol: 'http',
          nexusUrl: '172.31.82.36:8081',
          groupId: 'webapp',
          version: "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}",
          repository: 'maven-project-releases',  //"${NEXUS_REPOSITORY}",
          credentialsId: "${NEXUS_CREDENTIAL_ID}",
          artifacts: [
              [artifactId: 'webapp',
              classifier: '',
              file: '/var/lib/jenkins/workspace/jenkins-complete-cicd-pipeline/webapp/target/webapp.war',
              type: 'war']
          ]
        )
    }
}
After confirming all changes, go ahead and save, then push to GitHub.Test your Pipeline to Make Sure That The Artifacts Upload Stage Succeeds.Navigate to Jenkins Dashboard (Run/Test The Job) PipelineStagesArtifactSuccess!Navigate to Nexus as well to confirm that the artifact was Stored in the maven-project-releases repository ArtifactStored!Configure Ansible To Deploy to Dev, Stage and Prod
NOTE: Make sure you Assign an IAM ROLE / PROFILE with EC2 Full Access to your JENKINS server
NOTE: Update ALL Pipeline Deploy Stages with your Ansible Credentials ID (IMPORTANT)
Also Make sure the following Userdata was executed across all the Environment Deployment Nodes/Areas
#!/bin/bash
# Tomcat Server Installation
sudo su
amazon-linux-extras install tomcat8.5 -y
systemctl enable tomcat
systemctl start tomcat# Provisioning Ansible Deployer Access
useradd ansibleadmin
echo ansibleadmin | passwd ansibleadmin --stdin
sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
systemctl restart sshd
echo "ansibleadmin ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
TEST PIPELINE DEPLOYMENT
Confirm/Confirm that your deployments where all successful accross all Environments PipelineStagesCompleted!Verify/Confirm Slack Success Feedback. SlackSuccessAllStages!Confirm Access to your application: http://Dev-or-Stage-or-Prod-PubIP:8080/webapp/ FinalProductDisplay!NOTE: That By completing this project, you are now considered a Professional DevOps Engineer.
You've been able to accomplish something very unique and special which most people only dream of in their IT journey. Remmber that during an interview, you may be asked some challenging questions or be faced with a trial assignment that require you to both utilize your existing skillsets and think out of the box. During this time you must be very confident and determined in your pursuit.Never forget that you have what it takes to add more than enough VALUE to any organization out there in the industry and to STAND OUT in any interview setting no matter who is sitted on the interview seat.Congratulations Team!!!👨🏼‍💻 Congratulations!!!👨🏼‍💻Use an agent called agent1 and trivyExplain step by step how we can achieve the project aboveShow moreComplete End-to-End Jenkins CI/CD Pipeline with Ansible, Trivy & Agent Setup
I'll guide you through implementing this comprehensive CI/CD pipeline with a dedicated Jenkins agent and Trivy integration.

Phase 1: Infrastructure Setup (9 EC2 Instances)
Step 1: Launch Jenkins Master Server
Instance Configuration:

Name: Jenkins-Master
AMI: Amazon Linux 2
Instance Type: t2.medium
Security Group:

Port 22 (SSH) - Your IP
Port 8080 (Jenkins) - 0.0.0.0/0
Port 50000 (Jenkins Agent) - agent1 security group


User Data:

bash#!/bin/bash
sudo yum update -y
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo yum upgrade -y
sudo amazon-linux-extras install java-openjdk11 -y
sudo yum install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins

# Install Git
sudo yum install git -y

echo "Jenkins Master installation complete!"
Step 2: Launch Jenkins Agent (agent1)
Instance Configuration:

Name: agent1
AMI: Amazon Linux 2
Instance Type: t2.medium
Security Group:

Port 22 (SSH) - Jenkins Master IP
Port 9100 (Node Exporter) - Prometheus IP


User Data:

bash#!/bin/bash
# Update system
sudo yum update -y

# Install Java (required for Jenkins agent)
sudo amazon-linux-extras install java-openjdk11 -y

# Install Maven
cd /opt
sudo wget https://dlcdn.apache.org/maven/maven-3/3.9.5/binaries/apache-maven-3.9.5-bin.tar.gz
sudo tar -xvzf apache-maven-3.9.5-bin.tar.gz
sudo mv apache-maven-3.9.5 maven
sudo rm apache-maven-3.9.5-bin.tar.gz

# Set Maven environment variables
echo "export M2_HOME=/opt/maven" >> /etc/profile.d/maven.sh
echo "export PATH=\${M2_HOME}/bin:\${PATH}" >> /etc/profile.d/maven.sh
source /etc/profile.d/maven.sh

# Install Git
sudo yum install git -y

# Install Ansible
sudo amazon-linux-extras install ansible2 -y

# Install Docker (for Trivy container scanning)
sudo yum install docker -y
sudo systemctl enable docker
sudo systemctl start docker

# Install Trivy
sudo rpm -ivh https://github.com/aquasecurity/trivy/releases/download/v0.48.0/trivy_0.48.0_Linux-64bit.rpm

# Create jenkins user and setup
sudo useradd -m -s /bin/bash jenkins
sudo usermod -aG docker jenkins

# Create workspace directory
sudo mkdir -p /home/jenkins/workspace
sudo chown -R jenkins:jenkins /home/jenkins

# Install unzip and jq
sudo yum install unzip jq -y

echo "Agent1 setup complete!"
Step 3: Launch Remaining Infrastructure
Launch the following instances as specified in the original guide:
3.1 SonarQube Server

Ubuntu 20.04, t2.medium
Ports: 9000, 9100, 22
User data from: jenkins-install.sh link

3.2 Nexus Server

Amazon Linux 2, t2.medium
Ports: 8081, 9100, 22
User data from: nexus-install.sh link

3.3 Application Servers (Dev, Stage, Prod)

3x Amazon Linux 2, t2.micro each
Ports: 8080, 9100, 9997, 22
User data from: tomcat-ssh-configure.sh link

3.4 Prometheus Server

Ubuntu 20.04, t2.micro
Ports: 9090, 22

3.5 Grafana Server

Ubuntu 20.04, t2.micro
Ports: 3000, 22

3.6 Splunk Server

Amazon Linux 2, t2.micro
Ports: 8000, 9997, 9100, 22

Total: 9 EC2 Instances

Phase 2: Configure Jenkins Master and Agent Connection
Step 4: Initial Jenkins Master Setup

Access Jenkins Master:

bash# Get initial admin password
ssh -i your-key.pem ec2-user@<Jenkins-Master-IP>
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

2. **Open browser**: `http://<Jenkins-Master-IP>:8080`

3. **Complete setup wizard:**
   - Paste admin password
   - Install suggested plugins
   - Create admin user: admin/admin
   - Save and continue

### Step 5: Configure Jenkins Agent (agent1)

**On Jenkins Master UI:**

1. **Navigate to**: Manage Jenkins → Manage Nodes and Clouds → New Node

2. **Configure Node:**
   - **Node name**: agent1
   - **Type**: Permanent Agent
   - Click **OK**

3. **Node Configuration:**
```
   Number of executors: 2
   Remote root directory: /home/jenkins
   Labels: agent1 maven ansible trivy
   Usage: Use this node as much as possible
   Launch method: Launch agents via SSH

SSH Configuration:

Host: <agent1-Private-IP>
Credentials: Click Add → Jenkins

Kind: SSH Username with private key
ID: agent1-ssh-key
Username: jenkins
Private Key: Enter directly → Paste your .pem key content
Click Add


Host Key Verification Strategy: Non verifying Verification Strategy
Availability: Keep this agent online as much as possible


Click Save
Verify Connection:

Go back to Nodes list
Click on agent1
Should show "Agent successfully connected and online"



Step 6: Setup SSH Keys for Ansible Deployment
On agent1 server:
bashssh -i your-key.pem ec2-user@<agent1-IP>

# Switch to jenkins user
sudo su - jenkins

# Generate SSH key
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa -N ""

# Display public key (save this)
cat ~/.ssh/id_rsa.pub
On each App Server (Dev, Stage, Prod):
bashssh -i your-key.pem ec2-user@<Dev/Stage/Prod-IP>

# Switch to ansibleadmin
sudo su - ansibleadmin

# Create .ssh directory if not exists
mkdir -p ~/.ssh
chmod 700 ~/.ssh

# Add agent1 public key to authorized_keys
vi ~/.ssh/authorized_keys
# Paste the public key from agent1
# Save and exit

# Set permissions
chmod 600 ~/.ssh/authorized_keys
Test SSH connection from agent1:
bash# On agent1 as jenkins user
ssh ansibleadmin@<Dev-Private-IP>
# Should connect without password
exit

ssh ansibleadmin@<Stage-Private-IP>
exit

ssh ansibleadmin@<Prod-Private-IP>
exit

Phase 3: Configure Trivy on agent1
Step 7: Setup Trivy Scanning Environment
SSH into agent1:
bashssh -i your-key.pem ec2-user@<agent1-IP>
sudo su - jenkins
Create Trivy directory structure:
bashsudo mkdir -p /opt/trivy/{scripts,reports,configs}
sudo chown -R jenkins:jenkins /opt/trivy
Create Trivy scan script:
bashsudo vi /opt/trivy/scripts/comprehensive-scan.sh
bash#!/bin/bash
# Comprehensive Trivy Security Scan

set -e

WORKSPACE=$1
BUILD_ID=${2:-"unknown"}
REPORT_DIR="/opt/trivy/reports"
TIMESTAMP=$(date +%Y%m%d_%H%M%S)

echo "========================================"
echo "Starting Trivy Security Scan"
echo "Build ID: ${BUILD_ID}"
echo "Workspace: ${WORKSPACE}"
echo "========================================"

mkdir -p ${REPORT_DIR}/{json,html,sarif}

# Update Trivy database
echo "[1/5] Updating Trivy vulnerability database..."
trivy image --download-db-only

# Scan for secrets
echo "[2/5] Scanning for secrets..."
trivy fs \
  --scanners secret \
  --severity HIGH,CRITICAL \
  --format json \
  --output ${REPORT_DIR}/json/secrets-${TIMESTAMP}.json \
  ${WORKSPACE}

SECRET_COUNT=$(jq '[.Results[]?.Secrets[]?] | length' ${REPORT_DIR}/json/secrets-${TIMESTAMP}.json 2>/dev/null || echo 0)
echo "Found ${SECRET_COUNT} secrets"

if [ "${SECRET_COUNT}" -gt 0 ]; then
  echo "ERROR: Secrets detected in source code!"
  trivy fs --scanners secret --format table ${WORKSPACE}
  exit 1
fi

# Scan for misconfigurations
echo "[3/5] Scanning for misconfigurations..."
trivy config \
  --severity HIGH,CRITICAL \
  --format json \
  --output ${REPORT_DIR}/json/config-${TIMESTAMP}.json \
  ${WORKSPACE}

# Scan dependencies
echo "[4/5] Scanning dependencies..."
trivy fs \
  --scanners vuln \
  --severity HIGH,CRITICAL \
  --format json \
  --output ${REPORT_DIR}/json/dependencies-${TIMESTAMP}.json \
  --skip-dirs target \
  ${WORKSPACE}

# Scan WAR artifact
echo "[5/5] Scanning WAR artifact..."
WAR_FILE="${WORKSPACE}/webapp/target/webapp.war"

if [ -f "${WAR_FILE}" ]; then
  TEMP_DIR="/tmp/trivy-scan-${TIMESTAMP}"
  mkdir -p ${TEMP_DIR}
  
  cd ${TEMP_DIR}
  unzip -q ${WAR_FILE}
  
  trivy fs \
    --severity HIGH,CRITICAL \
    --format json \
    --output ${REPORT_DIR}/json/artifact-${TIMESTAMP}.json \
    ${TEMP_DIR}
  
  # Generate HTML report
  trivy fs \
    --severity HIGH,CRITICAL \
    --format template \
    --template "@contrib/html.tpl" \
    --output ${REPORT_DIR}/html/trivy-report-${TIMESTAMP}.html \
    ${TEMP_DIR} 2>/dev/null || echo "HTML template not found, skipping HTML report"
  
  rm -rf ${TEMP_DIR}
  
  # Parse results
  CRITICAL=$(jq '[.Results[]?.Vulnerabilities[]? | select(.Severity=="CRITICAL")] | length' ${REPORT_DIR}/json/artifact-${TIMESTAMP}.json)
  HIGH=$(jq '[.Results[]?.Vulnerabilities[]? | select(.Severity=="HIGH")] | length' ${REPORT_DIR}/json/artifact-${TIMESTAMP}.json)
  
  echo ""
  echo "========================================"
  echo "Scan Results:"
  echo "  Critical: ${CRITICAL}"
  echo "  High: ${HIGH}"
  echo "========================================"
  
  # Fail if too many critical vulnerabilities
  if [ "${CRITICAL}" -gt 10 ]; then
    echo "ERROR: Too many critical vulnerabilities (${CRITICAL})"
    exit 1
  fi
  
  echo "✅ Security scan passed"
  exit 0
else
  echo "WARNING: WAR file not found at ${WAR_FILE}"
  exit 0
fi
Make script executable:
bashsudo chmod +x /opt/trivy/scripts/comprehensive-scan.sh
sudo chown -R jenkins:jenkins /opt/trivy

Phase 4: Setup Ansible on agent1
Step 8: Configure Ansible Inventory and Playbooks
Create Ansible directory structure:
bashsudo su - jenkins
mkdir -p /home/jenkins/ansible/{playbooks,inventory,roles}
cd /home/jenkins/ansible
Create inventory file:
bashvi inventory/hosts
ini[dev]
dev-server ansible_host=<Dev-Private-IP> ansible_user=ansibleadmin

[stage]
stage-server ansible_host=<Stage-Private-IP> ansible_user=ansibleadmin

[prod]
prod-server ansible_host=<Prod-Private-IP> ansible_user=ansibleadmin

[all:vars]
ansible_ssh_private_key_file=/home/jenkins/.ssh/id_rsa
ansible_ssh_common_args='-o StrictHostKeyChecking=no'
tomcat_home=/opt/apache-tomcat-8.5.82
tomcat_user=tomcat
app_name=webapp
Create deployment playbook:
bashvi playbooks/deploy-webapp.yml
yaml---
- name: Deploy Java Web Application
  hosts: "{{ target_env }}"
  become: yes
  
  vars:
    artifact_path: "{{ workspace }}/webapp/target/webapp.war"
    backup_dir: "{{ tomcat_home }}/backup"
    
  tasks:
    - name: Create backup directory
      file:
        path: "{{ backup_dir }}"
        state: directory
        owner: "{{ tomcat_user }}"
        group: "{{ tomcat_user }}"
    
    - name: Backup existing application
      copy:
        src: "{{ tomcat_home }}/webapps/{{ app_name }}.war"
        dest: "{{ backup_dir }}/{{ app_name }}-{{ ansible_date_time.epoch }}.war"
        remote_src: yes
      when: ansible_stat.exists
      ignore_errors: yes
    
    - name: Stop Tomcat
      systemd:
        name: tomcat
        state: stopped
    
    - name: Remove old application
      file:
        path: "{{ item }}"
        state: absent
      loop:
        - "{{ tomcat_home }}/webapps/{{ app_name }}"
        - "{{ tomcat_home }}/webapps/{{ app_name }}.war"
    
    - name: Deploy new application
      copy:
        src: "{{ artifact_path }}"
        dest: "{{ tomcat_home }}/webapps/{{ app_name }}.war"
        owner: "{{ tomcat_user }}"
        group: "{{ tomcat_user }}"
        mode: '0644'
    
    - name: Start Tomcat
      systemd:
        name: tomcat
        state: started
        enabled: yes
    
    - name: Wait for application to be ready
      wait_for:
        port: 8080
        delay: 10
        timeout: 60
    
    - name: Verify application is responding
      uri:
        url: "http://localhost:8080/{{ app_name }}/"
        status_code: 200
      register: result
      until: result.status == 200
      retries: 10
      delay: 5
Create health check playbook:
bashvi playbooks/health-check.yml
yaml---
- name: Application Health Check
  hosts: "{{ target_env }}"
  become: yes
  
  tasks:
    - name: Check Tomcat service
      systemd:
        name: tomcat
      register: tomcat_status
    
    - name: Verify Tomcat is listening
      wait_for:
        port: 8080
        timeout: 5
    
    - name: Check application endpoint
      uri:
        url: "http://localhost:8080/{{ app_name }}/"
        status_code: 200
      register: app_check
    
    - name: Display health status
      debug:
        msg:
          - "Tomcat: {{ tomcat_status.status.ActiveState }}"
          - "Application: {{ app_check.status }}"
Test Ansible connectivity:
bashansible all -i inventory/hosts -m ping

Phase 5: Configure Jenkins Pipeline
Step 9: Install Required Jenkins Plugins
On Jenkins Master:

Go to: Manage Jenkins → Manage Plugins → Available
Install these plugins (without restart):

Pipeline
Pipeline: Stage View
Git
Maven Integration
SonarQube Scanner
Nexus Artifact Uploader
Slack Notification
Build Timestamp
SSH Agent
Credentials Binding


Check: "Restart Jenkins when no jobs running"

Step 10: Configure Global Tool Configuration
Go to: Manage Jenkins → Global Tool Configuration
1. JDK Configuration:

Click Add JDK
Name: JDK11
Uncheck "Install automatically"
JAVA_HOME: /usr/lib/jvm/java-11-openjdk

2. Git Configuration:

Usually auto-detected
If not, add Git with path: /usr/bin/git

3. Maven Configuration:

Click Add Maven
Name: Maven3
Uncheck "Install automatically"
MAVEN_HOME: /opt/maven (on agent1)

4. SonarQube Scanner:

Click Add SonarQube Scanner
Name: SonarQube-Scanner
Check "Install automatically"
Version: Latest

Click Save
Step 11: Configure Jenkins Credentials
Go to: Manage Jenkins → Manage Credentials → Global → Add Credentials
Create these credentials:
1. GitHub Credentials (if private repo):

Kind: Username with password
Username: your-github-username
Password: your-github-token
ID: github-credentials

2. SonarQube Token:

First generate token in SonarQube (covered later)
Kind: Secret text
Secret: <SonarQube-token>
ID: SonarQube-Token

3. Nexus Credentials:

Kind: Username with password
Username: admin
Password: admin
ID: Nexus-Credential

4. Ansible Credentials:

Kind: Username with password
Username: ansibleadmin
Password: ansibleadmin
ID: Ansible-Credential

5. Slack Token:

Kind: Secret text
Secret: <Slack-integration-token>
ID: Slack-Token


Phase 6: Configure Supporting Tools
Step 12: Configure SonarQube
Access SonarQube:
bashhttp://<SonarQube-Public-IP>:9000
# Login: admin/admin (change password on first login)
1. Generate Token:

Click profile → My Account → Security → Tokens
Name: Jenkins-Token
Click Generate
Copy token and add to Jenkins credentials

2. Create Quality Gate:

Quality Gates → Create
Name: Jenkins-Pipeline-QG
Add Condition:

Metric: Bugs
Operator: is greater than
Value: 10


Click Add Condition

3. Create Webhook:

Administration → Configuration → Webhooks → Create
Name: Jenkins-Webhook
URL: http://<Jenkins-Master-Private-IP>:8080/sonarqube-webhook/
Click Create

Step 13: Configure Nexus
Access Nexus:
bashhttp://<Nexus-Public-IP>:8081
1. Get Initial Password:
bashssh -i your-key.pem ec2-user@<Nexus-IP>
sudo cat /opt/nexus/sonatype-work/nexus3/admin.password
2. Login and change password to: admin
3. Create Repositories:

Repository 1 (Releases):

Create repository → maven2 (hosted)
Name: maven-project-releases
Version policy: Release
Create


Repository 2 (Snapshots):

Create repository → maven2 (hosted)
Name: maven-project-snapshots
Version policy: Snapshot
Create


Repository 3 (Proxy):

Create repository → maven2 (proxy)
Name: maven-project-central
Remote storage: https://repo.maven.apache.org/maven2
Create


Repository 4 (Group):

Create repository → maven2 (group)
Name: maven-project-group
Add all above repositories to group
Create



Step 14: Configure Slack
1. Join Workspace:

Go to: https://join.slack.com/t/realworldcicdproject/shared_invite/zt-1tryd7x1v-g8a~zEJBKKchVvvK87jkeQ

2. Create Channel:

Create private channel: yourname-jenkins-cicd-alerts

3. Add Jenkins App:

Channel → Integrations → Add apps
Search "Jenkins CI" → Add to Slack
Select your channel
Copy the Integration Token Credential ID
Save settings

4. Configure in Jenkins:

Manage Jenkins → Configure System
Scroll to Slack section:

Workspace: realworldcicdproject
Credential: Select Slack-Token
Default channel: #yourname-jenkins-cicd-alerts
Test Connection


Save

Step 15: Configure SonarQube Server in Jenkins
Go to: Manage Jenkins → Configure System
SonarQube servers section:

Check "Environment variables"
Add SonarQube:

Name: SonarQube
Server URL: http://<SonarQube-Private-IP>:9000
Server authentication token: Select SonarQube-Token


Save


Phase 7: Setup Monitoring Stack
Step 16: Configure Prometheus
SSH into Prometheus server:
bashssh -i your-key.pem ubuntu@<Prometheus-IP>

# Clone repo
git clone https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
cd realworld-cicd-pipeline-project
git checkout prometheus-and-grafana

# Install Prometheus
chmod +x install-prometheus.sh
./install-prometheus.sh

# Verify
sudo systemctl status prometheus
Step 17: Install Node Exporter on All Servers
On each server (Dev, Stage, Prod, agent1, Jenkins-Master, Nexus, SonarQube):
bashssh -i your-key.pem <user>@<server-IP>

# Install git if not present
sudo yum install git -y  # For Amazon Linux
# OR
sudo apt install git -y  # For Ubuntu

# Clone repo
git clone https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
cd realworld-cicd-pipeline-project
git checkout prometheus-and-grafana

# Install Node Exporter
chmod +x install-node-exporter.sh
./install-node-exporter.sh

# Verify
sudo systemctl status node_exporter

# Test
curl http://localhost:9100/metrics
Step 18: Configure Prometheus Targets
On Prometheus server:
bashsudo vi /etc/prometheus/prometheus.yml
Add all node_exporter targets:
yamlscrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']
  
  - job_name: 'node_exporters'
    static_configs:
      - targets:
        - '<Dev-Private-IP>:9100'
        - '<Stage-Private-IP>:9100'
        - '<Prod-Private-IP>:9100'
        - '<agent1-Private-IP>:9100'
        - '<Jenkins-Master-Private-IP>:9100'
        - '<Nexus-Private-IP>:9100'
        - '<SonarQube-Private-IP>:9100'
Restart Prometheus:
bashsudo systemctl restart prometheus
Verify targets:

Go to: http://<Prometheus-IP>:9090
Status → Targets
All should show UP

Step 19: Configure Grafana
SSH into Grafana server:
bashssh -i your-key.pem ubuntu@<Grafana-IP>

# Clone and install
git clone https://github.com/awanmbandi/realworld-cicd-pipeline-project.git
cd realworld-cicd-pipeline-project
git checkout prometheus-and-grafana
chmod +x install-grafana.sh
./install-grafana.sh

# Verify
sudo systemctl status grafana-server
Access Grafana:

URL: http://<Grafana-IP>:3000
Login: admin/admin
Change password: admin

Add Prometheus Data Source:

Configuration → Data Sources → Add data source
Select Prometheus
URL: http://<Prometheus-Private-IP>:9090
Click Save & Test

Import Dashboard:

Create → Import
Dashboard ID: 1860
Click Load
Select Prometheus data source
Click Import


Phase 8: Setup Splunk
Step 20: Configure Splunk Server
SSH into Splunk server:
bashssh -i your-key.pem ec2-user@<Splunk-IP>

# Download Splunk
wget -O splunk-9.0.4.1-419ad9369127-linux-2.6-x86_64.rpm \
"https://download.splunk.com/products/splunk/releases/9.0.4.1/linux/splunk-9.0.4.1-419ad9369127-linux-2.6-x86_64.rpm"

# Install
sudo yum install ./splunk-9.0.4.1-419ad9369127-linux-2.6-x86_64.rpm -y

# Start Splunk
sudo bash
cd /opt/splunk/bin
./splunk start --accept-license --answer-yes

# Create admin credentials (password must be 8+ characters)
# Username: admin
# Password: Admin@123
Configure Splunk:

Access: http://<Splunk-IP>:8000
Login with credentials
Settings → Server Settings → General Settings
Change "Pause indexing if free disk space" from 5000 to 50
Save

Enable listening port:
bashcd /opt/splunk/bin
./splunk enable listen 9997
./splunk restart
Step 21: Install Splunk Forwarders on App Servers
On each app server (Dev, Stage, Prod):
bashssh -i your-key.pem ec2-user@<App-Server-IP>

# Download forwarder
wget -O splunkforwarder-9.0.4-de405f4a7979-linux-2.6-x86_64.rpm \
"https://download.splunk.com/products/universalforwarder/releases/9.0.4/linux/splunkforwarder-9.0.4-de405f4a7979-linux-2.6-x86_64.rpm"

# Install
sudo yum install ./splunkforwarder-9.0.4-de405f4a7979-linux-2.6-x86_64.rpm -y

# Configure
sudo bash
cd /opt/splunkforwarder/bin
./splunk start --accept-license --answer-yes

# Same credentials as Splunk server
# Username: admin
# Password: Admin@123

# Add forward server
./splunk add forward-server <Splunk-Server-Public-IP>:9997

# Add monitor for Tomcat logs
./splunk add monitor /var/log/tomcat/

# Restart
./splunk restart

Phase 9: Create and Configure Pipeline
Step 22: Fork/Create GitHub Repository

Go to: https://github.com/awanmbandi/realworld-cicd-pipeline-project
Click Fork to your account
Clone to your local machine:

bashgit clone https://github.com/YOUR-USERNAME/realworld-cicd-pipeline-project.git
cd realworld-cicd-pipeline-project
Step 23: Update Project Configuration Files
Update pom.xml (lines 32 and 36):
bashvi pom.xml
xml<distributionManagement>
    <repository>
        <id>maven-project-releases</id>
        <url>http://<Nexus-Private-IP>:8081/repository/maven-project-releases/</url>
    </repository>
    <snapshotRepository>
        <id>maven-project-snapshots</id>
        <url>http://<Nexus-Private-IP>:8081/repository/maven-project-snapshots/</url>
    </snapshotRepository>
</distributionManagement>
Step 24: Create Complete Jenkinsfile
Create Jenkinsfile in repository root:
bashvi Jenkinsfile
groovypipeline {
    agent {
        label 'agent1'
    }
    
    tools {
        maven 'Maven3'
        jdk 'JDK11'
    }
    
    environment {
        WORKSPACE = "${env.WORKSPACE}"
        BUILD_TIMESTAMP = new Date().format('yyyyMMdd-HHmmss')
        NEXUS_CREDENTIAL_ID = 'Nexus-Credential'
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }
    
    stages {
        
        stage('Checkout Code') {
            steps {
                echo "Checking out code from GitHub..."
                checkout scm
            }
        }
        
        stage('Trivy - Update Database') {
            steps {
                echo "Updating Trivy vulnerability database..."
                sh 'trivy image --download-db-only'
            }
        }
        
        stage('Trivy - Filesystem Scan') {
            steps {
                echo "Running Trivy filesystem scan..."
                sh """
                    trivy fs \
                      --severity HIGH,CRITICAL \
                      --format table \
                      ${WORKSPACE}
                """
            }
        }
        
        stage('Maven Build') {
            steps {
                echo "Building application with Maven..."
                sh 'mvn clean install'
            }
        }
        
        stage('Unit Tests') {
            steps {
                echo "Running unit tests..."
                sh 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
        
        stage('Checkstyle Analysis') {
            steps {
                echo "Running Checkstyle analysis..."
                sh 'mvn checkstyle:checkstyle'
            }
        }
        
        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool 'SonarQube-Scanner'
            }
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh """
                        ${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=maven-project \
                        -Dsonar.projectName=maven-project \
                        -Dsonar.projectVersion=1.0 \
                        -Dsonar.sources=src/ \
                        -Dsonar.java.binaries=target/classes/ \
                        -Dsonar.junit.reportsPath=target/surefire-reports/ \
                        -Dsonar.jacoco.reportsPath=RetryEContinuetarget/jacoco.exec 
-Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml
"""
}
}
}
    stage('SonarQube Quality Gate') {
        steps {
            echo "Waiting for SonarQube Quality Gate..."
            timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
            }
        }
    }
    
    stage('Trivy - Comprehensive Security Scan') {
        steps {
            echo "Running comprehensive Trivy security scan..."
            sh """
                /opt/trivy/scripts/comprehensive-scan.sh ${WORKSPACE} ${BUILD_ID}
            """
        }
        post {
            always {
                archiveArtifacts artifacts: '/opt/trivy/reports/**/*',
                               fingerprint: true,
                               allowEmptyArchive: true
            }
        }
    }
    
    stage('Upload to Nexus') {
        steps {
            echo "Uploading artifact to Nexus Repository..."
            nexusArtifactUploader(
                nexusVersion: 'nexus3',
                protocol: 'http',
                nexusUrl: '<Nexus-Private-IP>:8081',
                groupId: 'webapp',
                version: "${env.BUILD_ID}-${BUILD_TIMESTAMP}",
                repository: 'maven-project-releases',
                credentialsId: "${NEXUS_CREDENTIAL_ID}",
                artifacts: [
                    [
                        artifactId: 'webapp',
                        classifier: '',
                        file: 'webapp/target/webapp.war',
                        type: 'war'
                    ]
                ]
            )
        }
    }
    
    stage('Deploy to Dev') {
        steps {
            echo "Deploying to Development Environment..."
            script {
                sh """
                    cd /home/jenkins/ansible
                    ansible-playbook playbooks/deploy-webapp.yml \
                      -i inventory/hosts \
                      -e "target_env=dev" \
                      -e "workspace=${WORKSPACE}" \
                      -vv
                """
            }
        }
    }
    
    stage('Health Check - Dev') {
        steps {
            echo "Running health check on Dev..."
            sh """
                cd /home/jenkins/ansible
                ansible-playbook playbooks/health-check.yml \
                  -i inventory/hosts \
                  -e "target_env=dev"
            """
        }
    }
    
    stage('Deploy to Stage') {
        steps {
            echo "Deploying to Staging Environment..."
            script {
                sh """
                    cd /home/jenkins/ansible
                    ansible-playbook playbooks/deploy-webapp.yml \
                      -i inventory/hosts \
                      -e "target_env=stage" \
                      -e "workspace=${WORKSPACE}" \
                      -vv
                """
            }
        }
    }
    
    stage('Health Check - Stage') {
        steps {
            echo "Running health check on Stage..."
            sh """
                cd /home/jenkins/ansible
                ansible-playbook playbooks/health-check.yml \
                  -i inventory/hosts \
                  -e "target_env=stage"
            """
        }
    }
    
    stage('Approval for Production') {
        steps {
            timeout(time: 1, unit: 'HOURS') {
                input message: 'Deploy to Production?',
                      ok: 'Deploy',
                      submitter: 'admin'
            }
        }
    }
    
    stage('Deploy to Production') {
        steps {
            echo "Deploying to Production Environment..."
            script {
                sh """
                    cd /home/jenkins/ansible
                    ansible-playbook playbooks/deploy-webapp.yml \
                      -i inventory/hosts \
                      -e "target_env=prod" \
                      -e "workspace=${WORKSPACE}" \
                      -vv
                """
            }
        }
    }
    
    stage('Health Check - Production') {
        steps {
            echo "Running health check on Production..."
            sh """
                cd /home/jenkins/ansible
                ansible-playbook playbooks/health-check.yml \
                  -i inventory/hosts \
                  -e "target_env=prod"
            """
        }
    }
}

post {
    always {
        cleanWs()
    }
    
    success {
        slackSend(
            channel: '#yourname-jenkins-cicd-alerts',
            color: 'good',
            message: """
            ✅ *BUILD SUCCESS*
            Job: ${env.JOB_NAME}
            Build Number: ${env.BUILD_NUMBER}
            Duration: ${currentBuild.durationString}
            
            📊 *Deployment Status:*
            • Dev: ✅ Deployed & Healthy
            • Stage: ✅ Deployed & Healthy
            • Production: ✅ Deployed & Healthy
            
            🔒 *Security Scan:* Passed
            ✨ *Quality Gate:* Passed
            
            👉 <${env.BUILD_URL}|View Build Details>
            """
        )
    }
    
    failure {
        slackSend(
            channel: '#yourname-jenkins-cicd-alerts',
            color: 'danger',
            message: """
            ❌ *BUILD FAILED*
            Job: ${env.JOB_NAME}
            Build Number: ${env.BUILD_NUMBER}
            Failed Stage: ${env.STAGE_NAME}
            
            ⚠️ *Action Required*
            Please check the console output and logs.
            
            👉 <${env.BUILD_URL}console|View Console Output>
            """
        )
    }
}
}

**Important: Update these values in Jenkinsfile:**
- Replace `<Nexus-Private-IP>` with actual Nexus private IP
- Replace `#yourname-jenkins-cicd-alerts` with your actual Slack channel name

### Step 25: Push Code to GitHub
```bash
git add .
git commit -m "Initial pipeline setup with Trivy and Ansible on agent1"
git push origin main
```

---

## **Phase 10: Create Jenkins Pipeline Job**

### Step 26: Configure Pipeline in Jenkins

**On Jenkins Master:**

1. **Click** "New Item"

2. **Configure Job:**
   - **Name**: `Complete-CICD-Pipeline`
   - **Type**: Pipeline
   - Click **OK**

3. **General Settings:**
   - ✅ **GitHub project**
   - Project URL: `https://github.com/YOUR-USERNAME/realworld-cicd-pipeline-project/`

4. **Build Triggers:**
   - ✅ **GitHub hook trigger for GITScm polling**

5. **Pipeline Configuration:**
   - **Definition**: Pipeline script from SCM
   - **SCM**: Git
   - **Repository URL**: `https://github.com/YOUR-USERNAME/realworld-cicd-pipeline-project.git`
   - **Credentials**: Select if private repo (or leave none for public)
   - **Branch Specifier**: `*/main`
   - **Script Path**: `Jenkinsfile`

6. **Click Save**

### Step 27: Configure GitHub Webhook

**In your GitHub repository:**

1. Go to **Settings** → **Webhooks** → **Add webhook**

2. **Configure:**
   - **Payload URL**: `http://<Jenkins-Master-Public-IP>:8080/github-webhook/`
   - **Content type**: application/json
   - **Which events**: Just the push event
   - ✅ Active

3. **Click** "Add webhook"

4. **Verify**: Green checkmark should appear

---

## **Phase 11: Testing and Validation**

### Step 28: Initial Pipeline Test

**Trigger the pipeline:**

1. **In Jenkins**, click on your pipeline
2. **Click** "Build Now"
3. **Monitor** the execution

**Expected Stage Flow:**
✅ Checkout Code
✅ Trivy - Update Database
✅ Trivy - Filesystem Scan
✅ Maven Build
✅ Unit Tests
✅ Checkstyle Analysis
✅ SonarQube Analysis
✅ SonarQube Quality Gate (may take time on first run)
✅ Trivy - Comprehensive Security Scan
✅ Upload to Nexus
✅ Deploy to Dev
✅ Health Check - Dev
✅ Deploy to Stage
✅ Health Check - Stage
⏸️ Approval for Production (manual approval needed)
✅ Deploy to Production (after approval)
✅ Health Check - Production

### Step 29: Verify Each Component

**1. Verify agent1 is executing jobs:**
```bash
# On Jenkins, go to Manage Jenkins → Nodes
# Click on agent1
# Should show "In use" or recent activity
```

**2. Verify Trivy scans:**
```bash
# SSH to agent1
ssh -i your-key.pem ec2-user@<agent1-IP>
sudo su - jenkins
ls -la /opt/trivy/reports/
# Should see scan reports
```

**3. Verify SonarQube analysis:**
- Go to `http://<SonarQube-IP>:9000`
- Click **Projects**
- Should see `maven-project` with analysis results

**4. Verify Nexus artifact:**
- Go to `http://<Nexus-IP>:8081`
- Browse → `maven-project-releases`
- Should see uploaded WAR file

**5. Verify Deployments:**
```bash
# Dev Environment
curl http://<Dev-Public-IP>:8080/webapp/

# Stage Environment
curl http://<Stage-Public-IP>:8080/webapp/

# Production Environment (after approval)
curl http://<Prod-Public-IP>:8080/webapp/
```

**6. Verify Ansible execution:**
```bash
# On agent1
ssh -i your-key.pem ec2-user@<agent1-IP>
sudo su - jenkins

# Check Ansible connectivity
cd /home/jenkins/ansible
ansible all -i inventory/hosts -m ping
# Should show SUCCESS for all hosts
```

**7. Verify Monitoring:**
- **Prometheus**: `http://<Prometheus-IP>:9090/targets`
  - All targets should be **UP**
- **Grafana**: `http://<Grafana-IP>:3000`
  - Select dashboard
  - Choose host from dropdown
  - Should see metrics

**8. Verify Logging:**
- **Splunk**: `http://<Splunk-IP>:8000`
- Search: `index=* source="/var/log/tomcat/*"`
- Should see logs from Dev, Stage, Prod

**9. Verify Slack notifications:**
- Check your Slack channel
- Should see build notifications

---

## **Phase 12: Complete Documentation**

### Step 30: Create Comprehensive Documentation

**Create README in your repository:**
```bash
vi README.md
```
```markdown
# Enterprise CI/CD Pipeline with Jenkins, Ansible & Trivy

## Architecture Overview
```
┌─────────────────────────────────────────────────────────────┐
│                   COMPLETE CI/CD PIPELINE                    │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  Developer → GitHub → Webhook → Jenkins Master              │
│                           ↓                                  │
│                      Jenkins Agent (agent1)                  │
│                           ↓                                  │
│  ┌────────────────────────────────────────────┐            │
│  │  1. Checkout Code                          │            │
│  │  2. Trivy Security Scan (Filesystem)       │            │
│  │  3. Maven Build                            │            │
│  │  4. Unit Tests                             │            │
│  │  5. Checkstyle Analysis                    │            │
│  │  6. SonarQube Analysis                     │            │
│  │  7. SonarQube Quality Gate                 │            │
│  │  8. Trivy Comprehensive Scan (WAR)         │            │
│  │  9. Upload to Nexus                        │            │
│  │ 10. Ansible Deploy to Dev                  │            │
│  │ 11. Health Check - Dev                     │            │
│  │ 12. Ansible Deploy to Stage                │            │
│  │ 13. Health Check - Stage                   │            │
│  │ 14. Manual Approval                        │            │
│  │ 15. Ansible Deploy to Production           │            │
│  │ 16. Health Check - Production              │            │
│  └────────────────────────────────────────────┘            │
│                           ↓                                  │
│     Monitoring (Prometheus + Grafana)                       │
│     Logging (Splunk)                                        │
│     Notifications (Slack)                                   │
│                                                              │
└─────────────────────────────────────────────────────────────┘
Infrastructure Components
Core Pipeline Infrastructure (9 EC2 Instances)

Jenkins-Master (Amazon Linux 2, t2.medium)

Jenkins orchestration server
Ports: 8080, 50000, 22


agent1 (Amazon Linux 2, t2.medium)

Jenkins build agent
Maven, Ansible, Trivy, Docker installed
All pipeline stages execute here
Ports: 22, 9100


SonarQube (Ubuntu 20.04, t2.medium)

Code quality analysis
Ports: 9000, 9100, 22


Nexus (Amazon Linux 2, t2.medium)

Artifact repository
Ports: 8081, 9100, 22


Dev-Env (Amazon Linux 2, t2.micro)

Development environment
Tomcat 8.5
Ports: 8080, 9100, 9997, 22


Stage-Env (Amazon Linux 2, t2.micro)

Staging environment
Tomcat 8.5
Ports: 8080, 9100, 9997, 22


Prod-Env (Amazon Linux 2, t2.micro)

Production environment
Tomcat 8.5
Ports: 8080, 9100, 9997, 22


Prometheus (Ubuntu 20.04, t2.micro)

Metrics collection
Ports: 9090, 22


Grafana (Ubuntu 20.04, t2.micro)

Metrics visualization
Ports: 3000, 22


Splunk-Server (Amazon Linux 2, t2.micro)

Log aggregation
Ports: 8000, 9997, 9100, 22



Technology Stack
ComponentToolPurposeSource ControlGitHubVersion control and code repositoryCI/CDJenkinsPipeline automation and orchestrationBuild Agentagent1Dedicated build execution nodeBuild ToolMavenApplication compilation and packagingCode QualitySonarQubeStatic code analysisCode StandardsCheckstyleJava coding standards validationSecurity ScanningTrivyVulnerability and secret detectionArtifact ManagementNexusBinary artifact storageConfiguration ManagementAnsibleInfrastructure automation and deploymentMonitoringPrometheusMetrics collectionVisualizationGrafanaDashboards and alertingLog ManagementSplunkCentralized loggingNotificationsSlackReal-time alerts
Pipeline Stages Explained
Stage 1: Checkout Code

Clones source code from GitHub repository
Executes on: agent1

Stage 2: Trivy - Update Database

Updates Trivy vulnerability database
Ensures latest CVE information
Executes on: agent1

Stage 3: Trivy - Filesystem Scan

Scans source code for vulnerabilities
Checks for hardcoded secrets
Blocks build if secrets found
Executes on: agent1

Stage 4: Maven Build

Compiles Java source code
Packages application as WAR file
Executes on: agent1

Stage 5: Unit Tests

Runs JUnit tests
Generates test reports
Fails build if tests fail
Executes on: agent1

Stage 6: Checkstyle Analysis

Validates Java coding standards
Generates Checkstyle report
Executes on: agent1

Stage 7: SonarQube Analysis

Performs deep code quality analysis
Checks for bugs, code smells, vulnerabilities
Calculates code coverage
Sends results to SonarQube server
Executes on: agent1

Stage 8: SonarQube Quality Gate

Waits for SonarQube analysis completion
Validates against quality gate rules
Fails build if quality gate fails
Threshold: Max 10 bugs
Executes on: agent1

Stage 9: Trivy - Comprehensive Security Scan

Extracts and scans WAR artifact
Checks dependencies for vulnerabilities
Scans for configuration issues
Generates multiple report formats (JSON, HTML, SARIF)
Fails if >10 critical vulnerabilities
Executes on: agent1
Script: /opt/trivy/scripts/comprehensive-scan.sh

Stage 10: Upload to Nexus

Uploads WAR artifact to Nexus repository
Version format: BUILD_ID-TIMESTAMP
Repository: maven-project-releases
Executes on: agent1

Stage 11: Deploy to Dev

Uses Ansible playbook from agent1
Connects to Dev-Env via SSH
Stops Tomcat
Backs up existing application
Deploys new WAR file
Starts Tomcat
Playbook: /home/jenkins/ansible/playbooks/deploy-webapp.yml
Executes on: agent1 (controlling Dev-Env)

Stage 12: Health Check - Dev

Verifies Tomcat service running
Checks application endpoint (HTTP 200)
Validates deployment success
Playbook: /home/jenkins/ansible/playbooks/health-check.yml
Executes on: agent1 (checking Dev-Env)

Stage 13: Deploy to Stage

Same as Dev deployment
Target: Stage-Env
Executes on: agent1 (controlling Stage-Env)

Stage 14: Health Check - Stage

Validates Stage deployment
Executes on: agent1 (checking Stage-Env)

Stage 15: Approval for Production

Manual approval gate
Timeout: 1 hour
Authorized approver: admin
Pauses pipeline until approval
Executes on: Jenkins Master

Stage 16: Deploy to Production

Deploys to production after approval
Target: Prod-Env
Executes on: agent1 (controlling Prod-Env)

Stage 17: Health Check - Production

Final production validation
Executes on: agent1 (checking Prod-Env)

Access URLs
Jenkins Master:  http://<Jenkins-Master-IP>:8080
agent1:          SSH only (no web interface)
SonarQube:       http://<SonarQube-IP>:9000
Nexus:           http://<Nexus-IP>:8081
Dev App:         http://<Dev-IP>:8080/webapp/
Stage App:       http://<Stage-IP>:8080/webapp/
Prod App:        http://<Prod-IP>:8080/webapp/
Prometheus:      http://<Prometheus-IP>:9090
Grafana:         http://<Grafana-IP>:3000
Splunk:          http://<Splunk-IP>:8000
Credentials
ServiceUsernamePasswordNotesJenkinsadminadminChange after first loginSonarQubeadminadminChange after first loginNexusadminadminGet initial password from fileGrafanaadminadminChange on first loginSplunkadminAdmin@1238+ character requirementAnsibleansibleadminansibleadminOn all app servers
File Locations
On agent1:
/home/jenkins/workspace/              # Build workspace
/home/jenkins/ansible/                # Ansible configuration
  ├── inventory/hosts                 # Server inventory
  ├── playbooks/deploy-webapp.yml     # Deployment playbook
  └── playbooks/health-check.yml      # Health check playbook
/opt/trivy/                           # Trivy installation
  ├── scripts/comprehensive-scan.sh   # Security scan script
  └── reports/                        # Scan reports
/opt/maven/                           # Maven installation
On App Servers:
/opt/apache-tomcat-8.5.82/            # Tomcat installation
  ├── webapps/webapp.war              # Deployed application
  ├── logs/                           # Application logs
  └── backup/                         # Application backups
/var/log/tomcat/                      # Tomcat logs (Splunk monitored)
Monitoring & Alerting
Prometheus Metrics

System metrics (CPU, Memory, Disk)
Application metrics
Node Exporter on all servers (port 9100)

Grafana Dashboards

Infrastructure Overview (Dashboard ID: 1860)
Real-time system metrics
Historical data analysis

Splunk Logging

Centralized log aggregation
Tomcat application logs
Searchable and indexed
Forwarders on Dev, Stage, Prod

Slack Notifications

Build started/completed
Success/failure alerts
Stage-specific updates
Includes build links

Security Features
Trivy Security Scanning

Filesystem Scan

Scans source code
Detects hardcoded secrets
Identifies configuration issues


Comprehensive Scan

Scans WAR artifact
Dependency vulnerability detection
CVE database integration
Multiple report formats


Thresholds

Build fails on secrets found
Build fails on >10 critical vulnerabilities



SonarQube Quality Gates

Code coverage requirements
Bug threshold: Max 10
Code smell detection
Security hotspot identification

Troubleshooting
Pipeline Fails at Trivy Scan
bash# On agent1
ssh -i key.pem ec2-user@<agent1-IP>
sudo su - jenkins

# Check Trivy installation
trivy --version

# Update database manually
trivy image --download-db-only

# Check scan reports
ls -la /opt/trivy/reports/
Ansible Deployment Fails
bash# On agent1
sudo su - jenkins
cd /home/jenkins/ansible

# Test connectivity
ansible all -i inventory/hosts -m ping

# Check SSH keys
ls -la ~/.ssh/

# Test manual SSH
ssh ansibleadmin@<target-server-private-ip>
SonarQube Quality Gate Timeout
bash# Check SonarQube webhook
# In SonarQube: Administration → Webhooks
# Should point to: http://<Jenkins-Master-Private-IP>:8080/sonarqube-webhook/

# Verify webhook is associated with project
# Projects → Your Project → Administration → Webhooks
Application Not Accessible
bash# Check Tomcat status
ssh ansibleadmin@<server-ip>
sudo systemctl status tomcat

# Check application logs
sudo tail -f /var/log/tomcat/catalina.out

# Verify deployment
ls -la /opt/apache-tomcat-8.5.82/webapps/
```

## Pipeline Performance

| Metric | Value |
|--------|-------|
| Average Build Time | ~12-15 minutes |
| Security Scan | ~2-3 minutes |
| Deployment per Env | ~30-60 seconds |
| Total (with approval) | ~20 minutes |

## Success Criteria

✅ All unit tests pass (100%)
✅ Checkstyle validation passes
✅ SonarQube quality gate passes
✅ No secrets detected in code
✅ Critical vulnerabilities < 10
✅ All deployments successful
✅ All health checks pass
✅ Slack notifications sent
✅ Artifacts stored in Nexus
✅ Logs visible in Splunk
✅ Metrics visible in Grafana

## Key Achievements

🎯 **Distributed Build Architecture** - Separate master and agent for scalability
🔒 **Multi-layer Security** - Trivy scanning at multiple stages
🤖 **Infrastructure as Code** - Ansible for consistent deployments
📊 **Complete Observability** - Metrics, logs, and traces
🚀 **Zero-downtime Deployments** - Controlled rollout with health checks
✨ **Quality Enforcement** - Automated gates prevent bad code
🔔 **Real-time Feedback** - Instant Slack notifications
📦 **Artifact Management** - Versioned and stored artifacts

## Future Enhancements

- [ ] Implement blue-green deployments
- [ ] Add automated rollback on failure
- [ ] Integrate container scanning with Trivy
- [ ] Add performance testing stage
- [ ] Implement GitOps with ArgoCD
- [ ] Add chaos engineering tests
- [ ] Enhance security with Vault integration
- [ ] Add cost optimization tracking

## Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open Pull Request

## License

This project is licensed under the MIT License

## Contact

For questions or support:
- Email: devops@company.com
- Slack: #cicd-pipeline-support

---

**Congratulations!** You now have a production-ready, enterprise-grade CI/CD pipeline! 🎉
```

---

## **Phase 13: Final Validation and Testing**

### Step 31: Complete End-to-End Test

**1. Make a code change:**
```bash
# On your local machine
cd realworld-cicd-pipeline-project

# Make a small change
echo "<!-- Pipeline Test $(date) -->" >> src/main/webapp/index.jsp

# Commit and push
git add .
git commit -m "Testing complete pipeline with agent1 and Trivy"
git push origin main
```

**2. Watch the pipeline automatically trigger**

**3. Monitor execution on agent1:**
```bash
# On agent1
ssh -i your-key.pem ec2-user@<agent1-IP>
sudo su - jenkins

# Watch workspace
watch -n 2 'ls -lh /home/jenkins/workspace/'

# Monitor Trivy scans
tail -f /opt/trivy/reports/json/*.json
```

**4. Verify all stages complete successfully**

**5. Approve production deployment when prompted**

**6. Verify application in all environments:**
```bash
# Dev
curl http://<Dev-IP>:8080/webapp/ | grep "Pipeline Test"

# Stage
curl http://<Stage-IP>:8080/webapp/ | grep "Pipeline Test"

# Production
curl http://<Prod-IP>:8080/webapp/ | grep "Pipeline Test"
```

**7. Check all reports and dashboards:**
- Jenkins build page → Console output
- SonarQube → Projects → maven-project
- Nexus → Browse → maven-project-releases
- Prometheus → Targets (all UP)
- Grafana → Dashboard → Select hosts
- Splunk → Search for logs
- Slack → Check notifications

---

## **🎊 CONGRATULATIONS! 🎊**

You have successfully implemented an **Enterprise-Grade CI/CD Pipeline** with:

### **✅ Complete Pipeline Features:**

1. **🏗️ Distributed Architecture**
   - Jenkins Master for orchestration
   - Dedicated build agent (agent1) for execution
   - Scalable and maintainable design

2. **🔒 Multi-Layer Security**
   - Trivy filesystem scanning
   - Trivy comprehensive artifact scanning
   - Secret detection
   - SonarQube security analysis
   - Quality gates enforcement

3. **🤖 Infrastructure Automation**
   - Ansible playbooks for deployment
   - SSH key-based authentication
   - Idempotent deployments
   - Automated health checks

4. **📊 Complete Observability**
   - Prometheus metrics collection
   - Grafana visualization dashboards
   - Splunk centralized logging
   - Node Exporter on all servers

5. **🚀 Production-Ready Pipeline**
   - Automated build and test
   - Code quality enforcement
   - Security scanning at multiple stages
   - Multi-environment deployment
   - Manual production approval
   - Real-time Slack notifications

### **📈 Key Metrics:**

- **Total Infrastructure**: 9 EC2 instances
- **Pipeline Stages**: 17 automated stages
- **Security Scans**: 3 different scanning points
- **Deployment Environments**: 3 (Dev, Stage, Prod)
- **Average Build Time**: ~15 minutes
- **Success Rate Target**: >95%

### **🎯 Skills Demonstrated:**

✅ Jenkins Master-Agent Architecture
✅ Trivy Security Scanning
✅ Ansible Configuration Management
✅ Maven Build Automation
✅ SonarQube Code Quality
✅ Nexus Artifact Management
✅ Multi-Environment Deployments
✅ Infrastructure Monitoring
✅ Log Aggregation
✅ CI/CD Best Practices

### **📚 What You've Learned:**

- Setting up distributed Jenkins architecture
- Configuring dedicated build agents
- Implementing comprehensive security scanning
- Automating deployments with Ansible
- Managing SSH keys for automation
- Integrating multiple DevOps tools
- Building production-grade pipelines
- Implementing monitoring and alerting

---

## **Quick Reference Commands**
```bash
# Check agent1 status
ssh -i key.pem ec2-user@<agent1-IP>
ps aux | grep java

# Test Ansible connectivity
sudo su - jenkins
cd /home/jenkins/ansible
ansible all -i inventory/hosts -m ping

# Run Trivy scan manually
/opt/trivy/scripts/comprehensive-scan.sh /path/to/workspace BUILD_123

# Check pipeline workspace
ls -lh /home/jenkins/workspace/Complete-CICD-Pipeline/

# View Trivy reports
ls -lh /opt/trivy/reports/

# Test application deployment
curl http://<Dev/Stage/Prod-IP>:8080/webapp/

# Check Prometheus targets
curl http://<Prometheus-IP>:9090/api/v1/targets

# Search Splunk logs
# In Splunk UI: index=* source="/var/log/tomcat/*"
```

---

**You are now a professional DevOps Engineer with hands-on experience in enterprise CI/CD pipeline implementation!** 🚀

**Keep learning, keep building, and never stop improving!** 💪

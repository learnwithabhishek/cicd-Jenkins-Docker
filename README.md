## Continuous Integration & delivery using Jenkins, maven, Sonarqube and Docker

#Run jenkinsserver.sh on a ubuntu vm with 2gb ram, 2 cpus or more

#Run sonarserver.sh on on a ubuntu vm with 2.5gb ram, 2 cpus or more 

Install Jenkins Plugin : Build Timestamp Plugin , CloudBees Docker Build and Publish plugin , Docker Pipeline, Docker plugin, Pipeline Maven Integration Plugin, Pipeline Utility Steps, SonarQube Scanner for Jenkins, Slack Notification Plugin

In global tool configuration add jdk8. Install openjdk-8-jdk on Jenkins vm and provide it's path as show in the picture :

![JDK-GlobalToolConfiguration](https://user-images.githubusercontent.com/110404399/229291349-a87818ca-914b-4b00-8ba0-bafbcc38f8d0.jpg)

In global tool configuration add Maven 3.3.9 :

![Maven-Global-Tool-Configuration](https://user-images.githubusercontent.com/110404399/229296162-7de7cc5f-c612-4a82-9699-28b8ed7e2fd8.jpg)

Add SonarQube scanner in global tool configuration:

![Sonar_scanner-GlobalToolConfiguration](https://user-images.githubusercontent.com/110404399/229296268-6c1bcf30-cdc0-4785-a008-7e802e7e482f.jpg)

For slack notification create an account on slack. Create a workspace, create a channel(ex #jenkins-cicd). In order for the Jenkins to authenticate to workspace, we need to create a token in Slack. For that, we need to add an app in Slack account. Search for the Slack apps or add apps to Slack :

![addAppSlack](https://user-images.githubusercontent.com/110404399/229297743-64ccf1e4-f704-4f6d-83a5-eeed444cb753.jpg)

Add this app to slack. Choose a channel where you want to receive notification (ex. #jenkins-cicd). Add Jenkins Ci integration.

![addAppSlack2](https://user-images.githubusercontent.com/110404399/229298625-beee0472-7a1e-47d4-a999-7d28d2a8b796.jpg)

In set up instruction steps go to step3, copy the token then save the settings. Now go to manage jenkins --> configure system , search for Slack :

![addAppSlack3](https://user-images.githubusercontent.com/110404399/229299711-cdc58981-a955-474e-bafe-e413ca947704.jpg)

provide workspace name, credential( token copied earlier) , channel name then save it.

These 3 credentials required for this project :

![Global-credentials](https://user-images.githubusercontent.com/110404399/229300766-eab95d6f-7822-46bf-9401-b6af388fb799.jpg)

For sonarqube token first login to sonar server , username: admin, password: admin. Click on my aacount

![image](https://user-images.githubusercontent.com/110404399/229301317-1b1b60a4-3cd0-499b-b0b6-6bd3f8812e1c.png)

In security give a name and generate token :

![image](https://user-images.githubusercontent.com/110404399/229301493-462918d9-cb9e-4269-9358-4453b5df9637.png)

copy the token generated and use it to configure sonarqube server

![image](https://user-images.githubusercontent.com/110404399/229301653-c00edce6-7dd5-4dc9-b489-a648111a1927.png)

In configure system add your Sonarqube server :

![SonarQubeServer-ConfigureSystem](https://user-images.githubusercontent.com/110404399/229297010-b2a3db51-f50b-44fe-ba7a-4fe22b2f141f.jpg)

Create a job of type pipeline :

![Jenkins-pipeline-config](https://user-images.githubusercontent.com/110404399/229302403-196592bc-7eaa-46f5-a08b-e0824893cdf7.jpg)

Click Build now to run the job :

![Jenkins-pipeline](https://user-images.githubusercontent.com/110404399/229302606-e1ac70c2-031d-473f-906f-a214760cbb7e.jpg)

After competion of job we will receive a slack notification ( green colour for success & red colour for failure ) :

![Slack-Notification](https://user-images.githubusercontent.com/110404399/229302753-d142db6a-a554-4a38-9c6b-5982b3a8af45.jpg)
![image](https://user-images.githubusercontent.com/110404399/229302863-d0b5e5df-e054-4214-b057-03db9d8e2af4.png)

Docker image will be build and uploaded to docker hub account:

![Docker-Hub](https://user-images.githubusercontent.com/110404399/229302945-cfdf0e60-f9e2-4486-a4fa-9e58e92dd309.jpg)

This latest tag image will be used in our continuous deployment with Argocd on kubernetes cluster project



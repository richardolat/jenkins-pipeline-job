# jenkins-pipeline-job
The jenkins pipeline job is a continuation of the jenkins-mini-project. Here, we are creating job using the jenkins pipeline



#  Create a jenkins Pipeline Job

#### From the dashboard, select new item

![image](https://github.com/user-attachments/assets/b5078719-88c0-4e5d-97d5-0e418d5dfc8c)



#### Configure Build Trigger 
![image](https://github.com/user-attachments/assets/85dfc266-d6f3-4f7c-9e32-cda824053ec7)


#### Write a jenkins pipeline script 
pipeline \{
    agent any

    stages \{
        stage('Connect To Github') \{
            steps \{
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/richardolat/jenkins-scm.git']])
            \}
        \}
        stage('Build Docker Image') \{
            steps \{
                script \{
                    sh 'docker build -t dockerfile .'
                \}
            \}
        \}
        stage('Run Docker Container') \{
            steps \{
                script \{
                    sh 'docker run -itd -p 8081:80 dockerfile'
                \}
            \}
        \}
    \}
\}



#### Put the pipeline script in the section below 
![image](https://github.com/user-attachments/assets/ca6c9e12-3f83-44b1-b3b8-3a760a04f39b)



#### Click on pipeline syntax 

![image](https://github.com/user-attachments/assets/d7dab578-a87a-4f50-95b9-a041549b621f)




#### Select the drop down for checkout: checkout for version control 
![image](https://github.com/user-attachments/assets/07e98510-a332-4934-a8d1-98837e0024ab)





#### Copy and paste your github repository url and make sure the branch is main
![image](https://github.com/user-attachments/assets/6441836e-8bb6-4d62-9881-5fb6c1fde5ee)


#### Generate the pipeline script
![image](https://github.com/user-attachments/assets/8ccaae5b-d155-4d26-b41c-a3652da1c84b)



#### Replace the genertaed script for jenkins connect to github
![image](https://github.com/user-attachments/assets/623b9635-fbf8-40d6-887b-f117a93cfdea)


## Install Docker 

#### Create a file called docker.sh
![image](https://github.com/user-attachments/assets/d5e752ee-aeeb-4955-9595-119dd85235e4)



#### Open the file and paste the script below 
sudo apt-get update -y
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update -y
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
sudo systemctl status docker



#### Save and close the file 
![Screenshot 2024-11-15 203157](https://github.com/user-attachments/assets/560913ba-e73e-499e-bd5a-699997c942fa)


#### Make the file executable 
sudo chmod u+x docker.sh


#### Execute the file 
sudo ./docker.sh


#### Docker is successfully installed 
![image](https://github.com/user-attachments/assets/a0c1c464-6475-4676-b2b2-873a2177cbba)



#### Create a new file named "dockerfile" and paste the code snippet below into the file 
# Use the official NGINX base image
FROM nginx:latest

# Set the working directory in the container
WORKDIR  /usr/share/nginx/html/

# Copy the local HTML file to the NGINX default public directory
COPY index.html /usr/share/nginx/html/

# Expose port 80 to allow external access
EXPOSE 80

#### Create a "index.html" file and paste a code like the one below. You can customize it to your desire 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Congratulations on Your First Pipeline Job</title>
</head>
<body>
    <header>
        <h1 style="text-align: center; background-color: #f0f0f0; padding: 10px;">RICHARD DEVOPS CONGRATULATIONS ON YOUR FIRST PIPELINE JOB</h1>
    </header>
</body>
</html>

![image](https://github.com/user-attachments/assets/755c7aba-3cf8-4855-be32-92accc290ff7)


































































































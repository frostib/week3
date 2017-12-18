Day 1
# Install Linux
http://www.osboxes.org/ubuntu/

# Install sublime text
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt-get update
sudo apt-get install sublime-text

# Install Git
sudo apt install git

# Login to GitHub

# initialize empty git repo
git init
# add all files to repo
git add .
# tell who you are
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
# commit changes
git commit -m "adding files"
# connect local repo with github repo
git remote add origin https://github.com/yourusername/your-repo-name.git
# push commited files to remote repo (ssh connection to github: https://help.github.com/articles/connecting-to-github-with-ssh/)
git push -u origin master


Day 2
# Part 1: Install Docker. Getting Started
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install docker-ce

# Part 2: Create and run docker image. Store on Docker Cloud
mkdir day2
cd day2
subl Dockerfile
subl app.js
subl package.json
docker build -t pagecounter .
docker run -d -p 3000:3000 pagecounter
docker container ls
docker container stop CONTAINER_ID
docker login
docker tag pagecounter frostib/week1:day2
docker push frostib/week1:day2

# Part 3: Install docker-compose
sudo curl -L https://github.com/docker/compose/releases/download/1.17.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

subl docker-compose.yml
docker-compose up

Day 3
# Step 1
# Login to aws

# install python-pip
sudo apt install python-pip

# install the AWS CLI
pip install awscli --upgrade --user

# Launch instance -> Amazon Linux -> Next -> Next... Step 6: Configure Security Group -> Create New -> Name: ssh-http
Type	Port 	Addr
Http 	80		0.0.0.0/0
SSH 	22		MyIP
Launch -> week1-day3.pem -> Save -> Launch -> View
InstanceID: i-00827d8620f5a54ab
Public DNS: ec2-52-31-140-190.eu-west-1.compute.amazonaws.com

--------Brazil-----------
AMI: ami-286f2a44
vpc-6cf41e0b
InstanceID: i-0bb17ff6769c61ec4
Public DNS: ec2-54-207-21-128.sa-east-1.compute.amazonaws.com

# change directory to where the pem file is saved
chmod 400 week1-day3.pem
ssh -i week1-day3.pem ec2-user@ec2-52-31-140-190.eu-west-1.compute.amazonaws.com
# now you're logged in the aws machine
# install docker on the aws machine
sudo yum update -y
sudo yum install -y docker
sudo service docker start
sudo usermod -a -G docker ec2-user
exit
ssh -i week1-day3.pem ec2-user@ec2-52-31-140-190.eu-west-1.compute.amazonaws.com
docker run -d -p 80:3000 frostib/week1:day2

# Step 2
TODO

Day 4
# Postgres
npm install pg
TODO

Day 6
# Installing Jenkins and Docker on AWS
# open new port in security group
# Create Jenkinsfile
# Jenkins setup (make sure cicd-access-policy exists)
aws iam create-role --role-name StudentCICDServer  --assume-role-policy-document file://./cicd-access-policy.json
ARN="arn:aws:iam::aws:policy/AmazonEC2FullAccess"
aws iam attach-role-policy --role-name StudentCICDServer --policy-arn $ARN 
aws iam create-instance-profile --instance-profile-name CICDServer-Instance-Profile
aws iam add-role-to-instance-profile --role-name StudentCICDServer --instance-profile-name CICDServer-Instance-Profile
aws ec2 associate-iam-instance-profile --instance-id i-08867ec24e2313a11 --iam-instance-profile Name=CICDServer-Instance-Profile

# login to aws using ssh
ssh -i week1-day3.pem ec2-user@ec2-52-31-140-190.eu-west-1.compute.amazonaws.com

# update java on the remote machine
sudo yum install java-1.8.0
sudo yum remove java-1.7.0-openjdk

# install jenkins
sudo yum update
sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
sudo rpm --import http://pkg.jenkins-ci.org/redhat-stable/jenkins-ci.org.key
sudo yum install jenkins
sudo service jenkins start
sudo chkconfig jenkins on

# install docker and git
sudo yum install -y ecs-init
sudo gpasswd -a jenkins docker
sudo service docker start
sudo chkconfig docker on
sudo yum install git

# Key for GitHub plugin
sudo su -s /bin/bash jenkins
cd /var/lib/jenkins/
ssh-keygen
cat .ssh/id_rsa.pub
# add the new key to github
exit
sudo reboot

cat /var/lib/jenkins/secrets/InitialAdminPassword

subl Jenkinsfile

Day 7

# install nvm
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.7/install.sh | bash

# install node
nvm install 6.9.1

# install yarn
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update && sudo apt-get install yarn

# Getting started...
npm install -g nodemon
npm install -g create-react-app
npm run startpostgres && sleep 10 && npm run migratedb
----ERROR----

Day 11
git clone https://github.com/hgop/week3.git
npm install -g db-migrate
cd server
db-migrate create day11
# [INFO] Created migration at /home/osboxes/hgop/final/week3/server/migrations/20171218003018-day11.js
# edit 20171218003018-day11.js
# create assignment.md inside apitest folder 
docker container ls
docker container stop id
docker container rm id

nvm install 6.9.1
npm install -g nodemon
npm install -g create-react-app

npm run startpostgres && sleep 10 && npm run migratedb:dev

yarn install
cd client
npm install

Day 12
yarn add jasmine-reporters
sudo apt install junit

Day 13
Datadog...
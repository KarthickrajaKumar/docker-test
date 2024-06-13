EC2 integrating with ECR using docker and jenkins code.

#!/bin/bash

whoami
sudo apt update
sudo apt install git -Y
rm -rf *
git clone https://github.com/krishnansai/docker-test.git
cp -r ./docker-test/* .
sudo apt install docker.io -y
sudo docker build . -t 730335336468.dkr.ecr.ap-south-1.amazonaws.com/jenkinsimage
aws ecr get-login-password --region ap-south-1 | sudo docker login --username AWS --password-stdin 730335336468.dkr.ecr.ap-south-1.amazonaws.com
sudo docker push 730335336468.dkr.ecr.ap-south-1.amazonaws.com/jenkinsimage
sudo docker pull 730335336468.dkr.ecr.ap-south-1.amazonaws.com/jenkinsimage
sudo docker run -d httpd
sudo docker stop $(sudo docker ps)
sudo docker rm $(sudo docker ps -a)
sudo docker run -d -p 80:80 730335336468.dkr.ecr.ap-south-1.amazonaws.com/jenkinsimage

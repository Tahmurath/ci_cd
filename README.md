#- tried to run gitea:
#docker run -d --name gitea -p 3000:3000 -p 2222:22 -v ~/gitea/data:/data gitea/gitea:latest

#- tried to connect to local mysql:
#access host os from container host.docker.internal

- changed to docker-compose:
./docker-compose.yml

- instaled with user pass & email:
gitea gitea@local.com gitea@local.com

- user & pass secound account:
hamidreza
hamidreza.tahmooresi@gmail.com
hamidreza.tahmooresi@gmail.com


- jenkins added to docker-compose:
Jenkins initial setup is required. An admin user has been created and a password generated.
2025-03-06 17:05:55 Please use the following password to proceed to installation:
2025-03-06 17:05:55 
2025-03-06 17:05:55 edd4dbd026c54c84bf98ac71bd2c589d
2025-03-06 17:05:55 
2025-03-06 17:05:55 This may also be found at: /var/jenkins_home/secrets/initialAdminPassword
2025-03-06 17:05:55

- user & pass secound account:
jenkins
hamidreza.tahmooresi@gmail.com
hamidreza.tahmooresi@gmail.com


- created new go app ./app
git remote set-url origin http://hamidreza:deff24b76fd449547fe94ecc75eef635edb29ba9@localhost:3000/gitea/golang.git


- added dockfile to go app

- go app image build
docker build -t my-go-app .
docker tag my-app:latest localhost:5000/my-app:latest
docker push localhost:5000/my-app:latest

docker pull localhost:5000/my-app:latest
docker run -d -p 8484:8484 localhost:5000/my-app:latest

- run go image
docker run -p 8484:8484 my-go-app


#- localstack added to docker-compose

#- aws to localstack
#aws --endpoint-url=http://localhost:4566 configure
#AWS Access Key ID [None]: test
#AWS Secret Access Key [None]: test
#Default region name [None]: us-east-1
#Default output format [None]: json

#aws --endpoint-url=http://localhost:4566 ecr create-repository --repository-name my-repo
#aws --endpoint-url=http://localhost:4566 list-repositories


#docker build -t username/repository:tag .
#docker login -u username -p password
#docker push username/repository:tag

- Install jenkins plugins:
Pipeline
Docker Pipeline
Kubernetes CLI



- jenkins new pipeline job:
pipeline {
    agent any

    environment {
        REGISTRY = "localhost:5000"
        IMAGE_NAME = "my-app"
        TAG = "latest"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'http://localhost:3000/gitea/golang.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $REGISTRY/$IMAGE_NAME:$TAG .'
            }
        }

        stage('Push to Local Registry') {
            steps {
                sh 'docker push $REGISTRY/$IMAGE_NAME:$TAG'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl set image deployment/my-app my-app=$REGISTRY/$IMAGE_NAME:$TAG'
            }
        }
    }
}


- kuber
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
        - name: my-app
          image: localhost:5000/my-app:latest
          ports:
            - containerPort: 8080
			
			
- gittea webhook http://jenkins:8080/gitea-webhook/post


- jenkins Poll SCM H/5 * * * *


- jenkins docker plugin
- jenkins cloud new cloud

Expose daemon on tcp://localhost:2375 without TLS
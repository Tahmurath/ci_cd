
- tried to run gitea:
docker run -d --name gitea -p 3000:3000 -p 2222:22 -v ~/gitea/data:/data gitea/gitea:latest

- tried to connect to local mysql:
access host os from container host.docker.internal

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


- created new go app

- added dockfile to go app

- go app image build
docker build -t my-go-app .

- run go image
docker run -p 8484:8484 my-go-app


- localstack added to docker-compose

- aws to localstack
aws --endpoint-url=http://localhost:4566 configure
AWS Access Key ID [None]: test
AWS Secret Access Key [None]: test
Default region name [None]: us-east-1
Default output format [None]: json

next step : install goharbor/harbor
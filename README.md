Make volume
-----
mkdir jenkins_home

mkdir jenkins_slave_home

build Master
-----
docker-compose up -d --no-deps --build master

Create master ssh key
-----
docker-compose exec master ssh-keygen -t rsa -b 4096 -C ""

Update master ssh key to agent
-----
cat jenkins_home/.ssh/id_rsa.pub

vi docker-compose.yml 

update ssh public in JENKINS_SLAVE_SSH_PUBKEY 

	For example :
				....	
			    environment:
	      			- JENKINS_SLAVE_SSH_PUBKEY=ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAA.....................


Up master and slave
----

docker-compose up -d

Create key for agent
----
docker-compose exec -u jenkins agent ssh-keygen -t rsa -b 4096 -C "" 


Access master
----
Access localhost:8080 browser

	password
	----
		cat jenkins_home/secrets/initialAdminPassword

Create agent in master
-----
Create new secret with agent private key

	cat jenkins_slave_home/.ssh/id_rsa

Options
----

Remote root directory: /home/jenkins
Launch method: Launch agent via ssh
	Host: localhost
	click on advanced
	port: 2222
save


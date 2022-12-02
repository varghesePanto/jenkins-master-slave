Make volume
-----
mkdir jenkins_home

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

Access master
----
Access localhost:8080 browser

	password
	----
		cat jenkins_home/secrets/initialAdminPassword

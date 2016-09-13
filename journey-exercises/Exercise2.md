## Exercise 1 - Infrastructure as code

Follow these steps on your AWS instance to create a complete continuous delivery infrastructure.

### Install docker compose

Follow these steps to install docker-compose:

    ubuntu@docker:~$ sudo -i
    root@docker:~$ curl -L https://github.com/docker/compose/releases/download/1.8.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
    root@docker:~$ chmod +x /usr/local/bin/docker-compose
    root@docker:~$ exit
    ubuntu@docker:~$

Verify `compose` is installed:

    ubuntu@docker:~/code-infra/containers$ docker-compose --version
    docker-compose version 1.8.0, build f3628c7
    ubuntu@docker:~/code-infra/containers$

### Set up a jenkins, docker registry and artifactory server for the team
````
ubuntu@docker:~$ git clone https://github.com/praqma-training/code-infra
````
### Follow the setup instructions
Go here and follow the instructions to make the data directories: https://github.com/praqma-training/code-infra

Verify that you can reach the apache server in your web browser and that jenkins is up and running.

### Initial configuration of jenkins

Check that the jenkins server is up and running on: `http://YOUR-AWS-INSTANCE/jenkins`

(Note: It wont respond without the `/jenkins`context path)

#### Initial admin password

You need to access jenkins the first time by getting the initial admin password from the jenkins container.  Use this command on the aws node to retrieve it and set up a new user.

````
docker exec -it containers_jenkins_1 cat /var/jenkins_home/secrets/initialAdminPassword
````

Copy the output string and paste it in the "admin" user password field in the Jenkins console

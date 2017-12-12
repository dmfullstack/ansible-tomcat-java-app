# SE - Test

Create a automated deployment process that take a Grails application from source and deploys it to a Ubuntu server.

Details on the Ubuntu Server are provided in the **Vagrantfile**


## Process

The challenge has been solved by using **Ansible** and **Docker** containers. 

The automation starts by creating a Dockerfile on the target hosts and by installing Java and Git which are necessary during the following steps.

Then the application is fetched on the machine and the **war** file is built.

After that, an Ansible role (**docker-install**) will install Docker on the server.

When Docker is up and running, Ansible will build and image containing Tomcat7 and Java 8. After that, a container is started. As described in the Dockerfile, the built **war** file is copied inside the **Tomcat webapp** folder.


## Dockerfile

Here it shown how the Dockerfile looks like when installed on the machine:

```
FROM tomcat:7.0-jre8
# Remove default ROOT application
RUN ["rm", "-fr", "/usr/local/tomcat/webapps/ROOT"]

COPY grails-petclinic/target/petclinic-4.0.war /usr/local/tomcat/webapps/ROOT.war
```

This is not a static file. It has been created based on a Jinja2 template.

```
FROM tomcat:{{ tomcat_image_version }}
# Remove default ROOT application
RUN ["rm", "-fr", "/usr/local/tomcat/webapps/ROOT"]

COPY grails-petclinic/target/petclinic-4.0.war /usr/local/tomcat/webapps/ROOT.war
```

Changing the template allows to tune the application deploiment.

## Variables

**vars/vault.yml**
This is an encrypted file containing access details
```
ansible_ssh_pass: 
ansible_sudo_pass: 
```

**vars/genersl.yml**

```
grail_dir:         Name of the dir in which fetch the repo

tomcat_image_version:      Docker container version
image_name:                Name to be assigned to the image
container_name:            Name to be assigned to the container
path_to_dockerfile:        Path to Docker file in the managed host
```

## How to run

```ansible-playbook main.yml --ask-vault-pass ```

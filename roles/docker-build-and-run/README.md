Docker - Build and Run Application
=========

The purpose of this role is to build a Docker image and run it.
The image is defined by a Dockerfile that should be passed on the managed host.


Role Variables
--------------

```
image_name:           name to be assigned to the image
path_to_dockerfile:   path to Dockerfile
container_name:       name to be assigned to the container
```



Example Playbook
----------------


    - hosts: servers
      roles:
         - role: docker-build-and-run
           image_name: my_image
           path_to_dockerfile: .docker
           container_name: my_app


Author Information
------------------
Matteo Mori

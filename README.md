# ansible-playbook-pssid-build-publish
An Ansible script that builds Docker images for the containers in the pssid-gui2
project, namely `pssid-gui2_client`, `pssid-gui2_server`, and `pssid-gui2_mongo`, 
and publish these images to Docker Hub.

## Prerequisites
* Ansible is installed locally. If not, install it with
```
sudo apt-get update && sudo apt-get install ansible
```

## Usage
Open `playbook.yml` with an editor and complete the **two** TODO items.

1. Update the path to the docker-compose file in the source code directory.
```
...
# *CAVEAT: use absolute path*
# TODO: change docker_compose_file path as appropriate.
docker_compose_file: "/home/wmarcoyu/pssid-gui2/docker-compose.yml"
frontend_image_name: "pssid-gui2_client"
...
```
***Caveat***: use absolute path for `docker_compose_file`. The reason is that 
building images requires sudo access, and the user-relative home directory `~` is 
ambiguous for root.

2. Change `dockerhub_username` accordingly.
```
...
    # TODO: change dockerhub_username as appropriate.
    dockerhub_username: "wmarcoyu"
  tasks:
...
```
If authentication fails, make sure you have logged into your Docker account at 
command-line. Refer to the (quick) tutorial 
[here](https://docs.docker.com/reference/cli/docker/login/#password-stdin).

Now you can run the script as follows in the same directory as the `playbook.yml`
file
```
ansible-playbook playbook.yml --ask-become-pass
```

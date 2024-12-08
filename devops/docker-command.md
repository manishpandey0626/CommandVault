# Docker Commands

**Table of Content**
- [Install Linux distribution](To-install-linux-distribution-in-windows-linux-system(WLS)-using-powershell)


### Return the list of all running containers.
`docker ps`
> options
>- -a to view all containers running or not.


### To run and install docker image
`docker run -d -p 80:80 image_name`
> options
>- -d detach
>- -p port
>- -e environment variable
>- --name container_name
>- --net for docker network


### To create image
`docker build -t "project name" .`

### To pull image
`docker pull image_name`

### To check all docker images in local system
`docker images`

### To stop container
`docker stop container_id`

### To start container
`docker start container_id`

### To see the con container logs
`docker logs container_id :`

### Get the terminal to current container
`docker exec -it container_id /bin/bash`


>Docker Network : if two container deployed in same docker network they can
communicate with just container name.

### To create docker networks
`docker network create network-name`

---

# To install linux distribution in windows linux system(WLS) using powershell.

---

- Display list of installed linux distribution: `wsl -l -v`
- Install distribution: `wsl --install -d Ubuntu` : 
- Set WSL version 2: `wsl --set-default-version 2` 


> Note: Open Linux(ubuntu) terminal to install docker

1. update package index and install packages: `apt-get update`


2. set repository
```bash
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
 ```

3. `sudo apt-get update`

4. Install docker
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

5. Create docker group and add user.
```bash
sudo groupadd docker
sudo usermod -aG docker $USER
```

6. Run docker Image

`sudo docker run hello-world`

`sudo -e /etc/wsl.conf`

[boot]

systemd=true
Exit Ubuntu and again:

To exit Ubuntu: `wsl --shutdown`
Then restart Ubuntu.

sudo systemctl status

start docker engine service: `systemctl start docker`


Set default user to root: `ubuntu config --default-user root`

=== to update wsl to store version

Add-AppxPackage C:/myproj/Microsoft.WSL_1.1.3.0_x64_ARM64.msixbundle
wsl --version # to confirm


---

To search the log in the all pods.
```bash
for pod in $(kubectl get pods -l app=orchestrator -n bipeatt -o jsonpath='{.items[*].metadata.name}'); do
  echo "Logs for pod: $pod"
  kubectl logs $pod -n bipeatt --since 5m| grep "Pipeline Execution Id= 683089"
done

```
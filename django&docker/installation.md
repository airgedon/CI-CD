## SET UP
```
sudo apt-get update && apt-get upgrade
```
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```
```
sudo apt update
```
```
apt-cache policy docker-ce  
```
```
sudo apt install docker-ce
```
> Optional 
```
sudo systemctl status docker

systemctl start docker

systemctl enable docker
```

---
## Configuring the Docker command without sudo (optional):
```
sudo usermod -aG docker ${USER}
```
```
su - ${USER}
```
```
id -nG
```
>output:    your_username sudo docker
```
sudo usermod -aG docker username
```

## Install docker-compose:
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
```
sudo chmod +x /usr/local/bin/docker-compose
```
```
docker-compose -v
```
> to stop docker-compose
```
docker-compose stop
```

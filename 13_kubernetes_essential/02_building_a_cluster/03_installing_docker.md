# Installing Docker

<img src="https://user-images.githubusercontent.com/6856382/221206121-5cc83a9e-f385-44e0-9e25-ec5ff951fdb9.png">

1. Login to each individual nodes, and type in the following command line codes (above doesnt work)

```
# UPDATE apt PACKAGE INDEX AND INSTALL PACKAGES TO ALLOW apt TO USE REPO OVER HTTPS
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release

# ADD THE DOCKER'S OFFICIAL GPG KEY:
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# SETUP REPO
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# RELOAD THE APT SOURCE LIST:
sudo apt-get update

# INSTALL DOCKER:
sudo apt-get install -y docker-ce=18.06.1~ce~3-0~ubuntu

# PREVENT UPDATE
sudo apt-mark hold docker-ce
```
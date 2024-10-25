# allora-worker

## Install requirements
```
sudo apt update && sudo apt upgrade -y
sudo apt install jq -y

# install docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
docker version

# install docker-compose
VER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)

curl -L "https://github.com/docker/compose/releases/download/"$VER"/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose
docker-compose --version
```


request some faucet from the [Allora Testnet Faucet](https://faucet.testnet-1.testnet.allora.network/) 

## Run the custom model
1. Create an account and obtain an Upshot ApiKey [here](https://developer.upshot.xyz)

2. Clone the git repository
```
git clone https://github.com/snake2102/allora-worker.git
cd allora-worker
```

3. Run the bash script
```
bash run.sh
```
* **Index:** Set your worker index.(the index gives you the ability to run multiple workers on one server)
* **Mnemonic Phrase:** Import you menmonic phrase
* **Upshot ApiKey:** Import your upshot apikey


make sure both `custom-worker-0` & `custom-inference` containers are running with `docker ps`
<img width="1325" alt="Screenshot 2024-09-09 at 3 33 15 PM" src="https://github.com/user-attachments/assets/e54c50ff-8fb6-4983-8586-5ddef8768a49">


check the worker container with `docker logs -f custom-worker-0` command

<img width="816" alt="Screenshot 2024-08-17 at 3 30 29 PM" src="https://github.com/user-attachments/assets/a24a19b0-36a5-407d-8fb5-46c72c63c819">

make sure `custom-inference` returns correct response
```
curl http://localhost:8001/inference/ETH
curl http://localhost:8001/inference/MEME
curl http://localhost:8001/inference/ELECTION
```

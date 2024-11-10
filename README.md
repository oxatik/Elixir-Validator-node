# Elixir-Validator-node
Modular DPoS Network

# Elixir Validator 

Elixir is a modular liquidity network that enables anyone to supply liquidity to orderbooks. The protocol serves as crucial decentralized infrastructure allowing for exchanges and protocols to easily bootstrap liquidity to their books.The infrastructure is similar to Arbitrum's security model, with fraud proofs posted on Ethereum mainnet.Validators will be delegated Elixir Foundation governance stake via the Elixir Foundation Delegation Program, whereby top performing validators participate in governance with their delegated tokens and earn validator emission rewards from their delegated stake.

# Overview
 Elixir a revolutionary network using Delegated Proof of Stake (DPoS), allowing everyone to directly provide liquidity to DEX order books. With over 20 native integrations, Elixir provides essential decentralized infrastructure to tighten bid-ask spreads, thereby facilitating liquidity creation on exchange platforms.
 
![image](https://github.com/user-attachments/assets/3740dc45-5a24-43e0-a018-cde9e5717616)

Elixir has raised almost 10 million dollars.

## Installation
# Server requirements
Official documentation says that
https://docs.elixir.xyz/running-an-elixir-validator

8RAM, 100GB disk will be enough.

# VPS Configuration
To set up your masternode, you have the choice of hosting it on your own computer or opting for a Virtual Private Server. In my case, I opted for Contabo, a reputable VPS rental solution.Running Exlire requires a little configuration.I recommend choosing the Cloud VPS 2, or even 3, if you want to run multiple nodes on your VPS.
To order your https://contabo.com/enContabo VPS, you can click on this link.

# Prerequisite
Update the local package repository database & upgrade installed packages to their latest versions based on the updated package database:

```bash
sudo apt-get update && apt-get upgrade -y  
```

# Install packages:
```bash
sudo apt install wget -y  
```
# Install Docker:
```bash
sudo apt install docker.io -y && \
docker --version  
```
# Installation
 Create elixir folder:
 ```bash
mkdir elixir  
```
Move to elixir folder:
```bash
cd elixir  
```
# Download the validator environment template file:
```bash
wget https://files.elixir.finance/validator.env  
```
# Open validator.env with nano:
```bash
nano validator.env  
```
 Fill the info about the wallet that you’ll be using for this validator.
For security reasons, this wallet should never be used for anything other than running a testnet validator.

STRATEGY_EXECUTOR_IP_ADDRESS=your IP address
STRATEGY_EXECUTOR_DISPLAY_NAME=your moniker
STRATEGY_EXECUTOR_BENEFICIARY=your address for validator rewards
SIGNER_PRIVATE_KEY=your private key (use private key from newly created wallet, not the EXECUTOR_BENEFICIARY)

![image](https://github.com/user-attachments/assets/a8d263bc-4fc5-4d7f-be49-464ad4b2f23e)

# Save and exit:
Ctrl+X
Y 
Enter

#  Enroll validator
Go to faucet https://testnet-3.elixir.xyz/
and mint MOCK tokens on the Ethereum Sepolia test network.
Note, that You can mint tokens to any wallet, such as EXECUTOR_BENEFICIARY from above. It will require some Sepolia ETH https://www.alchemy.com/faucets/ethereum-sepolia for gas fee.
Approve received MOCK tokens and stake them.

![image](https://github.com/user-attachments/assets/e625b496-afb0-4239-9910-82058c383bef)

Click the “CUSTOM VALIDATOR” button above the active validator list.
In the Custom validator modal that appears, enter your validator’s public wallet address of SIGNER_PRIVATE_KEY from above and click “DELEGATE”.
Confirm the transaction and wait for it to complete on-chain.

![image](https://github.com/user-attachments/assets/b71b85e2-ec7a-4f58-a82d-7f5806b1cc0f)

# Running Your Validator
Pull the Docker image:
```bash
docker pull elixirprotocol/validator:testnet  
```
# Run the validator:
```bash
 docker run -d --env-file /root/elixir/validator.env --name elixir --restart unless-stopped elixirprotocol/validator:testnet 
```
# Check if Docker image was created:
```bash
docker ps  
```
You should see such info:

![image](https://github.com/user-attachments/assets/bbbce8a4-81e5-4ece-9ece-96e7afbef437)

# Logs
To check logs run:
```bash
docker logs <CONTAINER_ID>  
```
Where <CONTAINER_ID> is an ID from previous step.
Should look like this:

![image](https://github.com/user-attachments/assets/3abec69a-0507-4e00-b59b-7733545e2d4f)

# Useful commands
Running A Validator On Apple/ARM Silicon
```bash
docker run -d --env-file /root/elixir/validator.env --name elixir --platform linux/amd64 elixirprotocol/validator:testnet  
```
Exposing Health Checks and Metrics
```bash
docker run -d --env-file /root/elixir/validator.env --name elixir -p 17690:17690 elixirprotocol/validator:testnet  
```
# Upgrading to mainnet
Open validator.env with nano:
```bash
cd elixir && \
nano validator.env  
```
# Change your environment:
```bash
ENV=prod  
```
# Save and exit:
Ctrl+X 
Y 
Enter

# Update:
```bash
docker kill elixir && \
docker rm elixir && \
docker pull elixirprotocol/validator --platform linux/amd64 && \
docker run -d --env-file /root/elixir/validator.env --name elixir --restart unless-stopped -p 17690:17690 elixirprotocol/validator && \
docker system prune -a && \
docker volume prune -f && \
docker network prune -f  
```
# Upgrading your mainnet+testnet validator
```bash
cd elixir && \
docker kill elixir && \
docker rm elixir && \
docker kill elixir-test && \
docker rm elixir-test && \
docker pull elixirprotocol/validator --platform linux/amd64 && \
docker run -d --env-file /root/elixir/validator.env --name elixir --restart unless-stopped -p 17690:17690 elixirprotocol/validator && \
cd testnet && \
docker pull elixirprotocol/validator:testnet && \
docker run -d --env-file /root/elixir/testnet/test-validator.env --name elixir-test --restart unless-stopped -p 17691:17690 elixirprotocol/validator:testnet && \
docker system prune -a && \
docker volume prune -f && \
docker network prune -f  
```
# Delete Node
```bash
docker kill elixir && \
docker rm elixir && \
docker kill elixir-test && \
docker rm elixir-test && \
cd && \
rm –rf elixir && \
docker system prune -a && \
docker volume prune -f && \
docker network prune -f  
```
# About Elixir
https://docs.elixir.xyz/running-an-elixir-validator

https://www.elixir.xyz/

https://x.com/Elixir

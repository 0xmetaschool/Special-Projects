# Day 10

Previously, we tested our ERC20 token contract in the last section. Our next goal is to deploy the contract. But before deploying, we need to ensure that we have a few things in place. 

## Getting a Private Key from Metamask

Everyone has a MetaMask wallet installed at this stage. We need the private key to be able to deploy smart contracts from our MetaMask wallet. Remember, a private key should be stored in a safe place where no one other than you can access it. 

To get your private key, follow the below steps:

- Click on three dots in the top right corner  of your MetaMask wallet
- Go to account details
- Click on the export private key

## Setting up an Alchemy account

Platforms like Alchemy give you access to the blockchain nodes so that you don't have to go through the hassle of hosting your nodes. Let's set up an Alchemy account.

Firstly, create an account on Alchemy by signing up. Next, go to the dashboard or directly to [https://dashboard.alchemy.com/](https://dashboard.alchemy.com/)

Go to the `+CREATE APP` button

Give a name and description of your choice and select the chain Ethereum. At this point, we will be using the Ethereum Sepolia test network.

Once this is done, go to the app you created and click "view key".

Now go to `VIEW KEY` and copy the `HTTPS` key.  Do not share this key with anyone.

## Creating a .env file to secure our info

To deploy our contract to the blockchain, we need a private key and Alchemy HTTP URL. 

Firstly, we need to install `dotenv` by using:

```solidity
npm install dotenv
```

Now, let’s create a file called `.env`

.env file is included in .gitignore by default. But it's always better to check once and add .env in .gitignore if it's not already included. This makes sure that this file is ignored by git from future commits.

Inside the .env file, fill in your private key and alchemy HTTP URL as so:

```solidity

ALCHEMY_HTTP_URL="your alchemy http url"
PRIVATE_KEY="your private key"
```

## Test Ether

We will need some test ethers on the Sepolia network to execute the transactions. You can get these tests either from [https://www.alchemy.com/faucets/ethereum-sepolia](https://www.alchemy.com/faucets/ethereum-sepolia)

## That’s a wrap

We are now finally ready to write the deployment script next and deploy our contract on Sepolia Testnet. See you again!!
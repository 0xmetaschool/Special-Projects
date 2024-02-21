# Day 7

Welcome to the Day 7! Firstly, we would like to appreciate you for the immense level of commitment that you have shown for this course. Pat on your back for your great work till now let’s get started for another amazing day of learning! 

## Using Hardhat

Earlier, we wrote a code for our ERC20 token and also wrote code for our Proxy contract. Neither did we compile the code nor tested it. So don’t be surprised if we catch up an unexpected error while testing the code!! It’s all a part of learning! 

Now that we know that we need to compile, test and deploy our code, we are left with certain options which would help us to achieve that. Two of them would be using IDEs called Hardhat and Foundry. We would be going ahead with Hardhat this time. Reasons being the installation would be easy even for windows users which might be a bit of struggle using Foundry. 

## Hardhat Quick Setup

Along with learning and installation guide for the Hardhat that we will provide below, we strongly encourage you to look at the hardhat documentation [here](https://hardhat.org/docs). Learning to read and build from documentation is a great way ahead to be an amazing web3 developer. 

Well, let’s finally start with our hardhat installation. We assume that you already have node.js and Visual Studio Code installed in your system. 

Firstly, create a empty folder and create an npm project using

```solidity
npm init
```

Next, once your project is ready, run the following command

```solidity
npm install --save-dev hardhat
```

Once this is done, we will be creating a sample hardhat project which can be  using

```solidity
npx hardhat init
```

Now, you will get an output like so and will be asked to choose from certain options in order to create hardhat project: 

```solidity
$ npx hardhat init
888    888                      888 888               888
888    888                      888 888               888
888    888                      888 888               888
8888888888  8888b.  888d888 .d88888 88888b.   8888b.  888888
888    888     "88b 888P"  d88" 888 888 "88b     "88b 888
888    888 .d888888 888    888  888 888  888 .d888888 888
888    888 888  888 888    Y88b 888 888  888 888  888 Y88b.
888    888 "Y888888 888     "Y88888 888  888 "Y888888  "Y888

👷 Welcome to Hardhat v2.20.1 👷‍

? What do you want to do? …
❯ Create a JavaScript project
  Create a TypeScript project
  Create a TypeScript project (with Viem)
  Create an empty hardhat.config.js
  Quit
```

We will choose first option - Create a JavaScript Project and press default for rest. Once you are done with that, a hardhat project will be successfully created. 

## Hardhat Commands

Let’s try some most basic hardhat commands.

### Compile

Let’s familiarize ourselves with the basic hardhat commands that we will be using to compile, deploy and test our smart contract. 

Before implementing the smart contract code we wrote in the last section, let’s first work with the sample offered by Hardhat. 

If you go the `contracts` folder, you will see the file called `Lock.sol` and we will try to compile this file using: 

```solidity
npx hardhat compile
```

You should be able to see compilation successful message!! 

### Test

One of the most important aspect of smart contracts is testing the code. You can see the script for testing code in the `test` folder. 

You can simply run this command to test to code:

```solidity
npx hardhat test
```

You will be able to see the following commands:

```solidity
Compiled 2 Solidity files successfully

  Lock
    Deployment
      ✔ Should set the right unlockTime (610ms)
      ✔ Should set the right owner
      ✔ Should receive and store the funds to lock
      ✔ Should fail if the unlockTime is not in the future
    Withdrawals
      Validations
        ✔ Should revert with the right error if called too soon
        ✔ Should revert with the right error if called from another account
        ✔ Shouldn't fail if the unlockTime has arrived and the owner calls it
      Events
        ✔ Should emit an event on withdrawals
      Transfers
        ✔ Should transfer the funds to the owner

  9 passing (790ms)
```

### Deploy

The code for deploying your smart contract is written in the `script` folder. You simply need to run the following command to deploy your smart contract:

```solidity
npx hardhat run scripts/deploy.js
```

You should be able to see something like this once you run the command

```solidity
Lock with 0.001ETH deployed to: 0x5FbDB2315678afecb367f032d93F642f64180aa3
```

## That’s a wrap

We hope you have familiarized yourself with basic hardhat commands. In Day 8, we will be working with our own smart contracts in Hardhat. See you there!

# Day 5

We are so happy to see you in Day 5. In Day 4, we understood tokenomics for our Fan Token. In this section, we will get an understanding of few topics which are needed before we actually start writing our code for the smart contract: 

### ERC20 token contract by Openzeppelin

As mentioned earlier, we will be using ERC20 token standard for our Fan Token. We will be using standard ERC20 token contract from Openzeppelin. Well, one could actually do everything from scratch instead of using standard openzeppelin contracts, but we could introduce several vulnerabilities. Openzeppelin contracts are battle tested, used as industry standard and are available for almost all common standard contracts.

### Immutable nature of smart contracts

So, now that we are clear about why we will be using Openzeppelin contracts, not just for ERC20 but further as well when required, let’s try to understand something which is going to play an important role in our Build in Public series journey. 

You might have heard that smart contracts are immutable. Once you deploy your contract, there is no way to change or modify anything whatsoever. But let’s imagine a situation that your contracts are being used by millions of users and you found a huge vulnerability which can be exploit all your funds. What do you do in such situation? Is there nothing you can do at all even after knowing and put money of millions of people at risk? 

Well, sorry of we scared you!! But you don’t have to worry. To prevent such situations, there exists something called as ‘Proxy smart contract’. Let’s see what exactly it is below: 

### Proxy smart contract

Whenever the situation like above arises, we use Proxy smart contract to upgrade our original contract. But saying upgrade our original smart contract might be a misleading term in here. Because we cannot really upgrade or modify our original contract in any way when it is deployed. 

What Proxy smart contract does is acts as a layer between the user and the original smart contract. The user interacts with original smart contract using a proxy contract. So, when the original contract is needs an update, a new contract with updated functionalities is deployed and the proxy contract now points to the new contract. 

We understand it might be a bit confusing at this time but it will get very clear when we are working with Proxy smart contract. Oh yes, you heard it right!! To be extra cautious, we will be using Proxy smart contract just like all the big protocols do in web3. You can tell, we are going all in to build the most secure project.

## That’s a wrap

We hope you got to learn something new and interesting today. We believe you are now equipped with all the necessary information needed before we start writing code for our smart contract. In the next day content, we will start writing smart contract code and we cannot wait to see you there!!
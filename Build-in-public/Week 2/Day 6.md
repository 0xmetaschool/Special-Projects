# Day 6

We are so thrilled to see you already complete the first week and now getting started with the second week and day 6. Today, we are going to be working on something you have been waiting for a while now - writing our smart contract code. At this stage, its just important to understand the contract and we would be using hardhat in the next section for compiling, deploying and testing purpose.

## ERC20 Token Contract

Let’s start by writing the ERC20 token contract for our Fan token. This would be a very simple contract and for reasons mentioned during the day 5, we will be using openzeppelin contract. 

Below is the code for our ERC20 Fan token contract.  We will not hardcode any value in the contract right now but we can choose our name, symbol and initial supply of tokens during the deployment stage. 

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract FriendsToken is ERC20 {
    constructor(
        string memory name,
        string memory symbol,
        uint256 initialSupply
    ) ERC20(name, symbol) {
        _mint(msg.sender, initialSupply);
    }
}
```

Believe it or not, our token contract is already ready. The next stage is writing our proxy smart contract. If you need to recap what is proxy contract and why it’s important, please go back and check out day 5 before checking out the code for Proxy Smart contract.

## Writing Proxy Smart contract

As mentioned earlier, proxy smart contract will point us to our original smart contract which in our case is our token contract. Here’s the code for the proxy contract

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Proxy {
    address public implementation;
    address public admin;

    event Upgraded(address indexed newImplementation);

    modifier onlyAdmin() {
        require(msg.sender == admin, "Not admin");
        _;
    }

    constructor(address _implementation) {
        implementation = _implementation;
        admin = msg.sender;
    }

    function upgrade(address _newImplementation) external onlyAdmin {
        require(_newImplementation != address(0), "Invalid implementation address");
        implementation = _newImplementation;
        emit Upgraded(_newImplementation);
    }

    fallback() external {
        // delegatecall to the implementation contract
        (bool success, ) = implementation.delegatecall(msg.data);
        require(success, "Delegate call failed");
    }

    receive() external payable {}
}
```

Now, let’s try to understand step by step what our contract is doing: 

Firstly, we need to make sure that only admin which is equivalent to the owner can call certain functions. To ensure that, we can defined a modifier called **onlyAdmin**. In case you you don’t recall, modifiers impose certain conditions on our function.

Next and most important part is our **upgrade** function which should only be abled to be called by admin. The upgrade function takes in address as an argument and updates the address of the token contract it points to. The rest are generic things used in smart contracts.

In short, if the token contract needs to be updated, the admin will use the **upgrade** function to point to  a new token address. 

## That’s a wrap

This was a brief explanation of ERC20 and proxy smart contract but we will understand it even better in when we are deploying. See you all again tomorrow!
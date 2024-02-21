# Day 8

We hope you enjoyed working with the sample Hardhat project in the last section. In this section, we will be replacing the sample contract provided by Hardhat with our Token and Proxy contract. So without wasting any more time, let’s get straight into it! 

## Writing and compiling our smart contract

Firstly, let’s go to the `contracts` folder and delete the `Lock.sol` file. Now let’s create two new files called `FriendsToken.sol` and `Proxy.sol` in the same `contracts` folder.

Inside our `FriendsToken.sol` , paste this smart contract code we had written earlier for our token. 

```solidity
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

Now go to `Proxy.sol` and paste the below code that we had written for Proxy contract:

```solidity
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

## Compiling our Contracts

Now it’s time to compile our contracts. Like mentioned previously, similar to how we compiled the sample project on hardhat, we will compile using:

```solidity
npx hardhat compile
```

As you can see, when we run, we get an error which means that we had forgotten to install openzeppelin contracts. But if you already found out about that error and installed it, you deserve a pat on your back for a great observation!!

```solidity
Error HH411: The library @openzeppelin/contracts, imported from contracts/FriendsToken.sol, is not installed. Try installing it using npm. 
```

To resolve this error, let’s install using:

```solidity
npm install @openzeppelin/contracts
```

Once its installed, run the command to compile again and this time you can see that our files get successfully compiled! 

```solidity
Compiled 7 Solidity files successfully (evm target: paris)
```

Yayy, making something work after resolving an error is so rewarding no matter how small or silly the error was, isn’t it? 

## Testing our smart contract

We cannot emphasize enough how important it is to test your smart contract code. Today, we will be writing the test script for the `FriendsToken.js` . We will keep the explanation for the Day 9 as today’s lesson might go very long.

Go to the `test` folder and create a file called `FriendsToken.js`  and paste the following code: 

```solidity

const { expect } = require("chai");
const { ethers } = require("hardhat");

describe("FriendsToken", function () {
  let FriendsToken;
  let friendsToken;
  let owner;

  beforeEach(async function () {
    FriendsToken = await ethers.getContractFactory("FriendsToken");
    friendsToken = await FriendsToken.deploy("FriendsToken", "FT", 1000000);
    [owner] = await ethers.getSigners();
  });

  it("Should have the correct name, symbol, and initial supply", async function () {
    const name = await friendsToken.name();
    const symbol = await friendsToken.symbol();
    const totalSupply = await friendsToken.totalSupply();
    const ownerBalance = await friendsToken.balanceOf(owner.address);

    expect(name, "Name").to.equal("FriendsToken");
    expect(symbol, "Symbol").to.equal("FT");
    expect(totalSupply, "Total Supply").to.equal(1000000);
    expect(ownerBalance, "Owner Balance").to.equal(1000000);
  });
});

```

Roughly speaking, in the above test code, we are trying to check if our token gets correct Name, Symbol and Initial supply that we will provide during deploying the contract. We provide dummy name ‘FriendsToken’, dummy symbol ‘FT’ and dummy token supply of ‘1000000’ to check if the values get assigned correctly. Don’t worry if you don’t understand it right now. We will go into more details on Day 9.

Now let’s run the following command to test the smart contract code:

```solidity
npx hardhat test
```

We now get the following results:

```solidity
 FriendsToken
    ✔ Should have the correct name, symbol, and initial supply (93ms)

  1 passing (3s)
```

Great job everyone!! We have successfully passed the tests we had written!

## That’s a wrap

We will continue with explaining our test script and deploy our token contract next. After that, we will do the same with our Proxy contract. We hope you got to learn something new today. See you again!!

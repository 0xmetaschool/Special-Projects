# Day 9

Previously, we wrote the script for the test code. Today we will be explaining the test code for our token contract.

## Understanding the test code

The test code we wrote for our token contract previously was like this:

```

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

Now let’s understand the code step by step:

Import Libraries

```
const { expect } = require("chai");
const { ethers } = require("hardhat");
```

- `chai` is a testing library that provides a set of assertion functions for making test cases and comparing the expected result to what we get.
- We are using `ethers` to deploy and interact with smart contracts.

Test Suite Declaration

```
describe("FriendsToken", function () {}
```

- We will be writing our tests inside `describe`. It provides a testing framework that defines the tests for our token smart contract `FriendsToken`.

Variable Declarations

```
let FriendsToken;
let friendsToken;
let owner;
```

- The variables `FriendsToken`, `friendsToken`, and `owner` will be used to store the contract factory, deployed contract instance, and the contract owner's address respectively.

Before Each Test

```
beforeEach(async function () {
  FriendsToken = await ethers.getContractFactory("FriendsToken");
  friendsToken = await FriendsToken.deploy("FriendsToken", "FT", 1000000);
  [owner] = await ethers.getSigners();
});
```

- `beforeEach` is executed before each test case
- `ethers.getContractFactory("FriendsToken")`: Gets the contract factory for the "`FriendsToken`" contract for us to deploy with the set of parameters and interact with the contract
- `FriendsToken.deploy("FriendsToken", "FT", 1000000)`: Deploys the "`FriendsToken`" contract with the specified parameters.
- `ethers.getSigners()`: Gets the list of signers and assigns it to the `owner` variable.

Test Case

```
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
```

- `it` is a function the testing framework provides to define an individual test case.
- `await friendsToken.name()` calls the `name` function on the deployed contract to get its name. Similar calls are made for `symbol`, `totalSupply`, and `balanceOf` to retrieve other contract details as you can see in the code.
- `expect(name, "Name").to.equal("FriendsToken")` checks if the contract's name matches the expected value. Similarly, it checks for the `symbol`, `totalSupply`, and `ownerBalance` matches the expected value.

## That’s a wrap

As we had seen earlier, all our test cases have passed, so our contract is working correctly. We are finally ready to start deploying our token contract. See you again!!
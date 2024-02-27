# Day 11

Welcome to the eleventh day of our build-in public series! I can’t believe we have come so far! Previously, you set up the environment variables for your HardHat project. 

Today, we will write the deployment script for our `FriendsToken` contract. It might look like it needs to be fixed. We still need to figure out what the bug is. But at least we’ve done something. So let’s write it and understand how it works.

## Writing the deployment script

Head over to the `deploy.js` file in your HardHat project and paste the following code.

```
const hre = require("hardhat");

async function main() {
  const FriendsContract = await ethers.getContractFactory("FriendsToken");
  const initialSupply = ethers.parseUnits("100000", 18);
  const friendsContract = await FriendsContract.deploy(
    "Friends",
    "FRIENDS",
    initialSupply
  );
  console.log(`Friends Contract deployed to ${friendsContract.target}`);
}

// We recommend this pattern to be able to use async/await everywhere
// and properly handle errors.
main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```

### Understand the code

Now, let’s understand what we did in our deployment script line by line.

```
const hre = require("hardhat");
```

- This part imports the Hardhat Runtime Environment (`hre`) module, which provides utilities for deploying and interacting with contracts.

```
async function main() {
```

- This line defines an asynchronous function named `main()`, which serves as the entry point for the script. The `async` keyword indicates that this function will contain asynchronous code.

```
const FriendsContract = await ethers.getContractFactory("FriendsToken");
```

- This line uses the `ethers` module to retrieve the contract factory for the `FriendsToken` contract. The contract factory is a JavaScript object that provides methods for deploying new instances of the contract.

```
const initialSupply = ethers.parseUnits("100000", 18);
```

- This line defines the initial supply of tokens. It uses the `parseUnits` function provided by `ethers.js` to convert a numerical value (`100000`) to a unit with 18 decimal places, which is a common standard for Ethereum tokens (represented as wei).

```
const friendsContract = await FriendsContract.deploy(
  "Friends",
  "FRIENDS",
  initialSupply
);
```

- This line deploys a new instance of the `FriendsToken` contract using the contract factory obtained earlier.
- It specifies the name (`"Friends"`), symbol (`"FRIENDS"`), and initial supply of tokens for the contract.

```
console.log(`Friends Contract deployed to ${friendsContract.target}`);
```

- This line prints a message to the console, indicating the address where the `FriendsToken` contract was deployed.

```
// We recommend this pattern to be able to use async/await everywhere
// and properly handle errors.
main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```

- This block calls the `main()` function and uses `.catch()` to handle any errors that might occur during the execution of the asynchronous code.
- If an error occurs, it prints the error message to the console and sets the process exit code to 1, indicating that an error occurred during script execution.

## That’s a wrap

Overall, this script uses Hardhat and `ethers.js` to deploy a contract `FriendsToken` with specified parameters, including the contract's name, symbol, and initial token supply. Once deployed, it prints the address where the contract was deployed.

As we said this deployment file might be buggy, we’ll see the next if it is, then fix and deploy it. Meanwhile, try using this script and deploy the token on the Sepolia network.
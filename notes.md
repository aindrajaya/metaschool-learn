# How to write a Smart Contract and Mint Elon Musk NFT on OpenSea
----------------------------------------------------------
## 1. Getting Started
--> What are we building
gm everyone 🌈, I am Fama and along with Harpal, we are very excited to bring the first ever learning tutorial for developers on MetaSchool. So what are we building today? Today we're gonna write a smart contract and mint an image of Elon Must with the help of that smart contract on blockchain. This project is SO imporatnt, because not only witll it give you basic understanding of how smart contracts work, but will also help you understand how big collections of NFTs are programmaticallyh minted on different NFT platforms, Cool, right?! 
====
--> Prerequsites
We don't require anything special from your end to complete this project. Just be curious, open to learning and be very very very excited for the opportunities ahead. Having said that, it would be great if you have: 
(-) Basic understanding of Object Oriented Programming concepts. I will be talking about inheritance, objects and all. If you don't know about it. Why not take a basic tutorial on this subject here. 
(-) Basic understanding oh how to code in JavaScript
(-) You can run commands on Terminal
(-) You have a 🦊 MetaMask wallet. If not, take this 5 mins tutorial and quickly make an account, we will be using it. 
(-) Lastly….gm! Everyone is welcome at metaschool 🌈 
====
--> Setting Up Environment
Now that we've discussed all that, let's get straight to development. Most of the Ethereum libraries and tools are built on top of JavaScript. This is why I mentioned you needa basic understanding of JavaScritp.
--> First, install Node.js
NodeJS is a Javascript runitime built on Chrome's V8 JavaScript engine. I will leave this link here to help you install Node.js. 
Blockchain is a like a public database and our smart contracts live on that database. This database is publicly available and accessible. Based on ou contract's configuration, anyone or only specific people cna playh around with our contract. Every time we publish a contract on blockchain, it gets an address (a digital footprint) for us to track it. We'll build everything in the Ethereum blockchain and also use Solidity and othre libraries for this project.
Publishing a contract directly on blockchain for learning purpose wil be an expensive deal. Every time we create a new contract, edit the contract or publish it on the blockchain, we incur some costs in the form of ETH, or MATIC. In order to avoid that and test the contracts properly, we wil create a test environment which pretty much replicates the production environment, is free to use, and easy to access.
For this purpose, we will use HardHat. Hardhat gives you a local Ethereum network designed for rapid development. It allows you to deploy your contracts, run your test and debug your code without spending a dime. How cool is that? 😊
--> Now install HardHat 
(-) First make a project directory where you will work and we will install all the dependencies and hardhat there. 
(-) Now open your terminal and run the following commands one by one. Just copy and paste one by one.
```bash
mkdir elonNFT
cd elonNFT
npm init --yes
npm install --save-dev hardhat
```
The abobe commands means that you created a 'elonNFT' folder- and empty one. You etered that folder and initialised the project by making a `package.json` file. Then you installed hardhat in the same folder. If you have followed the instructions properly, and everything went according to the plan, you have Hardhat installed.
(-) Now write the following command on your terminal:
```bash
$ npx hardhat
```
You will see something like this 👇
```Bash Terminal
888    888                      888 888               888
888    888                      888 888               888
888    888                      888 888               888
8888888888  8888b.  888d888 .d88888 88888b.   8888b.  888888
888    888     "88b 888P"  d88" 888 888 "88b     "88b 888
888    888 .d888888 888    888  888 888  888 .d888888 888
888    888 888  888 888    Y88b 888 888  888 888  888 Y88b.
888    888 "Y888888 888     "Y88888 888  888 "Y888888  "Y888
 
👷 Welcome to Hardhat v2.8.3 👷‍
 
? What do you want to do? … 
❯ Create a basic sample project
  Create an advanced sample project
  Create an advanced sample project that uses TypeScript
  Create an empty hardhat.config.js
  Quit
```
We will follow the guide and create a basic sample project. Something like HelloWorld! Just follow through the questions and answer them yes. You will also install some more dependencies; hardhat ether and hardhat waffle in the project. The installation wizard will install those for you. If you haven't received a prompt for that, run the following comand:
```bash
$ npm install --save-dev @nomiclabs/hardhat-ethers ethers @nomiclabs/hardhat-waffle ethereum-waffle chai
```
We will also install a smart contracts library called OpenZeppelin. It will make it easy for us to developm, run and ship smart contracts.
```bash
$ npm install @openzeppelin/contracts
```
And if all that is done, congrats, you have a smart contract ready to go. Yasss!! 🚀 A basic sample project is created for you and you can execute your first ever smart contract. 
====
--> Running your Hello World Smart Contract
Let's go! Write the following code in the terminal and hit enter. Make sure you still are in your project directory in your terminal. 
```bash
$ npx hardhat run scripts/sample-script.js
```
You will see something like this on your terminal.
```bash terminal
$ Compiling 2 files with 0.8.4
$ Solidity compilation finished successfully
$ Deploying a Greeter with greeting: Hello, Hardhat!
$ Greeter deployed to: 0x5FbDB2315678afecb367f032d93F642f64180aa3
```
Congratulations 🎉 you've been successful in deploying your first smart contract to your local blockchain environment without having to code a single line. When you run the above command, your solidity code is converted into bytecode. A new local blockchain is created and your contract is deployed thers. But this blockchain is not permanene, every time you build and run your smart contract, a new blockchain is created in your local environment and the contract is deployed. So it is more like a clean slate- start from scratch. We will get back to it later and figure out a way to deploy our contract permantently. For now, just a piece of informatino for you to digest. 
Also the above long line of numbers is the address where your contract is deployed. Every contract has its own address. Because of hardhat we were able to create a local blockchain environment just like Ethereum where we can deploy contracts and play around with them free of cost. Let's open your project in VSCode or Sublime or any other IDE your prefer. The structure will look something like this. 
```bash terminal
elonNFT
-> artifacts
-> cache
-> contracts
    --- Greeter.sol
-> node_modules
-> scripts
    --- sample-script.js
-> tests
- hardhat.config.js
- package-lock.json
- package.json
```
Do open the `Greeter.sol` file. The `Greeter.sol` is a contract written in Solidity and it is very basic one. Let's go through it step by step.
```sol
//SPDX-License-Identifier: Unlicense
pragme solidity ^0.8.0;

import "hardhat/console.sol";

contract Greeter {
  string private greeting;

  constructor(string memory _greeting){
    console.log("Deploy a Greeter with greeting:", _greeting);
    greeting = _greeting;
  }

  function greet() public view returns (string memory){
    return greeting;
  }

  function setGreeting(string memory _greeting) public {
    console.log("Changing greeting from '%$' to '$%'", greeting, _greeting);
    greeting = _greeting;
  }
}
```
Our greeter file has three parts.
(1). A constructor where we can pass a string type variable called `_greeting`. In our case, we apssed 'Hello Hardhat!'. This is why we saw `Hello Hardhat!` on the terminal.
(2). A function `greet()` which returns the greeting value. It is a readonly functin. It just returns the current value of greeting variable
(3). A function `setGreeting()` where we can set the value of the greeting message. After deploying the contract, we can call this function to change the value of greeting.
Are we good so far? If not join our Discord community and go to the #questions channel and share your concerns there. 
Now let's open the `sample-script.js` in the scripts folder. Hardhat always runs the compile task when running scripts with ist command line interface. If this script is run directly using `node` you may want to call compile manuallyh to make sure everything is compiled.
```js
const hre = require("hardhat");

async function main(){
  const Greeter = await hre.ethers.getContractFactory("Greeter");
  const greeter = await Greeter.deploy("Hello, Hardhat!");
  await greeter.deployed();

  console.log("Greeter deployed to:", greeter.address);
}

main()
  .then(() => process.exit(0))
  .catch((e) => {
    console.log(e);
    process.exit(1);
  })
```
In the above code in function main, we get the contract by using its name Greeter. Once we have that, we call the deployh function and pass the greeting `Hello, Hardhat!` to the constructor. This deploys our contract and then we share the contract address on console. How about you deploy the contract with a different greeting message passed on to the constructor and see how it works? 
====
## 2. Hello World NFT
(https://metaschool.so/courses/how-to-write-a-smart-contract-and-mint-elon-musk-nft-on-opensea/lesson/aca9bde1-dc24-406f-8f12-ed26eeb545d2)
--> Creating and Elon Musk NFT locally
In the contracts folder, create a new file named Elon.sol. This is your new contract file.
```sol
// SPDX-License-Identifier: UNLICENSED\
//Notes 1: this is the version of the solidity we are using in the contract
pragma solidity ^0..8.0;

//Notes 2: This is a given to us by hardhat to debug our code. It is very helpful in local development
import "hardhat/console.sol";

contract ZzNFT{
  //Notes 3: This is our NFT contract and it has a constructor. As soon as the contract is deployed, the constructor is called and we will see a message on terminal. All these to the console log.

  constructor(){
    console.log("This is the Zizou NFT contract!!!!!")
  }
}
```
I have explained everything in the commends above. Now let's edit our scripts file to call this a contract. Also, you should know that for every contract you write, you must create a different contract file. This is the general convention used, it makes easy to manage the code and avoid coding mishaps!
First things first, I will renamve the `sample-scripts.js` file to `run.js` and then I will make some changes to the file. You can go ahead and copy them.
```js
const hre = require("hardhat");

async function main(){
  // Notes 4: We get the contract do deploy
  const ZzNFT = await hre.ethers.getContractFactory("ZzNFT");
  const elon = await ZzNFT.deploy();

  await elon.deployed();

  console.log("ZizouNFT deployed to: ", elon.address);
}

main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });
```
The above code is almost same as our Greeter script. But I have made some changes. Now I am calling it ZzNFT which is our contract name and then deploying it. Once the contract is deployed, we will see the constructor message on scereen and the address where the contract is deployed to.
```bash
Compiling 1 file with 0.8.4Solidity compilation finished successfullyThis is my Elon Musk NFT contract!!Elon NFT deployed to: 0x5FbDB2315678afecb367f032d93F642f64180aa3
```
🎉BOOOOMM!! Your first NFT contract is deployed. Give yourself a pat on the back.
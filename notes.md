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
====
--> Minting an NFT
So far you have a basic understanding of a smart contract and you have already deployed one too. Now, let's get to minting an NFT for you. We will write detailed NFT contract and for that we wil use OpenZeppelin. Remember you installed; it while setting up your workspace.
OpenZeppelin is a reusable and secure smart contracts library, which means that you can import this library, inherit the contracts in your project and get started without having to worry security issues and reinventing the wheel. I'd recommend you to check out their official website, read stuff and get to know more.
For minting NFTs, we will create a basic conract basedf on ERC721- tyhe non-fungible token standard. OpenZeppelin gives us th base ERC721 with all the important functionalities. You can read more about this contract and all functions encapsulated in that contract here. And while you are at it, read all the functions and capabilities that come packaged in this magical library here.
Since we had already created the `zznft.sol` file. We wil just updated it. Don't worry if you don't get anything. Just copy-paste it and I will explain it step-by-step.
Now let me explain the code step.
### Code 1
```sol
pragma solidity ^0.8.0;
```
This code before is the version of Solidity that we are suing in our contract, so you should make sure that the compiler that you used to run this contract have meet the version requirement or newer.
### Code 2
```sol
import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol"; \
import "@openzeppelin/contracts/utils/Counters.sol";
```
Here we are importing ERC721URIStorage contract, this contract contains ERC721 contracts. The metadata part of th NFT contract needs to be stored somewhere else. So we are using an extension of base ERC721 contract which can have URI storage.
We are also importing a library called `Counters.sol`. This is also an OpenZeppelin utility to keep track of NFTs which are to be minted. Let's say our contract has minted 5 NFTs, and now someone makes a call to the contract to mint another NFT. How does the contract keep track that it's the 6th NFT? This hapens via this utility
### Code 3
```sol
contract ZZnft is ERC721URIStorage {
  using Counters for Counters.Counter;
  Counters.Counter private _tokenIds;

  constructor() ERC721("ZizouNFT", "ZZ"){}
}
```
Here we are creating a contract called `Zizou` and inheriting `ERC721URIStorage`. As I mentioned earlier, `Counters` is a utility, a library, so we call it differently as you can see form the code. Then we are creating a `private _tokenIds;` counter with default value as 0. By maing it private, no one outside the contract can call it.
The `constructor` is the first function which is used called when we deploy our contract and all we are doing is specifying ERTC721 and giving it a name `ZizouNFT` and symbol `ZZ`. This name will be reflected in Opensea, Rarible and Etherscan- both the names and syumbol. So `ZizouNFT` is the name of our NFT collection and `ZZ` is the symbol. This constructor function ERC721 is coming from `ERC721URIStorage`. It is not visible here because it is inside this file.
### Code 4
```sol
function minNFT() public returns (uint256){
  _tokenIds.increment();
  uint256 newItemId = _tokenIds.contract();
  _mint(msg.sender, newItemId);
  _setTokenURI(newItemId, "Zizzouu Goal");
  console.log("The NFT ID %s has been minted to %s". newItemId, msg.sender);
  return newItemId;
}
```
This is the function that can be executed externally. See how we have kept its scope public when we are creating this function. This function is not called when the contract is deployed but is called on demand. I have kept it very simple. The function first increments the `_tokenIds` and assigns its value to the `newItemId`.
Then we call a `_mint` function, that takes the address of the person calling this function and the `current _tokenIds`. And then I call `_setTokenURI` function that takes the `current _tokenIds` and the data of the NFT. So, basically the mint function is storing the address where the NFT needs to be minted to along with the `_tokenIds` ajd `_setTokenURI` function stores `_tokenIds` along with the data associated with it. Now let's take a look at our script and see how do we deploy this project and call this function.
### Code 5 - Deploy code
```js
const {ethers} from "@nomiclabs/hardhat-ethers";

async function main(){
  const ZZ = await ethers.getContractFactory("ZizouNFT")
  const zizou = await ZZ.deploy()

  await zizou.deployed();
  console.log("Zizou NFT deployed to:", zizou.address);

  let txn = await zizou.mintNFT();
  await txn.wait();
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```
Havew we are added only two or more lines of code. First we wait for the ElonNFT contract to be deployed and once the contract is deployed, we call the mintNFT function to mint the NFT. The NFT currently doesn't have anything. Don't worry, we will get to that flashy stuff later. When you run the script, you will see something like this.
```bash
The NFT ID 1 has been minted to 0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266
```
And there weeee gooo! Congratulations, using OpenZeppelin ERC721 contract, you successfully created a contract, deployed it on blockchain and then called a function of that contract too. You should be proud of yourself. Now you must be wondering, ‘Fatima! I have been doing everything on my console, when can I see my ElonMusk NFT deployed on real blockchain?’ 
Well, we're moving to that just now. Gear up! 
Btw, if you have any questions, please share in the questions channel in our discord.
====
--> Adding Image to NFT
Every NFT has some data linked to it in the form of JSON format that describes the NFT. We call it metadata. This metadata has a special JSON format and the format needs to be followed if we want our NFT to appear properply on platforms like OpenSea, Rarible, etc.
In the previous lesson, I shared how we wrote 'Hello, world' instead of sharing the Uniform Resource Identifier I mean, the data about the NFT.
Let's look back at it.
```sol
_setTokenURI(newItemId, "Hello, world");
```
Now we will use the standard forat required by NFT platforms to describe the data related to the NFT.
```json
{
  "name":"Zinedine Zidane",
  "description":"One of the best football/soccer player of the world, and magician playmaker.",
  "image":"https://64.media.tumblr.com/2ba8e284401d3279646f503da9b9294c/tumblr_n8390eu4JJ1qdcx1no1_500.jpg",
  "attributes":[
    {
      "trait_type":"Zodiac",
      "value":"Cancer"
    },
    {
      "trait_type":"Height",
      "value":"6'1"
    },
    {
      "trait_type":"Personality Type",
      "value":"ISFP"
    }
  ]
}
```
We will use `jsonkeeper` website to convert my JSON into linkable URL. Here is the url `https://jsonkeeper.com/b/XTRJ`.
I will recommend you to kepp your image hosted somewhere safe, the image can't be altered and it doesn't incur your costs. I am being lazy here and found a website where and image was already hosted. Please never do this for your real NFTs. If your server is down or compromised, the NFT will lose its value and important data.
As NFTSchool describes it.
"When an NFT is created and linked to a digital file that lives on some other system, how the data is linked is critical. There are a few reasons why traditional HTTP links aren't a great fir for the demands of NFTs"
With an HTTP address like:
`https://cloud-bucket.provider.com/my-nft.jpg`
Anyone can fetch the contents of
`m0nft.jpg`
, as long as the owner of the sever pays their bills. However, there's no way to guarantee that the contents of the image are the same as they were when the NFT was created. The sever owner can easily replace the image with something different at any time causing the NFT to change its meaning.
This problems was demonstrated by an artitst who pulled the rug (opens new window) on NFTs he creted by changing their images after htye were minted and sold to others.
```sol
_setTokenIds(newItemId, "https://jsonkeeper.com/b/XTRJ");
```
Let's deploy our contract now. You will see this output.
```bash
Compiling 1 file with 0.8.4
Solidity compilation finished successfullyThe NFT ID 1 has been minted to 0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266
```
We are reaching the very last part of this project where we will deploy this contract to testnet and then production as well.
Are you excited? I am very excited!!!!!!!!!
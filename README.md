# Hello World

This Solidity program is a "DEGEN TOKEN" program that demonstrates the basic syntax and functionality of the Solidity programming language. The purpose of this program is to serve as a starting point for those who are new to Solidity and want to get a feel for how it works.

## Description

This program is a simple contract written in Solidity, a programming language used for developing smart contracts on the Ethereum blockchain. The contract of "TentoToken" is in file named "Tentomushi.sol"


## Getting Started

### Executing program

Open VS code and run this Commmand

```javascript
npm init-y
```

this will initiate your NPM packages

```javascript
npm install --save-dev hardhat
```

then

```javascript
npx hardhat
```

after than paste the following code in degentoken.sol

```javascript

// SPDX-License-Identifier: MIT

pragma solidity ^0.8.24;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";


contract TentoToken is ERC20{
    struct oneItem{
        uint value;
        string name;
    }
    oneItem[] public alloneItems;
    address owner;
    mapping (address => oneItem[]) public userReddem;
    
    constructor() ERC20("TENOTO", "TTO") {
         owner = msg.sender;      
         alloneItems.push(oneItem(200,"NFT BATMAN"));   
         alloneItems.push(oneItem(300,"NFT KALKI"));   
         alloneItems.push(oneItem(100,"NFT JON"));   
    }


    function Mints(address toAddress, uint supply) public {
        require(msg.sender == owner,"Only Owner can min the tokesn");
        _mint(toAddress, supply);
    }

    function Burns(uint supply) public {
        if(balanceOf(msg.sender) < supply){
            revert("You Don't have enough Tokens");
        }

        _burn(msg.sender, supply);
    }

    function getoneItem() public  view returns (oneItem[] memory){
        return alloneItems;
    }

    function getUserReddem() public  view returns (oneItem[] memory){
        return userReddem[msg.sender];
    }

    function NowReddem(uint index) public  {
        require(index > 0 && index < 3, "Please Enter index in range 0 to 2");
        require(balanceOf(msg.sender) >= alloneItems[index].value, "You don't have enough Tokens");

        userReddem[msg.sender].push(alloneItems[index]);
        Burns(alloneItems[index].value);
    }

    // function Reddem()



}


```

To Run the program just clone this repository and update your private key in 'hardhat.config.js' file
to deploy the contract run the following command
```javascript
npx hardhat run scripts/deploy.js --network fuji
```

this will give you the address of your contract

now you can tract this address on SnowTrace or test the contract on Remix.

## Authors

Pulkit Dubey 

## License

This project is licensed under the MIT License - see the LICENSE.md file for details

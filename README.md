# ShreyanshuToken

ShreyanshuToken is an ERC20 token implemented in Solidity programming. This project is for those who are new to Solidity programming, demonstrating the basic syntax and functionality of smart contracts on the Ethereum blockchain.

## Description

ShreyanshuToken is a simple contract written in Solidity, a programming language used for developing smart contracts on the Ethereum blockchain. The contract demonstrates the use of ERC20 tokens, allowing the creation, burning and transfern of tokens. It also includes error handling and pause-unpausing functions in the contract.

## Getting Started

### Executing program

To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., ShreyanshuToken.sol). Copy and paste the following code into the file:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.4.0/contracts/token/ERC20/ERC20.sol";
import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.4.0/contracts/access/Ownable.sol";
import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.4.0/contracts/security/Pausable.sol";

contract ShreyanshuToken is ERC20("Shreyanshu", "SP"), Ownable, Pausable {

    event TokensPurchased(address indexed purchaser, uint256 amount);

    constructor() Ownable() Pausable() {}

    // Function to mint token
    function mintTokens(address to, uint256 amount) public onlyOwner {
        require(to != address(0), "Token cannot be minted to the zero address");
        require(amount > 0, "The amount of minting token must be greater than zero");
        _mint(to, amount);
    }

    // Function to burn token
    function burnTokens(uint256 amount) public {
        require(amount > 0, "The amount of burning token must be greater than zero");
        require(balanceOf(msg.sender) >= amount, "Insufficient balance to burn token");
        _burn(msg.sender, amount);
    }

    // Function to transfer token
    function transferTokens(address to, uint256 amount) public whenNotPaused returns (bool) {
        require(to != address(0), "The token cannot be transferred to the zero address");
        require(amount > 0, "The amount to be transferred must be greater than zero");
        require(balanceOf(msg.sender) >= amount, "Insufficient balance to transfer");
        _transfer(_msgSender(), to, amount);
        return true;
    }

    // Function to buy token
    function buyTokens(uint256 amount) public payable whenNotPaused {
        require(amount > 0, "Amount must be greater than zero");
        _transfer(owner(), msg.sender, amount);
    }

    // Function to pause contract
    function pause() public onlyOwner {
        _pause();
    }

    // Function to unpause contract
    function unpause() public onlyOwner {
        _unpause();
    }
}
```

To compile the code, click on the "Solidity Compiler" tab in the left-hand sidebar. Make sure the "Compiler" option is set to "0.8.20" (or another compatible version), and then click on the "Compile ShreyanshuToken.sol" button.

Once the code is compiled, you can deploy the contract by clicking on the "Deploy & Run Transactions" tab in the left-hand sidebar. Select the "ShreyanshuToken" contract from the dropdown menu, and then click on the "Deploy" button.

Once the contract is deployed, you can interact with it by calling the 'mintToken'function. Click on the "ShreyanshuToken" contract in the left-hand sidebar, and then click on the "mintToken" function and input the account address and the number of token . Finally, click on the "transact" button to execute the function and mint the token.

Like the above mintToken function , we can also execute the other functions of the contract (e.g., 'burnToken' 'transferToken' 'buyToken' 'pause' 'unpause') and all these functions are in the left-hand sidebar, below mintToken function.


## Authors

Shreyanshu Pandey <br> [@shreyanshupandey](pandeyrishi562@gmail.com)

## License

This project is licensed under the MIT License. See the LICENSE file for details.

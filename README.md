# MetacraftersTypesOfFunctions
This project demonstrate a smart contract of ERC20 token. The contract owner can mint tokens to a provided address and any user can burn and transfer tokens.

# Description
Tokens are effectively transferred from one blockchain to another through burn and mint transfers, which burn tokens on the source chain and mint tokens on the destination chain simultaneously. By employing the same mechanism, tokens can be moved between the two chains.

# Getting Started
To run this code go to https://remix.ethereum.org/. Create a new file and (example: MintToken) and paste the code below

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/Ownable.sol";

//ERC20 Token with mint, burn, and transfer functions
contract MintToken is ERC20, Ownable {
    constructor(address initialOwner) ERC20("MintToken", "MT") Ownable(initialOwner) {
        _mint(msg.sender, 1000000 * 10 ** uint(decimals()));
    }

//Mint function - to mint new tokens (only owner can use this function)
    function mint(address account, uint256 amount) public {
        require(msg.sender == owner(), "Only owner can mint new tokens");
        _mint(account, amount);
    }
//Burn function - to burn tokens
    function burn(uint256 amount) public {
        _burn(msg.sender, amount);
    }
//Transfer function- to transfer token (sender to recepient)
    function transfer(address recipient, uint256 amount) public override returns (bool) {
        _transfer(msg.sender, recipient, amount);
        return true;
    }
//Transfer tokens with approval from sender
    function transferFrom(address sender, address recipient, uint256 amount) public override returns (bool) {
        _transfer(sender, recipient, amount);
        _approve(sender, msg.sender, allowance(sender, msg.sender) - amount);
        return true;
    }
}


# Author
Lusaya, Maria Carmela J.

email: 8210131@ntc.edu.ph

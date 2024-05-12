# MetacraftersTypesOfFunctions
This project demonstrate a smart contract of ERC20 token. The contract owner can mint tokens to a provided address and any user can burn and transfer tokens.

# Description
Tokens are effectively transferred from one blockchain to another through burn and mint transfers, which burn tokens on the source chain and mint tokens on the destination chain simultaneously. By employing the same mechanism, tokens can be moved between the two chains.

# Getting Started
To run this code go to https://remix.ethereum.org/. Create a new file and (example: MintToken) and paste the code below

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract MyToken {
    string public name = "MyToken";
    string public symbol = "MTK";
    uint8 public decimals = 18;
    uint256 public totalSupply;

    mapping(address => uint256) public balanceOf;

    event Transfer(address indexed from, address indexed to, uint256 value);
    event Mint(address indexed to, uint256 value);
    event Burn(address indexed from, uint256 value);

    address public owner;

    modifier onlyOwner() {
        require(msg.sender == owner, "Only owner can call this function");
        _;
    }

    constructor(uint256 _initialSupply) {
        totalSupply = _initialSupply * 5 ** uint256(decimals);
        balanceOf[msg.sender] = totalSupply;
        owner = msg.sender;
    }

    function mint(address _to, uint256 _value) public onlyOwner {
        require(_to != address(0), "Invalid recipient address");

        balanceOf[_to] += _value;
        totalSupply += _value;

        emit Mint(_to, _value);
        emit Transfer(address(0), _to, _value);
    }

    function burn(uint256 _value) public {
        require(balanceOf[msg.sender] >= _value, "Insufficient balance");

        balanceOf[msg.sender] -= _value;
        totalSupply -= _value;

        emit Burn(msg.sender, _value);
        emit Transfer(msg.sender, address(0), _value);
    }

    function transfer(address _to, uint256 _value) public returns (bool success) {
        require(_to != address(0), "Invalid recipient address");
        require(_value > 0, "Transfer must be greater than 0");
        require(balanceOf[msg.sender] >= _value, "Insufficient balance");

        balanceOf[msg.sender] -= _value;
        balanceOf[_to] += _value;

        emit Transfer(msg.sender, _to, _value);
        return true;
    }
}

# Author
Lusaya, Maria Carmela J.

email: 8210131@ntc.edu.ph

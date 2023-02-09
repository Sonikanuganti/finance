// SPDX-License-Identifier: MIT

pragma solidity ^0.6.0;

contract Finance {
    // The address of the contract owner.
    address public owner;

    // The current balance of the contract.
    uint256 public balance;

    // The constructor for the contract.
    constructor() public {
        owner = msg.sender;
    }

    // Function to deposit funds into the contract.
    function deposit() public payable {
        require(msg.value > 0, "Cannot deposit 0 value");
        balance += msg.value;
    }

    // Function to withdraw funds from the contract.
    function withdraw(uint256 _amount) public {
        require(balance >= _amount, "Insufficient funds");
        require(_amount > 0, "Cannot withdraw 0 value");
        msg.sender.transfer(_amount);
        balance -= _amount;
    }

    // Function to transfer funds from the contract to another address.
    function transfer(address payable _to, uint256 _amount) public {
        require(balance >= _amount, "Insufficient funds");
        require(_to != address(0), "Invalid address");
        require(_amount > 0, "Cannot transfer 0 value");
        _to.transfer(_amount);
        balance -= _amount;
    }
}

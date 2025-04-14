# smart-contract-database
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SmartContractDatabase {
    struct ContractInfo {
        string name;
        address contractAddress;
        string description;
        address owner;
    }

    mapping(address => ContractInfo) public contracts;
    address[] public contractList;
    
    event ContractAdded(string name, address indexed contractAddress, address indexed owner);
    event ContractRemoved(address indexed contractAddress);

    function addContract(string memory _name, address _contractAddress, string memory _description) public {
        require(contracts[_contractAddress].contractAddress == address(0), "Contract already exists");
        
        contracts[_contractAddress] = ContractInfo({
            name: _name,
            contractAddress: _contractAddress,
            description: _description,
            owner: msg.sender
        });
        contractList.push(_contractAddress);
        
        emit ContractAdded(_name, _contractAddress, msg.sender);
    }
    
    function removeContract(addre

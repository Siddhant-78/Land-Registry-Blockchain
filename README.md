# Land Registry Blockchain  

A decentralized land registry system built with **Solidity** on the **Ethereum blockchain**. This project enables secure land registration, transparent ownership verification, and seamless property transfers using smart contracts.  

## 🚀 Features  
- **Secure Land Registration:** Register land with unique IDs, location, area, and ownership details.  
- **Ownership Transfer:** Easily transfer property ownership through secure smart contracts.  
- **Transparent Verification:** Verify land ownership and details anytime.  
- **Tamper-Proof Records:** Immutable data ensures security and prevents fraud.  

## 💠 Technologies Used  
- **Solidity:** For smart contract development.  
- **Ethereum Blockchain:** To provide a decentralized and secure environment.  
- **Remix IDE:** For writing, testing, and deploying smart contracts.  

## 🎞️ Smart Contract Overview  

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract LandRegistry {
    struct Land {
        uint256 id;
        string location;
        uint256 area;
        address owner;
        bool registered;
    }

    mapping(uint256 => Land) public lands;

    event LandRegistered(uint256 indexed landId, string location, uint256 area, address indexed owner);
    event OwnershipTransferred(uint256 indexed landId, address indexed oldOwner, address indexed newOwner);

    function registerLand(uint256 _id, string memory _location, uint256 _area) public {
        require(!lands[_id].registered, "Land already registered");
        lands[_id] = Land(_id, _location, _area, msg.sender, true);
        emit LandRegistered(_id, _location, _area, msg.sender);
    }

    function transferOwnership(uint256 _id, address _newOwner) public {
        Land storage land = lands[_id];
        require(land.registered, "Land not registered");
        require(land.owner == msg.sender, "Only the owner can transfer ownership");
        address oldOwner = land.owner;
        land.owner = _newOwner;
        emit OwnershipTransferred(_id, oldOwner, _newOwner);
    }

    function getLand(uint256 _id) public view returns (uint256, string memory, uint256, address, bool) {
        Land memory land = lands[_id];
        require(land.registered, "Land not registered");
        return (land.id, land.location, land.area, land.owner, land.registered);
    }
}
```

## ⚡ Getting Started  

1. **Clone the Repository:**  
   ```bash
   git clone https://github.com/Siddhant-78/Land-Registry-Blockchain.git
   ```  

2. **Open in Remix IDE:**  
   - Go to [Remix IDE](https://remix.ethereum.org/).  
   - Create a new file and paste the smart contract code.  
   - Compile the code with Solidity version `^0.8.0`.  
   - Deploy the contract to a local or test network.  

3. **Interact with the Contract:**  
   - Use the functions `registerLand()`, `transferOwnership()`, and `getLand()` to test features.  

## 💡 Use Cases  
- Secure land registration for property owners.  
- Fraud-proof property transfers.  
- Transparent verification for buyers, sellers, and government bodies.  

## 🙌 Contributing  
Contributions are welcome! Feel free to fork the repository, submit pull requests, or open issues for improvements.  




# Decentralized Stablecoin Deployment with Foundry

## Overview
This project implements a **Decentralized Stablecoin (DSC)** system using Solidity and Foundry. It includes smart contracts for the stablecoin itself, an engine to manage its issuance and collateralization, and deployment scripts for different networks.

## Project Structure
```
├── src/
│   ├── DecentralizedStableCoin.sol  # Stablecoin contract
│   ├── DSCEngine.sol                # Engine managing collateral and issuance
│
├── test/
│   ├── mocks/
│   │   ├── MockV3Aggregator.sol     # Mock price feed for local testing
│
├── script/
│   ├── DeployDSC.s.sol              # Deployment script
│   ├── HelperConfig.s.sol           # Configuration for different networks
│
├── foundry.toml                     # Foundry configuration file
└── README.md                         # Project documentation
```

## Smart Contracts

### **1. DecentralizedStableCoin.sol**
- Implements an ERC20-based stablecoin.
- Ownership is transferred to `DSCEngine` for decentralized control.

### **2. DSCEngine.sol**
- Manages the issuance and redemption of the stablecoin.
- Ensures stability through over-collateralization using ETH and BTC.

## Deployment Scripts

### **DeployDSC.s.sol**
- Fetches network-specific configurations from `HelperConfig`.
- Deploys `DecentralizedStableCoin` and `DSCEngine`.
- Transfers ownership of DSC to `DSCEngine`.

### **HelperConfig.s.sol**
- Defines configurations for Sepolia and Anvil networks.
- Uses real price feeds on Sepolia and mocks for local testing.
- Reads environment variables for private keys when deploying to Sepolia.

## Setup & Deployment

### **Prerequisites**
- [Foundry](https://book.getfoundry.sh/getting-started/installation)
- Node.js (for environment variable management)

### **Installation**
```sh
git clone <repository_url>
cd <project_directory>
forge install  # Install dependencies
```

### **Running Tests**
```sh
forge test
```

### **Local Deployment (Anvil)**
```sh
anvil &  # Start Anvil (local Ethereum testnet)
forge script script/DeployDSC.s.sol:DeployDSC --fork-url http://127.0.0.1:8545 --broadcast
```

### **Testnet Deployment (Sepolia)**
1. Set your `.env` file:
   ```sh
   PRIVATE_KEY=<your_private_key>
   ```
2. Deploy:
   ```sh
   forge script script/DeployDSC.s.sol:DeployDSC --rpc-url <sepolia_rpc_url> --broadcast
   ```

## License
This project is licensed under the **MIT License**.

---
If you have any questions, feel free to reach out! 🚀


# Hardhat Boilerplate

A production-ready Hardhat boilerplate with TypeScript, multi-network support, and best practices.

## Features

- Solidity 0.8.20 with optimizer and viaIR enabled
- TypeScript support with TypeChain
- Multi-network configuration (local, testnet, mainnet)
- OpenZeppelin contracts included
- Gas reporting and coverage tools
- Contract verification support (Etherscan, Basescan)
- No `.env` file - uses Hardhat vars for secure configuration

## Project Structure

```
├── contracts/          # Solidity smart contracts
├── scripts/            # Deployment scripts
├── test/               # Test files
├── artifacts/          # Compiled contracts (generated)
├── cache/              # Hardhat cache (generated)
├── typechain-types/    # TypeChain types (generated)
├── hardhat.config.ts   # Hardhat configuration
├── tsconfig.json       # TypeScript configuration
└── package.json        # Dependencies and scripts
```

## Quick Start

### 1. Install Dependencies

```bash
npm install
```

### 2. Compile Contracts

```bash
npm run compile
```

### 3. Run Tests

```bash
npm test
```

---

## Configuration (Hardhat Vars)

This project uses **Hardhat vars** instead of `.env` files for secure configuration.

### Setting Variables

```bash
# Required for deployment to testnet/mainnet
npx hardhat vars set DEPLOYER_PRIVATE_KEY

# Required for contract verification
npx hardhat vars set ETHERSCAN_API_KEY     # For Ethereum networks
npx hardhat vars set BASESCAN_API_KEY      # For Base networks

# Optional: Custom RPC URLs (defaults provided)
npx hardhat vars set SEPOLIA_RPC_URL
npx hardhat vars set BASE_SEPOLIA_RPC_URL
npx hardhat vars set MAINNET_RPC_URL
npx hardhat vars set BASE_RPC_URL

# Optional: For gas reporting in USD
npx hardhat vars set COINMARKETCAP_API_KEY
```

### Viewing Variables

```bash
npx hardhat vars list
```

### Deleting Variables

```bash
npx hardhat vars delete VARIABLE_NAME
```

---

## Deployment Guide

### Available Networks

| Network      | Chain ID | Type       | Command                       |
|--------------|----------|------------|-------------------------------|
| hardhat      | 31337    | Local      | `npm test` (in-memory)        |
| localhost    | 31337    | Local      | `npm run deploy:local`        |
| sepolia      | 11155111 | Testnet    | `npm run deploy:sepolia`      |
| baseSepolia  | 84532    | Testnet    | `npm run deploy:base-sepolia` |
| mainnet      | 1        | Production | `npm run deploy:mainnet`      |
| base         | 8453     | Production | `npm run deploy:base`         |

---

### Local Deployment

Deploy to a local Hardhat node for development and testing.

#### Step 1: Start Local Node

```bash
npm run node
```

This starts a local Ethereum node at `http://127.0.0.1:8545` with pre-funded accounts.

#### Step 2: Deploy (in a new terminal)

```bash
npm run deploy:local
```

---

### Sepolia Testnet Deployment

Deploy to Ethereum Sepolia testnet.

#### Prerequisites

1. Get Sepolia ETH from a faucet:
   - https://sepoliafaucet.com
   - https://www.alchemy.com/faucets/ethereum-sepolia

2. Set your deployer private key:
   ```bash
   npx hardhat vars set DEPLOYER_PRIVATE_KEY
   ```

3. (Optional) Set a custom RPC:
   ```bash
   npx hardhat vars set SEPOLIA_RPC_URL
   ```

#### Deploy

```bash
npm run deploy:sepolia
```

#### Verify Contract

```bash
npx hardhat verify --network sepolia <CONTRACT_ADDRESS> <CONSTRUCTOR_ARGS>
```

---

### Base Sepolia Testnet Deployment

Deploy to Base Sepolia testnet.

#### Prerequisites

1. Get Base Sepolia ETH:
   - Bridge from Sepolia: https://bridge.base.org
   - Or use faucet: https://www.coinbase.com/faucets/base-ethereum-goerli-faucet

2. Set your deployer private key:
   ```bash
   npx hardhat vars set DEPLOYER_PRIVATE_KEY
   ```

3. (Optional) Set BaseScan API key for verification:
   ```bash
   npx hardhat vars set BASESCAN_API_KEY
   ```

#### Deploy

```bash
npm run deploy:base-sepolia
```

#### Verify Contract

```bash
npm run verify:base-sepolia <CONTRACT_ADDRESS> <CONSTRUCTOR_ARGS>
```

---

### Production Deployment (Mainnet)

Deploy to Ethereum mainnet or Base mainnet.

#### Prerequisites

1. **IMPORTANT**: Ensure you have real ETH in your deployer wallet
2. Double-check your contract code and tests
3. Consider a security audit for production contracts

4. Set your deployer private key:
   ```bash
   npx hardhat vars set DEPLOYER_PRIVATE_KEY
   ```

5. Set API keys for verification:
   ```bash
   npx hardhat vars set ETHERSCAN_API_KEY   # For Ethereum mainnet
   npx hardhat vars set BASESCAN_API_KEY    # For Base mainnet
   ```

#### Deploy to Ethereum Mainnet

```bash
npm run deploy:mainnet
```

#### Deploy to Base Mainnet

```bash
npm run deploy:base
```

#### Verify on Mainnet

```bash
# Ethereum
npm run verify:mainnet <CONTRACT_ADDRESS> <CONSTRUCTOR_ARGS>

# Base
npm run verify:base <CONTRACT_ADDRESS> <CONSTRUCTOR_ARGS>
```

---

## Available Scripts

| Script                    | Description                           |
|---------------------------|---------------------------------------|
| `npm run compile`         | Compile contracts                     |
| `npm test`                | Run tests                             |
| `npm run test:coverage`   | Run tests with coverage report        |
| `npm run test:gas`        | Run tests with gas reporting          |
| `npm run node`            | Start local Hardhat node              |
| `npm run deploy:local`    | Deploy to localhost                   |
| `npm run deploy:sepolia`  | Deploy to Ethereum Sepolia            |
| `npm run deploy:base-sepolia` | Deploy to Base Sepolia            |
| `npm run deploy:mainnet`  | Deploy to Ethereum mainnet            |
| `npm run deploy:base`     | Deploy to Base mainnet                |
| `npm run clean`           | Clean build artifacts                 |
| `npm run typechain`       | Generate TypeChain types              |

---

## Adding Your Own Contracts

1. Create your contract in `contracts/`
2. Update `scripts/deploy.ts` for your contract
3. Write tests in `test/`
4. Compile and test:
   ```bash
   npm run compile
   npm test
   ```

---

## Security Considerations

- Never commit private keys
- Use Hardhat vars (not `.env`) for sensitive data
- Audit contracts before mainnet deployment
- Test thoroughly on testnets first
- Use OpenZeppelin contracts when possible

---

## Resources

- [Hardhat Documentation](https://hardhat.org/docs)
- [Solidity Documentation](https://docs.soliditylang.org)
- [OpenZeppelin Contracts](https://docs.openzeppelin.com/contracts)
- [Etherscan](https://etherscan.io)
- [Basescan](https://basescan.org)

---

## License

MIT

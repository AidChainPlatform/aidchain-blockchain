# AidChain Blockchain

AidChain Blockchain contains the blockchain and smart-contract layer for the AidChain platform. It combines a Hyperledger Besu QBFT network, smart-contract deployment tooling, and a Node/Express service layer that exposes blockchain operations to the rest of the platform.

This repository is published as a clean portfolio snapshot. Project provenance is documented in [PROVENANCE.md](./PROVENANCE.md).

## What This Repository Covers

- Hyperledger Besu network configuration
- QBFT validator-node setup
- Solidity smart contracts and deployment scripts
- blockchain-facing HTTP routes for accounts, escrow, and transactions
- support utilities for contract interaction and API documentation

## Platform Position

```text
AidChain clients -> AidChain API -> AidChain Blockchain -> Besu QBFT network
```

The backend API uses this service to translate business events into on-chain operations.

## Tech Stack

- Hyperledger Besu
- QBFT consensus
- Solidity
- Hardhat
- Truffle configuration
- Node.js / Express
- ethers.js and Ethereum tooling
- Docker Compose
- Swagger / OpenAPI-related assets

## Repository Layout

```text
besu/                 local blockchain network definition
contracts/            Solidity contracts
migrations/           deployment migration files
scripts/              deployment and support scripts
src/
  routes/
    Account/
    Escrow/
    Transaction/
    UserMgt/
  connectWeb3/        web3 connection helpers
  middleware/         request middleware
  docs/               API docs assets
config/               app and chain configuration
artifacts/            compiled contract artifacts
nginx/                reverse-proxy configuration
```

## Main Capabilities

- local multi-node Besu network startup
- token and escrow contract deployment
- account and transaction endpoints for backend integration
- API wrappers around smart-contract flows
- contract artifact management for downstream consumers

## Prerequisites

- Node.js 18+ recommended
- npm
- Docker and Docker Compose
- JavaScript toolchain for Hardhat/Truffle workflows

## Installation

```bash
npm install
```

## Environment Setup

Create your own `.env` file for local execution. The published snapshot excludes runtime secrets.

Typical values include:

```bash
PRIVATE_KEY=
RPC_URL=http://127.0.0.1:8545
ETHERSCAN_API_KEY=
ADMIN_TEST=
ADMIN_PASS_TEST=
PORT=3000
```

A sanitized `.env.example` can be used as a starting point where applicable.

## Run the Service

```bash
npm run dev
```

or

```bash
npm start
```

## Start the Besu Network

This repo includes Besu network assets and Docker compose files for local QBFT execution.

```bash
docker-compose up -d
```

Depending on your setup, you may also use the dedicated network files inside `besu/`.

## Contract Deployment

Typical Hardhat deployment flow:

```bash
npx hardhat run scripts/deploy.js --network besu
```

Adjust the network configuration to match your local or staging chain.

## Testing

```bash
npm test
```

## API Surface

Route groups in `src/routes/` include:

- `Account`
- `Escrow`
- `Transaction`
- `UserMgt`

These routes are intended to be consumed by the backend API and internal operational flows.

## Related Repositories

- `AidChainPlatform/aid-api`
- `AidChainPlatform/aidchain-ngo`
- `AidChainPlatform/aidchain-admin`

## Notes

- This repo contains both chain infrastructure and an application-facing blockchain wrapper.
- The published org repository is a clean snapshot without prior git history.
- Do not commit private keys or chain credentials.

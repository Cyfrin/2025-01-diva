# AaveDIVAWrapper

### Prize Pool

- Total Pool - $15,000
- H/M -  $14,000
- Low - $1,000

- Starts: January 24, 2025 Noon UTC
- Ends: January 31, 2025 Noon UTC

- nSLOC: 519

[//]: # (contest-details-open)

## About

AaveDIVAWrapper is a smart contract that acts as a **connector between [DIVA Protocol](https://github.com/divaprotocol/diva-protocol-v1/blob/main/DOCUMENTATION.md) and [Aave V3](https://discord.com/channels/602826299974877205/636902500041228309/1251248830767169729)**, allowing assets deposited into DIVA Protocol pools to **generate yield by supplying them on Aave V3**. The generated **yield is claimable by the owner** of the AaveDIVAWrapper contract.

The AaveDIVAWrapper contract was originally designed for DIVA Donate on Arbitrum, a parametric conditional donations platform, which aims to use the yield to purchase insurance policies to increase donation payouts beyond users' initial contributions. However, the contract can be utilized for any other use case enabled by DIVA Protocol (e.g., prediction markets, structured products, etc.).

### Relevant links

#### AaveDIVAWrapper:
- [AaveDIVAWrapper Documentation (Github)](../DOCUMENTATION.md)
- [AaveDIVAWrapper Codebase](https://github.com/Walodja1987/AaveDIVAWrapper)

#### DIVA Donate:
- [DIVA Donate Website/App](https://www.divadonate.xyz/)
- [DIVA Donate Documentation (Gitbook)](https://docs.divadonate.xyz/)
- [DIVA Donate App Codebase](https://github.com/Walodja1987/DIVA-Donate-App)

#### DIVA Protocol:
- [DIVA Protocol Website](https://www.divaprotocol.io/)
- [DIVA Protocol Documentation (Github)](https://github.com/divaprotocol/diva-protocol-v1/blob/main/DOCUMENTATION.md)
- [DIVA Protocol Documentation (Gitbook)](https://docs.divaprotocol.io/)
- [DIVA Protocol Codebase](https://github.com/divaprotocol/diva-protocol-v1)

#### Aave:
- [Aave Website](https://aave.com/)
- [Aave V3 Documentation](https://aave.com/docs)
- [Aave V3 Codebase](https://github.com/aave/aave-v3-origin)

## Actors

Actors:
- **Users:** Can create pools, add/remove liquidity, redeem position tokens, and convert wrapped collateral tokens back to the original token.
- **Owner:** Can register collateral tokens and claim yield generated from Aave deposits.
- **Data providers/oracles:** Resolve pools by reporting the outcome via DIVA Protocol.

[//]: # (contest-details-close)

[//]: # (scope-open)

## Scope (contracts)

The following contracts in `contracts/src/` are in scope:

```js
src/
├── AaveDIVAWrapper.sol
├── AaveDIVAWrapperCore.sol
├── WToken.sol
├── interfaces
│   └── IAave.sol
│   └── IAaveDIVAWrapper.sol
│   └── IDIVA.sol
│   └── IWToken.sol

```

## Compatibilities

AaveDIVAWrapper contract will be deployed on EVM-compatible chains where both DIVA Protocol and Aave V3 are available. These include:

- Ethereum Mainnet
- Polygon
- Arbitrum One
- Gnosis Chain
- Ethereum Sepolia (Testnet)

Supported collateral tokens:
- Any ERC20 token supported by Aave V3, but mainly stablecoins like USDC, USDT are expected to be used for DIVA Donate.
- Fee-on-transfer and rebaseable tokens are NOT supported.
- Tokens must have between 6-18 decimals.

[//]: # (scope-close)

[//]: # (getting-started-open)

## Setup

Install `pnpm` (if not already installed):

```bash
npm install -g pnpm
```

Build:
```bash
pnpm install
```

Configuration:
```bash
npx hardhat vars set PRIVATE_KEY
```

Tests:
```bash
pnpm test:hh
```

[//]: # (getting-started-close)

[//]: # (known-issues-open)

## Known Issues

- The AaveDIVAWrapper contract becomes useable only after the owner has registered collateral tokens post contract deployment.
- Aave V3 is upgradeable and could introduce breaking changes, though the risk is deemed low as AaveDIVAWrapper only uses core functions.
- Integration risk with both Aave V3 and DIVA Protocol - vulnerabilities in either protocol may affect AaveDIVAWrapper.
- Fee-on-transfer and rebaseable tokens are not supported but also not prevented on code level (same as in Aave V3).
- Direct ETH deposits are not supported (requires wrapper contract).
- Yield rounding issues could temporarily prevent yield claims if aToken balance becomes smaller than wToken supply.

**Additional Known Issues detected by LightChaser are available [here](https://github.com/Cyfrin/2025-01-diva/issues/7).**

[//]: # (known-issues-close)

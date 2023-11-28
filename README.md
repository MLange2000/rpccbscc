# RPC-Based Cross-Blockchain Smart Contract Calls (rpccbscc)
A Framework for Asynchronous Cross-Blockchain Smart Contract Calls as extension to [@soberm](https://github.com/soberm/ccsc)'s Framework.

Attention: Work in Progress!

## General Description

In the framework by [@soberm](https://github.com/soberm/ccsc), the source blockchain contains the client and the target blockchain, the server. The framework uses stub contracts on the client and on the server side, which are called by an external user, which is, in most cases, the owner of the issuing transaction to the stub-smart contract. On both sides, there are also relays to provide a mechanism for cross-blockchain communication. The Relays are based on the client side on an ETH-relay and on the server side on implementation by a BSC-relay using PoS Consensus. To keep the Relays up to date, so-called relayers as off-chain clients have to forward the blocks added to the specific blockchain. An Incentive Mechanism checks that a cross-blockchain call is executed completely. This ensures there is no inconsistency regarding the state of the blockchain. In short, the client is called to call a Client Stub function that prepares and extends the metadata for the cross-blockchain call. The Server Stub is then called, and after validation with the destination's blockchain relay, it executes the function. The data is then transferred back and checked by the client stub relay on the source blockchain.

## New Features Of This Extension

This Implementation was done as part of a research project at the [Institute for Data Engineering](https://www.tuhh.de/ide/homepage) at Hamburg University of Technology.

The Framework is extended in the way that:
* it implements a solution for the stub-contracts to automatically generate these with a simple Interface Definition Language or even with the Application Binary Interface of the different contracts
* the old framework was implemented with Ethereum using the PoW consensus mechanism -> new framework will work with the new Ethereum PoC consensus

### Prerequisites

* [Hardhat](https://hardhat.org/)
* [Golang](https://go.dev/)
* [Solidity](https://docs.soliditylang.org/en/v0.8.10/)

### Installing the example contracts

1. Deploy [ETH-Relay-Verilay](https://github.com/pantos-io/research-ethrelay) and [BSC-Relay](https://github.com/soberm/bsc_relay).
2. Change into the contract directory: `cd ccsc_contracts/`
3. Install all dependencies: `npm install`
4. Change the network configuration in `hardhat.config.js`
5. Update the addresses for ETH-Relay and BSC-Relay in `./scripts/deploy.js`
6. Run `hardhat run ./scripts/deploy.js` to deploy the example on the configured networks

### Installing the example caller

1. Change into the contract directory: `cd ccsc_go/`
2. Build the example caller with `go build -o example_caller ./cmd/main.go`
3. Adapt the configuration in `./configs/config.json`
4. Run the example caller with `./example_caller`

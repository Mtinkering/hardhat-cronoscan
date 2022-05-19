[![npm](https://img.shields.io/npm/v/@nomiclabs/hardhat-etherscan.svg)](https://www.npmjs.com/package/@nomiclabs/hardhat-etherscan) [![hardhat](https://hardhat.org/buidler-plugin-badge.svg?1)](https://hardhat.org)

# hardhat-cronoscan

## This is a fork of hardhat-etherscan

[Hardhat](https://hardhat.org) plugin for integration with [Cronoscan](https://cronoscan.com)'s contract verification service.

## What

This plugin helps you verify the source code for your Solidity contracts on [Cronoscan](https://cronoscan.com).

It's smart and it tries to do as much as possible to facilitate the process:

- Just provide the deployment address and constructor arguments, and the plugin will detect locally which contract to verify.
- If your contract uses Solidity libraries, the plugin will detect them and deal with them automatically. You don't need to do anything about them.
- A simulation of the verification process will run locally, allowing the plugin to detect and communicate any mistakes during the process.
- Once the simulation is successful the contract will be verified using the Etherscan API.

## Installation

```bash
npm install --save-dev @eaglewalker/hardhat-cronoscan

// or

yarn add --dev @eaglewalker/hardhat-cronoscan
```

And add the following statement to your `hardhat.config.js`:

```js
require("@eaglewalker/hardhat-cronoscan");
```

Or, if you are using TypeScript, add this to your `hardhat.config.ts`:

```js
import "@eaglewalker/hardhat-cronoscan";
```

## Tasks

This plugin provides the `verify` task, which allows you to verify contracts through Cronoscan's service.

## Environment extensions

This plugin does not extend the environment.

## Usage

You need to add the following Cronoscan config to your `hardhat.config.js` file:

```js
module.exports = {
  networks: {
    mainnet: { ... }
  },
  etherscan: {  // this is still etherscan. to avoid complexity
    // Your API key for Cronoscan
    // Obtain one at https://cronoscan.com/
    apiKey: "YOUR_CRONOSCAN_API_KEY"
  }
};
```

Alternatively you can specify more than one block explorer API key, by passing an object under the `apiKey` property, see [`Multiple API keys and alternative block explorers`](#multiple-api-keys-and-alternative-block-explorers).

Lastly, run the `verify` task, passing the address of the contract, the network where it's deployed, and the constructor arguments that were used to deploy it (if any):

```bash
npx hardhat verify --network mainnet DEPLOYED_CONTRACT_ADDRESS "Constructor argument 1"
```

### Complex arguments: Check hardhat-etherscan

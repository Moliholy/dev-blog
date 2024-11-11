---
title: Blacklist Pallet
date: "2024-11-11T00:00:00.000Z"
description: "My first pallet: Blacklist Pallet on Substrate"
---

## Introducing the Blacklist Pallet: Enhancing Security in Substrate-Based Blockchains

Hi there! Welcome to my very first blog post. My name is José, and I’m a Substrate engineer currently working at
**BlockDeep Labs**. Previously, I had the incredible opportunity to work at **Parity Technologies**, where I honed my
skills in blockchain development and Substrate.

This post is particularly special to me because it showcases the **very first Substrate pallet I ever wrote** — the **Blacklist Pallet**.
I designed it to be simple yet effective, and it holds a lot of sentimental value as a foundational
milestone in my career as a blockchain developer.

### Why I Created the Blacklist Pallet

The idea for this pallet came to me when I noticed something curious: Substrate already has a **Whitelist Pallet**, but
there was no equivalent for managing blacklists. This observation sparked a thought—why not create a complementary
solution? With that, I set out to write my first pallet, keeping the scope straightforward to ensure it would be useful
without overcomplicating things.

The result? A lightweight and flexible tool for enhancing security in Substrate-based blockchains.

### What Does the Blacklist Pallet Do?

The Blacklist Pallet allows administrators to restrict specific accounts from performing certain actions within the
network. By enabling a configurable origin—typically the Root origin—to manage a blacklist, this pallet strengthens the
security framework of any blockchain it is integrated into.

#### Key Features

- **Account Blacklisting**: Add accounts to a blacklist to prevent them from executing designated actions.
- **Event Emission**: Emit an `AccountBlacklisted` event when an account is blacklisted, providing transparency.
- **Blacklist Removal**: Remove accounts from the blacklist and emit a `BlacklistedAccountRemoved` event.

#### How It Works

Here’s a quick breakdown of the extrinsics (or dispatchable functions) in the pallet:

1. **`blacklist_account`**: Adds an account to the blacklist.
    - **Parameters**:
        - `origin`: Must be a `Root` origin or relevant governance.
        - `accountId`: The account to blacklist.
    - **Errors**:
        - `AccountAlreadyBlacklisted`: The account is already blacklisted.

2. **`remove_blacklisted_account`**: Removes an account from the blacklist.
    - **Parameters**:
        - `origin`: Must be a `Root` origin.
        - `accountId`: The account to remove.
    - **Errors**:
        - `AccountNotBlacklisted`: The account is not on the blacklist.

#### Why It Matters

This pallet is a simple yet powerful addition to the Substrate ecosystem. It helps maintain the integrity of a
blockchain by enabling administrators to manage blacklists effectively. Whether you're building a permissioned or
permissionless network, having a blacklist option is a practical tool for addressing security concerns.

### How to Integrate the Blacklist Pallet

If you'd like to try out the Blacklist Pallet in your own Substrate-based blockchain, here’s how to get started:

1. **Update Dependencies**: Add the following to your `Cargo.toml`:

   ```toml
   [dependencies]
   pallet-blacklist = { version = "1.0.0", default-features = false, git = "https://github.com/Moliholy/pallet-blacklist.git" }

2. **Configure the Pallet**: Implement the pallet_blacklist::Config for your runtime:

```rust
impl pallet_blacklist::Config for Runtime {
    type RuntimeEvent = RuntimeEvent;
    type BlacklistingOrigin = EnsureRoot<AccountId>;
    type WeightInfo = ();  // compute the actual weights!
}
```

3. **Include It in the Runtime**: Add the pallet to your runtime via the `construct_runtime!` macro:

```rust
construct_runtime! {
    pub struct Runtime {
        // -- snip --
        Blacklist: pallet_blacklist,
    }
}
```

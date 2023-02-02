# Assignment #4 Instructions

This assignment will be focused on understanding the reserve asset transfer mechanism in XCM between chains.
You are provided a the means to start a relay chain and parachain node network, where key `xcm_config.rs` components are missing need to be completed.
Once configured, a reserve asset transfer of relay chain assets to a parachain will be required, and implemented in the XCM simulator.

## Instructions

This repo contains a customized [parachain template based on the `polkadot-v0.9.37` release](https://github.com/substrate-developer-hub/substrate-parachain-template/releases/tag/polkadot-v0.9.37) with some missing and/or erroneous XCM configurations.

The `xcm-executor` for use with the XCM Simulator includes some `log::debug!(...)` lines should prove useful, printed with:

```sh
RUST_LOG="debug" cargo test -- --nocapture
```

### 📜 Parachain XCM Configuration ([`./runtime/src/xcm_config.rs`](./runtime/src/xcm_config.rs))

You need to correct and/or complete the provided XCM configurations to accomplish the assignment objectives:

- **Barrier**: You can configure the Barrier in the way you consider best.
  Please note that copying and pasting from other parachains might not work as expected for this assignment.
  So please be mindful of your Barrier setup.

- **AssetTransactor**: The easiest way to configure this is by using the transactor related to the `pallet_balance`.
  This is the minimum accepted solution for this configuration.

  - Local transactor: For handling local assets.

  - _Optional_ : Add the Fungible transactor and instead of minting the received asset using the `pallet_balance`, use the `pallet_assets` to mint a derived (a.k.a wrapped) asset for the relay chain.

- **IsReserve**: Configure the parachain to recognize the relay chain as the valid reserve of assets.

- **Filters**: As the calls from `pallet_xcm` are not supposed to be used in the parachain, all the corresponding filters are set to `Nothing`.
  Please do not change anything from it.

### 🔽 Reserved Asset transfer from relay chain to a parachain

Send some native relay chain assets to the connected parachain template by executing a reserve asset transfer.
See the `limitedReservedTransferAssets` from the `xcmPallet` from sending relay chain assets to the parachain.
You need to define this transfer as a new test entry in the XCM simulator.

_Optional_: Instead of using the extrinsic `limitedReservedTransferAssets` from the `xcmPallet`, you can build the XCM message by your own.

### _Optional_ 🔼 Build a pallet that sends the token back to the relay chain.

For sending the relay chain assets back from the parachain to the relay chain, you will have to create a new pallet with a specific call that commits this purpose.
The logic for the pallet shouldn't be super complex as its only purpose is to send the XCM message only.
Also the pallet should be added in the XCM simulator as a separate test, so we can validate the correct functioning of the pallet.

## Grading

Your implementation will be assessed for:

- Implementation
  - Correctness and accuracy
  - Evidence of using various techniques used in class
  - As close to production ready as possible
- Code Quality
  - Tests and code coverage
  - Use of best practices and efficient code
  - Well documented, with considerations and compromises noted
- Bonus Points
  - Completing _Optional_ tasks, mentioned above
  - Incontestably going above and beyond the requirements above

## README

Graders will start by reviewing your updated [README.md](./README.md) that should describe at a minimum:

- How you designed your config and why
- Any compromises you made, and things you would improve if you had time
- How to run the project

Graders should have no issue in running and testing this project, and be able to understand what to expect to see before reviewing any of your code.

# Polkadot and XCM Config
My XCM config is as follows

### Barrier
My Barrier was set to require only unpaid transactions from the relay. The reason for this was because i wanted to test the differences of both attributes
for paid and unpaid executions on the relay and parachain but obviously in reality you want everything to be a paid execution to have a more trustless way of communicating between the relay and parachain

```rust 
pub type Barrier = (
	AllowTopLevelPaidExecutionFrom<Everything>,
	AllowUnpaidExecutionFrom<ParentOrParentsUnitPlurality>,
);
```

### AssetTransactor
For Fungible assets i noticed that the order in which it handles Local & Fungible assets matter. I was not able to finish my implementation but i have an idea on how to do it


### Reserves
This is configured to use NativeAsset to the correspoding chain. But in the case of Fungibility it is expected to mint the same Asset on receiving chain
```rust
pub type Reserves = NativeAsset;
```

I would have liked to:
- Test out my Barriers more and multiple configurations on the relaychain and parachain and seeing its impact
- Building the pallet piece
- Implement Fungible Assets# xcm-config

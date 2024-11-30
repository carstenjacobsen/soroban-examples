# Events

Events are the mechanism that applications off-chain can use to monitor changes and events in contracts on-chain. This events example demonstrates how to publish events from a contract. This example is an extension of the [storing data example](https://developers.stellar.org/docs/build/smart-contracts/getting-started/storing-data). 

See the [documentation](https://developers.stellar.org/docs/learn/encyclopedia/contract-development/events) for more information about events

## How it Works
This example contract extends the increment example by publishing an event each time the counter is incremented. Contract events let contracts emit information about what their contract is doing. Contracts can publish events using the environments events publish function.

```rust
env.events().publish(topics, data);
```

### Event Topics
Topics are conveniently defined using a tuple. In the sample code two topics of `Symbol` type are used.

```rust
env.events().publish((COUNTER, symbol_short!("increment")), ...);
```

> [!TIP]
> The topics don't have to be made of the same type.

### Event Data

An event also contains a data object of any value or type including types defined by contracts using `#[contracttype]`. In the example the data is the `u32` count.

```rust
env.events().publish(..., count);
```

### Publishing

Publishing an event is done by calling the `publish` function and giving it the topics and data. The function returns nothing on success, and panics on failure. Possible failure reasons can include malformed inputs (e.g. topic count exceeds limit) and running over the resource budget (TBD). Once successfully published, the new event will be available to applications consuming the events.

```rust
env.events().publish((COUNTER, symbol_short!("increment")), count);
```

> [!CAUTION]
> Published events are discarded if a contract invocation fails due to a panic, budget exhaustion, or when the contract returns an error.

## Build the Contract

To build the contract, use the `stellar contract build` command.

```sh
stellar contract build
```

A `.wasm` file should be outputted in the `target` directory:

```
target/wasm32-unknown-unknown/release/soroban_events_contract.wasm
```

## Run the Contract

If you have [`stellar-cli`] installed, you can invoke contract functions in the using it.

```sh
stellar contract invoke \
    --wasm target/wasm32-unknown-unknown/release/soroban_events_contract.wasm \
    --id 1 \
    -- \
    increment
```

The following output should occur using the code above.

```json
#0: "event": {"ext":"v0","contractId":[0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],"type":"contract","body":{"v0":{"topics":[{"symbol":[67,79,85,78,84,69,82]},{"symbol":[105,110,99,114,101,109,101,110,116]}],"data":{"u32":1}}}}
```

A single event `#0` is outputted, which is the contract event the contract published. The event contains the two topics, each a `symbol` (displayed as bytes), and the data object containing the `u32`.

[`stellar-cli`]: ../getting-started/setup.mdx#install-the-stellar-cli

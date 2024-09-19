
![](./picture/arbitrage-bot.png)



## What is Opensea-Arbitrage-Bot？


At its core, Opensea-Arbitrage-Bot is architected as an event processing pipeline. The library is made up of three main components: 

1. *Collectors*: *Collectors* take in external events (such as pending txs, new blocks, marketplace orders, etc. ) and turn them into an internal *event* representation. 
2. *Strategies*: *Strategies* contain the core logic required for each MEV opportunity. They take in *events* as inputs, and compute whether any opportunities are available (for example, a strategy might listen to a stream of marketplace orders to see if there are any cross-exchange arbs). *Strategies* produce *actions*.
3. *Executors*: *Executors* process *actions*, and are responsible for executing them in different domains (for example, submitting txs, posting off-chain orders, etc.).

## Strategies 

The following strategies have been implemented and fixed:

- [Opensea/Sudoswap NFT Arbitrage](/crates/strategies/opensea-sudo-arb/): A strategy implementing atomic, cross-market NFT arbitrage between Seaport and Sudoswap.

## Build, Test and Run

First, make sure the following are installed: 
1. [Anvil](https://github.com/foundry-rs/foundry/tree/master/crates/anvil#installing-from-source)

In order to build, first clone the github repo: 

```sh
git clone https://github.com/WendellRyan/Opensea-Arbitrage-Bot
cd Opensea-Arbitrage-Bot
```

Next, run tests with cargo(Ensure that Rust is installed): 

```sh
cargo test --all
```

In order to run the opensea sudoswap arbitrage strategy, you can run the following command: 

```sh
cargo run --bin artemis -- --wss <INFURA_OR_ALCHEMY_KEY> --opensea-api-key <OPENSEA_API_KEY> --private-key <PRIVATE_KEY> --arb-contract-address <ARB_CONTRACT_ADDRESS> --bid-percentage <BID_PERCENTAGE>
```

> [!IMPORTANT]
> 
> where `ARB_CONTRACT_ADDRESS` is the address to which you deploy the [arb contract](/crates/strategies/opensea-sudo-arb/contracts/src/SudoOpenseaArb.sol)
> 
> Before deploying the contract, you can fill this in as `"invalid_address"` to test for any errors. However, make sure the other four parameters are filled in correctly, and the bid-percentage can be set to `"0"`. Before making any adjustments, I recommend running the existing strategy first to familiarize yourself with how it works.


## Improvements and ideas

The current version has been deeply optimized, now capable of capturing arbitrage opportunities faster and more accurately to generate profits. In the future, I plan to build more strategies on this framework, such as arbitrage between decentralized exchanges.


## Contact

Working normally in September 2024

If you have any ideas, please contact me:

Discord: `@wendellryan`

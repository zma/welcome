---
title: "Read Modes"
excerpt: ""
---
EOSIO provides [a set of services and interfaces](https://developers.eos.io/eosio-cpp/docs/db-api) that enable contract developers to persist state across action, and consequently transaction, boundaries. Contracts may use these services and interfaces for different purposes. For example, `eosio.token` contract keeps balances for all users in the database.

Each instance of `nodeos` keeps the database in memory, so contracts can read and write data.   `nodeos` also provides access to this data over HTTP RPC API for reading the database.

However, at any given time there can be multiple correct ways to query that data: 
- `speculative` : (default) this includes the side effects of confirmed and unconfirmed transactions.
- `head` : this only includes the side effects of confirmed transactions, this mode processes unconfirmed transactions but does not include them.
- `read-only`: this only includes the side effects of confirmed transactions.

A transaction is considered confirmed when a nodeos instance has received, processed, and written it to a block on the blockchain, i.e. it is in the head block or an earlier block.
 
# Read Modes

The mode is specified using the `--read-mode` argument for the `eosio::chain_plugin`.

## Speculative

Clients such as `cleos` and the RPC API, will see database state as of the current head block plus changes made by all transactions known to this node but potentially not included in the chain, unconfirmed transactions for example. 

Speculative mode is low latency but fragile, there is no guarantee that the transactions reflected in the state will be included in the chain OR that they will reflected in the same order the state implies.  

This mode features the lowest latency, but is the least consistent. 

In speculative mode `nodeos` is able to execute transactions which have TaPoS (Transaction as Proof of Stake) pointing to any valid block in a fork considered to be the best fork by this node.

## Head

Clients such as `cleos` and the RPC API will see database state as of the current head block of the chain.  Since current head block is not yet irreversible and short-lived forks are possible, state read in this mode may become inaccurate  if `nodeos` switches to a better fork.  Note that this is also true of speculative mode.  

This mode represents a good trade-off between highly consistent views of the data and latency.

In this mode `nodeos` is able to execute transactions which have TaPoS pointing to any valid block in a fork considered to be the best fork by this node.

# Read-Only

Clients such as `cleos` and the RPC API will see database state as of the current head block of the chain. It **will not** include changes made by transactions known to this node but not included in the chain, such as unconfirmed transactions.
[block:callout]
{
  "type": "info",
  "body": "The EOSIO platform stores blockchain information in various data structures at various stages of a transaction's life-cycle. Some of these are described below. In these descriptions the producing node is the nodeos instance run by the block producer who is currently creating blocks for the blockchain (which changes every 6 seconds.)\n \n  * The `block log` is an append only log of blocks written to disk and contains all the irreversible blocks.\n  * `Reversible_blocks` is a memory mapped file and contains blocks that have been written to the blockchain but have not yet become irreversible.\n  * The `chain state` or `database` is a memory mapped file, storing the blockchain state of each block (account details, deferred transactions, transactions, data stored using multi index tables in smart contracts, etc.).  Once a block becomes irreversible we no longer cache the chain state.\n  * The `pending block` is an in memory block containing transactions as they are processed into a block, this will/may eventually become the head block. If this instance of nodeos is the producing node then the pending block is distributed to other nodeos instances.\n  * The head block is the last block written to the blockchain, stored in `reversible_blocks`.",
  "title": "Brief overview of blockchain state and storage"
}
[/block]
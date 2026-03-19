
# Rust RPC client for Doriancoin Core JSON-RPC

This is a Rust RPC client library for calling the Doriancoin Core JSON-RPC API. It provides a layer of abstraction over
[rust-jsonrpc](https://github.com/apoelstra/rust-jsonrpc) and makes it easier to talk to the Doriancoin JSON-RPC interface.

This git package compiles into two crates.
1. **bitcoincore-rpc** - contains an implementation of an rpc client that exposes
the Doriancoin Core JSON-RPC APIs as rust functions.

2. **bitcoincore-rpc-json** - contains rust data structures that represent
the json responses from the Doriancoin Core JSON-RPC APIs. bitcoincore-rpc depends on this.

# Usage
Given below is an example of how to connect to the Doriancoin Core JSON-RPC for a node running on `localhost`
and print out the hash of the latest block.

It assumes that the node has password authentication setup, the RPC interface is enabled at port `1948` and the node
is set up to accept RPC connections.

```rust
extern crate bitcoincore_rpc;

use bitcoincore_rpc::{Auth, Client, RpcApi};

fn main() {

    let rpc = Client::new("http://localhost:1948",
                          Auth::UserPass("<FILL RPC USERNAME>".to_string(),
                                         "<FILL RPC PASSWORD>".to_string())).unwrap();
    let best_block_hash = rpc.get_best_block_hash().unwrap();
    println!("best block hash: {}", best_block_hash);
}
```

See `client/examples/` for more usage examples. 

# Doriancoin

This is a fork adapted for Doriancoin (bech32 HRP `dsv`, default RPC port `1948`).

# Minimum Supported Rust Version (MSRV)
This library should always compile with any combination of features on **Rust 1.41.1**.

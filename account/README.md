# Account
Accounts are the central data structure in Stellar- they hold balances, sign transactions, and issue assets. Accounts can only exist with a valid keypair and the required minimum balance of XLM. 

This example is a basic multi-sig account contract with a customizable per-token authorization policy. This example contract demonstrates how to build the account contract, and how to implement custom authorization policies that can govern all the account contract interactions.

Custom accounts are exclusive to Soroban and can't be used to perform other Stellar operations.

## Quick Links
- [Open example in GitPod](https://gitpod.io/#https://github.com/stellar/soroban-examples/tree/v21.6.0)
- [Accounts documentation](https://developers.stellar.org/docs/learn/fundamentals/stellar-data-structures/accounts)
- [Detailed description of this example](https://developers.stellar.org/docs/build/smart-contracts/example-contracts/custom-account)


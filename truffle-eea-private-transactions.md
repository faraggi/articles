# Open call for contributions: truffle + EEA private transactions

[](Private EEA transactions with EEA and Pantheon)

Private transactions on truffle aren't working.
shim detects private_for from truffle
and translating that into the EEA_sendTransaction() endpoint
and intereacting with the web3eeajs client lib to make that happen


Possibly using a Delegation pattern to help make that work- when it detects those patterns there, its given off to the EEA lib, else its dropeed through and original methods are called in the standards web3 way.




Truffle

At Pegasys, we don't take client Specs lightly. In fact, we contribute heavily to make sure future specs are well defined and line p correctly with our software. There are a few people at pegasys who spend a lot of their time and activiely work on spec definition.

As part of the upcoming EEA 4.0 client spec, private transactions have slightly changed the way the get implemented. Therefore, we now find that the `truffle-interface-adapter` that implemented the old spec isn't up to date.




I'll be writing the call for proposals article for the truffle blog today, this is the current WIP version:

**Open call for contributions: truffle + EEA private transactions**

## What's missing?
- Truffle doesn't support Pantheon private transactions


## Why did this happen?
- As part of the upcoming EEA 4.0 client spec, private transactions have slightly changed the way the get implemented. Therefore, we now find that the `truffle-interface-adapter` that implemented the old spec isn't up to date.

## What's the solution?
Pegasys and Truffle have teamed up to make a single open call for contributions. This gest blog post is made by the Pegasys team and is to be posted on the Truffle blog
- add code to Truffle to support eea private transactions


- Possibly using a Delegation pattern to help make that work

The location of the files can be found here:
[truffle/packages/truffle-interface-adapter/lib](https://github.com/trufflesuite/truffle/tree/develop/packages/truffle-interface-adapter/lib)

## What to do Exactly?

Here are some high level instructions on

In short, when truffle receives a transaction, it should determine if its a `privateFor` transaction. If so, it would delegate the rest of the busines logic to the EEA library. If not, it should just continue processing the transaction with the original web3 methods.

More detail?
The `web3-shim.ts` file currently contains the overloads for the different interface definitions and their mappings.

```
import { EthereumDefinition } from "./ethereum-overloads";
import { QuorumDefinition } from "./quorum-overloads";
import { FabricEvmDefinition } from "./fabric-evm-overloads";

const initInterface = async(web3Shim: Web3Shim) => {

    const networkTypes: NetworkTypesConfig = new Map(Object.entries({
      "ethereum": EthereumDefinition,
      "quorum": QuorumDefinition,
      "fabric-evm": FabricEvmDefinition
    }));

    networkTypes.get(web3Shim.networkType).initNetworkType(web3Shim);
  }
```




- shim detects 'private_for' transaction from truffle
- translates that into the EEA_sendTransaction() endpoint
- interacts with the web3eeajs client lib to make that happen

## Who can do this?

Anyone who'd like to try can very much do so we will gladly support any developer who wants to help out.
But here are some recommended knowledge areas to have:

The truffle codebase is mainly written in `javascript`, and this particular interface-adapter library we'll be looking at is written in `typescript`.
So knowing some javascript is a must.

It will definitely help if you've had some exposure and usage of the truffle library. Nothing fancy, just using it for compiling and deploying contracts for example.

Likewise, having some previous knowledge of the web3js library is going to prove quite helpful.

All of the above somewhat discribes a general dapp developer- so in other words; if you've already written a dapp before using truffle, this contribution could be done by you.

So what's in it for you?
Two things:
- You'll receive some Pegasys Swag.
- I'll personally thank and credit you on stage at [Trufflecon at my Permissioning Talk](https://twitter.com/trufflesuite/status/1150929297647034374)


eea_getTransactionReceipt

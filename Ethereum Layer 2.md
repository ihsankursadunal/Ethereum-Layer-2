<style>
green{
    color: #50d62f;
}
alt-top{
    color: #fc1685;
}
paragraph{
    margin-left:40px;
}
bl{
    color: #19b9ea;
}
bl-alt{
    color: #158fb5;
}
red{
    color:red;
}
</style>
# <center>Ethereum Layer 2<center>

<details>
<summary><alt-top><b>Abstract</b></alt-top></summary>
<paragraph>Layer 2 is a collective term for solutions designed to help scale your application by handling transactions off the main Ethereum chain (Layer 1). Transaction speed suffers when the network is busy which can make the user experience poor for certain types of dapps. And as the network gets busier, gas prices increase as transaction senders aim to outbid each other. This can make using Ethereum very expensive.</paragraph><br />
<paragraph>Generally speaking, transactions are submitted to these Layer 2 nodes instead of being submitted directly to Layer 1 (mainnet); the Layer 2 instance then batches them into groups before anchoring them to Layer 1, after which they are secured by Layer 1 and cannot be altered. The details of how this is done vary significantly between different Layer 2 technologies and implementations.A specific Layer 2 instance may be open and shared by many applications, or may be deployed by one company and dedicated to supporting only their application.</paragraph>
<details>
<summary><green>Types of Layer 2 Solutions</green></summary>

- <bl>Rollups</bl>
  - <bl-alt>ZK Rollups</bl-alt>
  - <bl-alt>Optimistic Rollups</bl-alt>
- <bl>State Channels</bl>
- <bl>Plasma</bl>
- <bl>Validium</bl>
- <bl>Sidechains</bl>
- <bl>Hybrid Solutions</bl>
</details>

## <alt-top>WHY ?</alt-top>
<paragraph>**Increasing transaction speed**, **decreasing transaction consts**, **keeping Layer 1 advantages**, this is why Layer 2 builds on top of Ethereum mainnet.</paragraph>
</details>

<details>
<summary><green><b>Rollups</b></green></summary>

<paragraph>Rollups are solutions that perform transaction _execution_ outside Layer 1, but post transaction data on Layer 1. As transaction data is on Layer 1, this allows rollups to be _secured by Layer 1_. **Inheriting the security properties of the main Ethereum chain, while performing execution outside of Layer 1, is a defining characteristic of rollups.**</paragraph><br />
<details>
<summary><green>Three simplified properties of rollups are:</green></summary>

1. <bl>Transaction execution outside Layer 1.</bl>
2. <bl>Data or proof of transactions is on Layer 1.</bl>
3. <bl>A rollup smart contract in Layer 1 that can enforce correct transaction execution by using the transaction data on Layer 1.</bl>
</details><br />
Rollups require operators to stake a bond in the rollup contract. This incentivises operators to verify and execute transactions correctly.<br /><br />

<details style="margin-left:20px;">
<summary><green>Advantages</green></summary>

- <bl>Reducing fees for users</bl>
- <bl>Open participation</bl>
- <bl>Fast transaction throughput</bl>
</details><br />

<green>There are two types of rollups with different security models:</green>
- Zero knowledge: runs computation off-chain and submits a validity proof to the chain.
  - <red>Validity Proof</red>
    - A security model for certain Layer 2 solutions where, to increase speed, transactions are rolled up into batches and submitted to Ethereum in a single transaction. The transaction computation is done off-chain and then supplied to the main chain with a proof of their validity. This method increases the amount of transactions possible while maintaining security.
- Optimistic: assumes transactions are valid by default and only runs computation, via a fraud proof, in the event of a challenge.
  - <red>Fraud Proof</red>
    - A security model for certain Layer 2 solutions where, to increase speed, transactions are rolled up into batches and submitted to Ethereum in a single transaction. They are assumed valid but can be challenged if fraud is suspected. A fraud proof will then run the transaction to see if fraud took place. This method increases the amount of transactions possible while maintaining security. 

<details><summary><bl-alt>Rollup History</bl-alt></summary>

<paragraph>The concept of Rollups dates back to 2014, described as “shadow chains” by Ethereum co-founder Vitalik Buterin. The failures of solutions like Plasma and state channels led developers to revisit Buterin’s shadow chains, now known as Rollups. While Plasma and state channels can scale millions of transactions per second, they are not compatible with the smart contracts that power many of the DeFi applications which have surged in popularity.</paragraph>

<img src="https://cdn.publish0x.com/prod/fs/images/eba3572b216bceed16bca31b60504dc74043211105b028cd7be5ab8026657e89.png" width="360" height="360" /><br />

<paragraph>Rollups build on the shadow chains idea by taking execution of the state off-chain and only using the Ethereum blockchain for data availability. Rollups post blocks or state updates, only publishing some data to the main chain for each transaction via tx CALLDATA, providing an improvement in throughput and overcoming a major hurdle for sidechains: data withholding attacks.</paragraph><br />
<paragraph>Another benefit is that each Rollup chain can be thought of as a shard where each shard (or Rollup chain) can permit experimentation with different execution and data models with no hard forks. As shown by Figure 4, each Rollup chain may have a different execution model, but will use the Ethereum main chain for data validation.</paragraph><br />

<img src="https://cdn.publish0x.com/prod/fs/cachedimages/3157800664-c044ef47caeda0da9de41ee7ccc0a70e3836c880b8c5cd9621c4e2b56a1d774b.webp" width="360" height="360" />
</details><br />

<details>
<summary><green>Zero Knowledge Rollups</green></summary>

<paragraph>Zero knowledge rollups, also known as ZK rollups, bundle or "roll up" hundreds of transfers off-chain and generates a cryptographic proof, known as a SNARK (succinct non-interactive argument of knowledge). This is known as a validity proof and is posted on Layer 1.</paragraph><br />

<paragraph>The ZK rollup contract maintains the state of all transfers on Layer 2, and this state can only be updated with a validity proof. This means that ZK rollups only need the validity proof, instead of all transaction data. With a ZK rollup, validating a block is quicker and cheaper because less data is included. Instead of waiting two weeks for a block in the Shadow Chain to become finalised. ZK-Rollups replace fraud challenges with zero-knowledge proofs. Accounts and balances are represented by separate Merkle Trees. These Merkle Tree roots ensure no one can fake the data. The roots of each Merkle Tree (one for accounts, the other for balances) are both stored in a smart contract on Ethereum which provides a succinct representation of the state of the sidechain. All other data is stored off-chain.</paragraph><br />

<img src="https://cdn.publish0x.com/prod/fs/images/d8b5ae35eea5514831a7ce5d46b1c0d5003e4122ce3a9e3f4df2067c9cea39fc.png" width="480" height="360"/>


<paragraph>With a ZK rollup, there are no delays when moving funds from Layer 2 to Layer 1 because a validity proof accepted by the ZK rollup contract has already verified the funds.</paragraph><br />

<paragraph>The sidechain where ZK rollups happen can be optimised to reduce transaction size further. For instance, an account is represented by an index rather than an address, which reduces a transaction from 32 bytes to just 4 bytes. Transactions are also written to Ethereum as calldata, reducing gas.</paragraph>

>What is a zero-knowledge proof :  A zero-knowledge proof simply demonstrates that you know some secret to someone else without revealing the secret itself. Through virtue of mathematics, the verifier can check that the prover knows the secret without it actually being revealed to them.

<details style="margin-left:20px;">
<summary><green>Pros and Cons</green></summary>

|Pros |Cons |
--- | --- 
|No delay as proofs are already considered valid when submitted to the main chain|Limited to simple transfers, not compatible with the EVM.|
|Less vulnerable to the economic attacks that Optimistic rollups can be vulnerable to.|Validity proofs are intense to compute – not worth it for applications with little on-chain activity.|
||Slower subjective finality time (10-30 min to generate a ZK proof) (but faster to full finality because there is no dispute time delay like in Optimistic rollups).|

<green>Finality</green>
: Finality is the guarantee that a set of transactions before a given time will not change and can't be reverted.
</details><br />

<green>Use ZK Rollups</green>
- [Loopring](https://loopring.org/#/)
- [Strakware](https://starkware.co/)
- [Matter Labs zkSync](https://matter-labs.io/)
- [Aztec 2.0](https://aztec.network/)
</details><br />

<details>
<summary><green>Optimistic Rollups</green></summary>

<paragraph>Optimistic rollups use a side chain that sits in parallel to the main Ethereum chain. They can offer improvements in scalability because they don't do any computation by default. Instead, after a transaction they propose the new state to mainnet. Or "notarise" the transaction.</paragraph><br />

<paragraph>With Optimistic rollups transactions are written to the main Ethereum chain as calldata, optimising them further by reducing the gas cost.</paragraph><br />

<paragraph>As computation is the slow, expensive part of using Ethereum, Optimistic rollups can offer up to 10-100x improvements in scalability dependent on the transaction. This number will increase even more with the introduction of the Eth2 upgrade: shard chains. This is because there will be more data available in the event that a transaction is disputed.</paragraph>

<img src="https://cdn.publish0x.com/prod/fs/images/d8b5ae35eea5514831a7ce5d46b1c0d5003e4122ce3a9e3f4df2067c9cea39fc.png" width="480" height="360"/>

<green>Disputing Transactions</green><br />
<paragraph>Optimistic rollups don't actually compute the transaction, so there needs to be a mechanism in place to ensure transactions are legitimate and not fraudulent. This is where fraud proofs come in. If someone notices a fraudulent transaction, the rollup will execute a fraud-proof and run the transaction's computation, using the available state data. This means you may have longer wait times for transaction confirmation than a ZK-rollup, because it could be challenged.</paragraph><br />
<img src="https://ethereum.org/static/254748fd33c43766a4f6a90c9a92fd19/c1b63/optimistic-rollups.png" /><br />
<paragraph>The gas you need to run the computation of the fraud proof is even reimbursed. Ben Jones from Optimism describes the bonding system in place: "Anyone who might be able to take an action that you would have to prove fraudulent to secure your funds requires that you post a bond. You basically take some ETH and lock it up and you say "Hey, I promise to tell the truth"... If I don't tell the truth and fraud is proven, this money will be slashed. Not only does some of this money get slashed but some of it will pay for the gas that people spent doing the fraud proof". So you get reimbursed for proving fraud.</paragraph><br />

<details style="margin-left:20px;">
<summary><green>Pros and Cons</green></summary>

|Pros |Cons |
--- | --- 
|Anything you can do on Ethereum Layer 1, you can do with Optimistic rollups as it's EVM and Solidity compatible.|Long wait times for on-chain transaction due to potential fraud challenges.|
|All transaction data is stored on the Layer 1 chain, meaning it's secure and decentralized.||
</details><br />


<green>Use Optimistic Rollups</green>
- [Optimism](https://optimism.io/)
- [Offchain Labs Arbitrum Rollup](https://offchainlabs.com/)
- [Fyal Network](https://fuel.sh/)
- [Cartesi](https://cartesi.io/)
</details><br />
</details>

<details>
<summary><green><b>Channels</b></green></summary>
<paragraph>Channels allow participants to transact x number of times off-chain while only submitting two transaction to the network on chain. This allows for extremely high transaction throughput</paragraph><br />

<details style="margin-left:20px;">
<summary><green>Advantages</green></summary>

- <bl>Lots of state updates</bl>
- <bl>When number of participants is known upfront</bl>
- <bl>When participants are always available</bl>
</details><br />

<paragraph>Participants must lock a portion of Ethereum's state, like an ETH deposit, into a multisig contract. A multisig contract is a type of contract that requires the signatures (and thus agreement) of multiple private keys to execute.</paragraph><br />

<paragraph>Locking the state in this way is the first transaction and opens up the channel. The participants can then transact quickly and freely off-chain. When the interaction is finished, a final on-chain transaction is submitted, unlocking the state</paragraph>

<details>
<summary><bl>Types Of Channels</bl></summary>

- <bl-alt>Payment Channels</bl-alt>
  - <p style="color:#167693">Simplified state channels that only deal with payments. They allow off-chain transfers between two participants, as long as the net sum of their transfers does not exceed the deposited tokens.</p>
- <bl-alt>State Channels</bl-alt> <red>&darr;</red>
</details><br />

<details style="margin-left:20px">
<summary><green>State Channels</green></summary>

<paragraph>State channels are very similar to the concept of payment channels in Bitcoin’s Lightning Network, but instead of only supporting payments, they also support general ‘state updates.’</paragraph><br />

<paragraph>Scaling is arguably the biggest obstacle that blockchains face when it comes to achieving mainstream adoption. While some applications can thrive today, most are still too slow and expensive for regular users.</paragraph><br />

<paragraph>State channels increase the throughput of public blockchains because they decrease the computational load that nodes have to expend when processing and storing transactions. This will make it easier to run a node, which makes the job of validating the miners’ work more decentralized. Similarly, State Channels reduce the costs required to use the Ethereum network. Instead of paying fees for each transaction, users only have to pay for gas when they open and close a channel.</paragraph><br />

<paragraph>State channels also help preserve user privacy. Transactions within a channel are only known by the participants in the channel. This is in contrast to transacting on the Ethereum blockchain where every transaction is recorded in a publicly auditable ledger.</paragraph><br />

<paragraph>Lastly, transactions within state channels get instant finality. Users don’t have to wait for each transaction to confirm onto the blockchain because each signed transaction abides by the network rules. This makes the user experience seamless and more mirrors how popular online applications operate today. </paragraph><br />

<paragraph>While at first glance it might seem like transactions within state channels aren’t backed up by the same level of security as on-chain transactions, the magic is that we can achieve the same level of security without using as much of the network’s resources. By being able to always revert back to the main chain as an arbitration mechanism, users are game-theoretically incentivized to act rationally. Also, each transaction is signed the same way a valid Ethereum transaction would be.</paragraph><br />

<paragraph>On-chain transactions aren’t completely eliminated but rather reduced to only the necessary sequences. Users have to create and pay for an Ethereum transaction when they first open up the channel. When they’re ready to close the channel, they again have to pay fees to process a transaction on the Ethereum blockchain. Cutting the number of necessary on-chain transactions down to two drastically reduces the costs and increase the speed associated with using Ethereum.</paragraph><br />

<details style="margin-left:20px;">
<summary><green>Pros and Cons</green></summary>

|Pros |Cons |
--- | --- 
|Instant withdrawal/settling on mainnet (if both parties to a channel cooperate)|Time and cost to set up and settle a channel - not so good for occasional one-off transactions between arbitrary users.|
|Extremely high throughput is possible|Need to periodically watch the network (liveness requirement) or delegate this responsibility to someone else to ensure the security of your funds.|
|Lowest cost per transaction - good for streaming micropayments|Have to lockup funds in open payment channels|
||Don't support open participation|

</details><br />

<green>Use State Channels</green>
- [Connext](https://connext.network/)
- [Kchannels](https://www.kchannels.io/)
- [Perun](https://perun.network/)
- [Raiden](https://raiden.network/)
- [Statechannels](https://statechannels.org/)

</details>
</details>

<details>
<summary><green><b>Plasma</b></green></summary>
<paragraph>A plasma chain is a separate blockchain that is anchored to the main Ethereum chain, and uses fraud proofs (like Optimistic rollups) to arbitrate disputes.</paragraph><br />

<paragraph>The Plasma structure is built through the use of smart contracts and Merkle trees, enabling the creation of an unlimited number of child chains - which are, essentially, smaller copies of the parent Ethereum blockchain. Each chain is designed to work in a singular way, serving different needs by coexisting and operating independently. On top of each child chain, more chains can be created and this is what builds a tree-like structure.</paragraph><br />

<paragraph>Deposits and withdrawals of Plasma chain funds with state transitions is enabled by fraud proofs. This ensures enforceable state and exchangeability. It also allows the processing of a greater number of transactions with less data loading on the basic platform. Any user can send funds to another, including those from a different set of participants. These fund transfers can be paid and withdrawn in the native platform coin.</paragraph><br />

<details>
<summary><green>Plasma: Pros and Cons</green></summary>

<paragraph>Each new plasma iteration reveals a new research problem that needs to be addressed, leading to multiple Plasma variants that navigate deployment trade-offs in different ways. </paragraph>

|Pros|Cons|
--- | ---
|Plasma will help the Ethereum blockchain scale by taking operations off-chain|Plasma requires a centralized component in order to operate as the off-chain component is managed by authorities|
|Lower fees and faster operations also enables computationally intensive applications to run on a blockchain|Long waiting periods(7-14 days) for users who wish to withdraw their funds|
|Eliminating significant amount of unnecessary data in the main chain which also reduces the processing bandwidth of nodes|Poor experience for users who don’t have a large number of assets and don’t want to wait weeks to access them|
|It is compatible with various on-chain scaling solutions such as sharding, varying block sizes, etc.|New security risks/challenges (primarly for exits) that would need to be addressed to maintain immutability.|
|Good for transactions between arbitrary users (no overhead per user pair if both are established on the plasma chain)|Does not support general computation. Only basic token transfers, swaps, and a few other transaction types are supported via predicate logic.|
||Need to periodically watch the network (liveness requirement) or delegate this responsibility to someone else to ensure the security of your funds.|
||	Relies on one or more operators to store data and serve it upon request.|

</details><br />



<details>
<summary><green>Plasma Examples</green></summary>

<paragraph>Many plasma variants have their own set of drawbacks such as: Plasma MVP has time constraints, is a less than ideal user experience, and is vulnerable to network congestion. Plasma Cash relies on non-fungible tokens (NFTs) to function which requires heavy transaction histories. You will have to keep track of the value and have to be constantly collecting proofs of non-inclusion, and so when you transfer ownership of the NFT you have to transfer its history as well.</paragraph><br />

<paragraph>There isn’t any single project called "Plasma". Instead, there are lots of different projects that use the tools provided by the Plasma framework/specification.</paragraph><br />

<bl>Today there are four main distinct versions of the Plasma protocol:</bl>
- <details><summary><bl-alt>Plasma Cash</bl-alt></summary>
    <paragraph>Plasma Cash is a Plasma design primarily built for storing and transferring non-fungible tokens. It is highly scalable because users only ever need to keep track of their own tokens.</paragraph>
  </details>
- <details><summary><bl-alt>Plasma Debit</bl-alt></summary>
    <paragraph>It uses Sparse Merkle Trees (SMT) for non inclusion proofs and hence can only be used for NFTs since SMTs uses indexing. Each block has a ‘slot’ for each coin (unique deposit). When a coin is spent, a transaction proof is recorded in that coin’s respective slot in the block.
    Note: Coin defragmentation research to support FTs is going on currently</paragraph>
  </details>
- <details><summary><bl-alt>Plasma Prime</bl-alt></summary>
    <paragraph>Plasma Prime is a fancy new design that makes use of RSA accumulators to solve the problem of large history proofs in Plasma Cash.</paragraph>
  </details>
- <details><summary><bl-alt>MVP (Minimum Viable Plasma)</bl-alt></summary>
    <paragraph>Plasma MVP is a design for an extremely simple UTXO-based Plasma chain. The basic Plasma MVP specification enables high-throughput payment transactions, but does not support more complicated constructions like scripts or smart contracts.</paragraph>
  </details>

<paragraph>Plasma MVP relies on confirmation signatures because withdrawals are processed in order based on the position of the output being withdrawn.</paragraph><br />

<paragraph>Users need to sign a signature before making a transaction, wait to see the transaction included in a valid block, and then sign another signature. These second signatures must also be included within a plasma block, reducing block space available for more transactions!</paragraph><br />

<paragraph>Note: Confirmation signatures make for pretty bad user experience. More Viable Plasma, also known as MoreVP, is an extension to Minimal Viable Plasma that removes the need for confirmation signatures. MoreVP modifies the process through which users can withdraw their funds. The ordering of each withdrawal becomes based on the position of the youngest input to the transaction that created an output.</paragraph><br />

|Plasma Design Component|Plasma MVP|Plasma Cash|Plasma Debit|
--- | --- | --- | ---
|Data Structure|Binary Merkle tree|Sparse Merkle Tree|Sparse Merkle tree|
|Consensus|Any (PoW,PoA,PoS)|Any (PoW,PoA,PoS)|Single or few operators preferred over because of payment channel structure|
|Deposits|UTXOs representation, support for ETH, ERC20|Unique Coin ID for each deposit, NFTs only|Accounts with unique coin IDs for each deposit, NFTs and FTs only|
|Fees|Plasma transaction fees to validators and gas fees when exiting/withdrawing to rootchain or other chains|Same as MVP|Users pay via operator-led payment channel instead of directly to other users|
|Signatures|Tx signature before block inclusion, confirmation signature post-inclusion|Confirmation signatures to avoid griefing|No confirmation signatures|
|Exits/Withdrawals|Proof of unspent UTXO required to exit, priority based on how old UTXO is|Proof of coin’s latest two transactions, proof of block inclusion, no priority|Proof of coin’s latest two transactions, proof that fraction of coin hasn’t been previously spent, proof of block inclusion, no exit priority|

<green>Comparison</green>

|Type|Plasma MVP|Plasma Cash|Plasma Debit|
--- | --- | --- | ---
|Pros|Scalable, all signatures sent to operator in PoA, High fungibility|Very scalable, watchers or users themselves need to only keep track of their own coins not all coins on the chain|Very scalable, watchers or users themselves need to only keep track of their own coins, Enables transactions with NFTs and FTs, Efficient balance updates don’t need to be included in blocks as agreement can be made between operator and coinholder (similar to channels)|
|Cons|Watchers or users themselves are required to watch and challenge invalid exits, Potential for honest bond slashing if operator withholds blocks and user attempts to re-submit transaction|Coin proofs can be massive, Coins are in fixed denomination, Watchers or users themselves are required to watch and challenge invalid txs with their own coins|Heavy reliance on operator, can be hedged by creating a set of rotating operators, Coin proofs can be massive, Requires operator to lock up significant funds in advance to fund payment channels, Tx size constrained by initial coin deposit size, Enabling decentralized exchange on Debit is non-trivial|
|Use Cases|Low-trust use cases (PoA), Exchanges, securities, P2P payments, recurring/bill payments, gaming|Collectibles, Asset management (real estate, art)|Use cases with high-trust of operators, ewallet or service providers, Gaming, Asset Management, P2P payments|

</details><br />

<green>Use Plasma</green>
- [OMG Network](https://omg.network/)
- [Polygon (new name of Matic Network)](https://polygon.technology/)
- [Matic Network](https://matic.network/)
- [Gluon](https://gluon.network/)
- [Gazelle](https://gzle.io/)
- [LeapDAO](https://ipfs.leapdao.org/)
</details>

<details>
<summary><green><b>Validium</b></green></summary>

<paragraph>Uses validity proofs like ZK-rollups but data is not stored on the main layer 1 Ethereum chain. This can lead to 10k transactions per second per validium chain and multiple chains can be run in parallel.</paragraph><br />

<details><summary><green>Pros and Cons</green></summary>

|Pros|Cons|
--- | ---
|No withdrawal delay (no latency to on-chain/cross-chain tx); consequent greater capital efficiency.|Limited support for general computation/smart contracts; specialized languages required.|
|Not vulnerable to certain economic attacks faced by fraud-proof based systems in high-value applications.|High computational power required to generate ZK proofs; not cost effective for low throughput applications.|
||Slower subjective finality time (10-30 min to generate a ZK proof) (but faster to full finality because there is no dispute time delay).|
</details><br />

<green>Use Validium</green>
- [Starkware](https://starkware.co/)
- [Matter Labs zkPorter](https://matter-labs.io/)
- [Loopring](https://loopring.org/#/)
</details>

<details><summary><green><b>Further reading</b></green></summary>

- [Ethereum Layer 2 Scaling](https://ethereum.org/en/developers/docs/layer-2-scaling/)
- [The Current State of Ethereum L2](https://defiprime.com/ethereum-l2)
- [Plasma vs Optimistic Rollups](https://medium.com/omgpool/plasma-vs-optimistic-rollups-9808c2f64975)
- [zkRollup vs. Validium](https://medium.com/matter-labs/zkrollup-vs-validium-starkex-5614e38bc263)
- [Evaluating Ethereum L2 Scaling Solutions: A Comparison Framework](https://medium.com/matter-labs/evaluating-ethereum-l2-scaling-solutions-a-comparison-framework-b6b2f410f955)
- [Validity Proofs vs. Fraud Proofs](https://medium.com/starkware/validity-proofs-vs-fraud-proofs-4ef8b4d3d87a)
- [Shard chains](https://ethereum.org/en/eth2/shard-chains/)


</details>
# An Introduction to the Ethereum Platform

This introductory information should allow anyone without any background knowledge to understand a high level overview of how blockchain and Ethereum work.

### Format

Add flash card points on a new line without a bullet point.

## Definitions
Some of these will be harder to explain in a concise manner but we'll try anyway.

See the Ethereum Wiki Glossary (https://github.com/ethereum/wiki/wiki/Glossary)

### Cryptography
See also: http://en.wikipedia.org/wiki/Public-key_cryptography

Computational infeasibility: a process is computationally infeasible if it would take an impracticably long time (eg. billions of years) to do it for anyone who might conceivably have an interest in carrying it out. Generally, 280 computational steps is considered the lower bound for computational infeasibility.

Hash: a hash function (or hash algorithm) is a process by which a piece of data of arbitrary size (could be anything; a piece of text, a picture, or even a list of other hashes) is processed into a small piece of data (usually 32 bytes) which looks completely random, and from which no meaningful data can be recovered about the document, but which has the important property that the result of hashing one particular document is always the same. Additionally, it is crucially important that it is computationally infeasible to find two documents that have the same hash. Generally, changing even one letter in a document will completely randomize the hash; for example, the SHA3 hash of "Saturday" is c38bbc8e93c09f6ed3fe39b5135da91ad1a99d397ef16948606cdcbd14929f9d, whereas the SHA3 hash of Caturday is b4013c0eed56d5a0b448b02ec1d10dd18c1b3832068fbbdc65b98fa9b14b6dbf. Hashes are usually used as a way of creating a globally agreed-upon identifier for a particular document that cannot be forged.

Encryption: encryption is a process by which a document (plaintext) is combined with a shorter string of data, called a key (eg. c85ef7d79691fe79573b1a7064c19c1a9819ebdbd1faaab1a8ec92344438aaf4), to produce an output (ciphertext) which can be "decrypted" back into the original plaintext by someone else who has the key, but which is incomprehensible and computationally infeasible to decrypt for anyone who does not have the key.

Public key encryption: a special kind of encryption where there is a process for generating two keys at the same time (typically called a private key and a public key), such that documents encrypted using one key can be decrypted with the other. Generally, as suggested by the name, individuals publish their public keys and keep their private keys to themselves.

Digital signature: a digital signing algorithm is a process by which a user can produce a short string of data called a "signature" of a document using a private key such that anyone with the corresponding public key, the signature and the document can verify that (1) the document was "signed" by the owner of that particular private key, and (2) the document was not changed after it was signed. Note that this differs from traditional signatures where you can scribble extra text onto a document after you sign it and there's no way to tell the difference; in a digital signature any change to the document will render the signature invalid.


### Blockchains
See also: https://bitcoin.org/en/vocabulary

Address: an address is essentially the representation of a public key belonging to a particular user; for example, the address associated with the private key given above is 0xCD2a3d9F938E13CD947Ec05AbC7FE734Df8DD826. Note that in practice, the address is technically the hash of a public key, but for simplicity it's better to ignore this distinction.

Transaction: a transaction is a digitally signed message authorizing some particular action associated with the blockchain. In a currency, the dominant transaction type is sending currency units or tokens to someone else; in other systems actions like registering domain names, making and fulfilling trade offers and entering into contracts are also valid transaction types.

Block: a block is a package of data that contains zero or more transactions, the hash of the previous block ("parent"), and optionally other data. Because each block (except for the initial "genesis block") points to the previous block, the data structure that they form is called a "blockchain".

State: the set of data that a blockchain network strictly needs to keep track of, and that represents data currently relevant to applications on the chain. In a currency, this is simply balances; in more complex applications this could refer to other data structures that the application in question needs to keep track of (eg. who has what domain name, what is the status of a given contract, etc). The post-state of a block is the state after executing all transactions in the ancestors of the block starting from the genesis going up to and including the transactions in that block itself.

History: the past transactions and blocks. Note that the state is a deterministic function of the history.

Account: an account is an object in the state; in a currency system, this is a record of how much money some particular user has; in more complex systems accounts can have different functions.

Proof of work: one important property of a block in Bitcoin, Ethereum and many other crypto-ledgers is that the hash of the block must be smaller than some target value. The reason this is necessary is that in a decentralized system anyone can produce blocks, so in order to prevent the network from being flooded with blocks, and to provide a way of measuring how much consensus there is behind a particular version of the blockchain, it must in some way be hard to produce a block. Because hashes are pseudorandom, finding a block whose hash is less than 0000000100000000000000000000000000000000000000000000000000000000 takes an average of 4.3 billion attempts. In all such systems, the target value self-adjusts so that on average one node in the network finds a block every N minutes (eg. N = 10 for Bitcoin and 1 for Ethereum).

Proof of work nonce: a meaningless value in a block which can be adjusted in order to try to satisfy the proof of work condition.

Mining: mining is the process of repeatedly aggregating transactions, constructing a block and trying different nonces until a nonce is found that satisfies the proof of work condition. If a miner gets lucky and produces a valid block, they are granted a certain number of coins as a reward as well as all of the transaction fees in the block, and all miners start trying to create a new block containing the hash of the newly generated block as their parent.

Stale: a stale is a block that is created when there is already another block with the same parent out there; stales typically get discarded and are wasted effort.

Fork: a situation where two blocks are generated pointing to the same block as their parent, and some portion of miners see one block first and some see the other. This may lead to two blockchains growing at the same time. Generally, it is mathematically near-certain that a fork will resolve itself within four blocks as miners on one chain will eventually get lucky and that chain will grow longer and all miners switch to it; however, forks may last longer if miners disagree on whether or not a particular block is valid.

Double spend: a deliberate fork, where a user with a large amount of mining power sends a transaction to purchase some product, then after receiving the product creates another transaction sending the same coins to themselves. The attacker then creates a block, at the same level as the block containing the original transaction but containing the second transaction instead, and starts mining on the fork. If the attacker has more than 50% of all mining power, the double spend is guaranteed to succeed eventually at any block depth. Below 50%, there is some probability of success, but it is usually only substantial at a depth up to about 2-5; for this reason, most cryptocurrency exchanges, gambling sites and financial services wait until six blocks have been produced ("six confirmations") before accepting a payment.

Light client - a client that downloads only a small part of the blockchain, allowing users of low-power or low-storage hardware like smartphones and laptops to maintain almost the same guarantee of security by sometimes selectively downloading small parts of the state without needing to spend megabytes of bandwidth and gigabytes of storage on full blockchain validation and maintenance.
Ethereum Blockchain
See also: http://ethereum.org/ethereum.html

Serialization: the process of converting a data structure into a sequence of bytes. Ethereum internally uses an encoding format called recursive-length prefix encoding (RLP), described here

Uncle: See Ommer, the gender-neutral alternative to aunt/uncle.

Ommer: a child of a parent of a parent of a block that is not the parent, or more generally a child of an ancestor that is not itself an ancestor. If A is an ommer of B, B is a nibling (niece/nephew) of A.

Uncle inclusion mechanism: Ethereum has a mechanism where a block may include its uncles; this ensures that miners that create blocks that do not quite get included into the main chain can still get rewarded.

Account nonce: a transaction counter in each account. This prevents replay attacks where a transaction sending eg. 20 coins from A to B can be replayed by B over and over to continually drain A's balance.

EVM code: Ethereum virtual machine code, the programming language in which accounts on the Ethereum blockchain can contain code. The EVM code associated with an account is executed every time a message is sent to that account, and has the ability to read/write storage and itself send messages.

Message: a sort of "virtual transaction" sent by EVM code from one account to another. Note that "transactions" and "messages" in Ethereum are different. A "transaction" in Ethereum parlance specifically refers to a digitally signed piece of data, originating from a source other than executing EVM code, to be recorded in the blockchain. Every transaction triggers an associated message, but messages can also be sent by EVM code, in which case they are never represented in data anywhere.

Storage: a key/value database contained in each account, where keys and values are both 32-byte strings but can otherwise contain anything.

Externally owned account: an account controlled by a private key. Externally owned accounts cannot contain EVM code.

Contract: an account which contains, and is controlled by, EVM code. Contracts cannot be controlled by private keys directly; unless built into the EVM code, a contract has no owner once released.

Ether: the primary internal cryptographic token of the Ethereum network. Ether is used to pay transaction and computation fees for Ethereum transactions.

Gas: a measurement roughly equivalent to computational steps. Every transaction is required to include a gas limit and a fee that it is willing to pay per gas; miners have the choice of including the transaction and collecting the fee or not. If the total number of gas used by the computation spawned by the transaction, including the original message and any sub-messages that may be triggered, is less than or equal to the gas limit, then the transaction processes. If the total gas exceeds the gas limit, then all changes are reverted, except that the transaction is still valid and the fee can still be collected by the miner. Every operation has a gas expenditure; for most operations it is ~3-10, although some expensive operations have expenditures up to 700 and a transaction itself has an expenditure of 21000.


## Other

Hash Rate
The hash rate is the measuring unit of the processing power of the Bitcoin network. The Bitcoin network must make intensive mathematical operations for security purposes. When the network reached a hash rate of 10 Th/s, it meant it could make 10 trillion calculations per second.

Mining
Bitcoin mining is the process of making computer hardware do mathematical calculations for the Bitcoin network to confirm transactions and increase security. As a reward for their services, Bitcoin miners can collect transaction fees for the transactions they confirm, along with newly created bitcoins. Mining is a specialized and competitive market where the rewards are divided up according to how much calculation is done. Not all Bitcoin users do Bitcoin mining, and it is not an easy way to make money.

P2P
Peer-to-peer refers to systems that work like an organized collective by allowing each individual to interact directly with the others. In the case of Bitcoin, the network is built in such a way that each user is broadcasting the transactions of other users. And, crucially, no bank is required as a third party.

Private Key
A private key is a secret piece of data that proves your right to spend bitcoins from a specific wallet through a cryptographic signature. Your private key(s) are stored in your computer if you use a software wallet; they are stored on some remote servers if you use a web wallet. Private keys must never be revealed as they allow you to spend bitcoins for their respective Bitcoin wallet.

Block Chain
The block chain is a public record of Bitcoin transactions in chronological order. The block chain is shared between all Bitcoin users. It is used to verify the permanence of Bitcoin transactions and to prevent double spending.

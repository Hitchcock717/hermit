---
title: 比特币 
date: 2019-11-22 18:37:56
tags: [Note, Markdown]
categories: Note
---
## Bitcoin —— Crypto-Currency
*Two functions*
1. Hash
2. Signiture (Public-key cryptography)

### Hash
*Three functions*
**1. collision resistance** 抗碰撞性
> collison refers to:
	input x != y;
	output H(x) = H(y)

	** In theory, it works**

	Practice: Upload a file on the cloud platform, how to prevent anyone from tampering it?
	Solution: 
	1. Consider it as an input file, caculate its hash(H(input)) and save it in local space. Then upload it. 
	2. Download the file from the cloud and recaculate its hash.
	3. Compare two hashes. If different, it has been tampered.

> MD5: Hash algorithm 
	can produce a 128-bit hash value
	can be cracked
	cannot be utilized into SSL pub-key certificate & digital signiture

**2. Hiding** 单向不可逆性
> 	input X ——> H(X)
	H(X) !——> X

	** Brute force can crack it**

#### Collision resistance + Hiding ——> Digital Commitment
>	Initially, publicize H(X); then publicize X, because H(X) is known and hiding allows it is impossible to deduce X from H(X). To verify X, recaculate H(X). 

**3. Puzzle Friendly**
>  It is unpredictable to calculate H(X). Brute Force is the only path. 
>  POW proof of work
   Get newest info of block header; then try nonce, calculate (SHA-256(SHA-256(block header)) to satisfy the requirement of **H(block header) <= target**

### Signiture
	1. private key represents miner's control over BitCoin
	2. Used in Transaction

## BitCoin —— Data Structure
*Two Structure*
1. Hash Pointers
2. Merkle Tree

**Hash Pointers**
图示：{% asset_img WechatIMG604.png BitCoin-1 %} [摘自简书](https://www.jianshu.com/p/f3570d8e1d27)
> Compared with normal pointers, hash pointers can detect tampering by saving extra hash into the structure body.
图示：{% asset_img WechatIMG605.png BitCoin-2 %}  [摘自简书](https://www.jianshu.com/p/f3570d8e1d27)
> According to above pic, there is only a need to remember the last hash if detecting tampering because block chain is a linked list using hash pointers. 

**Merkle Tree**
图示：{% asset_img WechatIMG606.png BitCoin-3 %}  [摘自简书](https://www.jianshu.com/p/f3570d8e1d27)
> First Tier(root node): Root Hash saved; Hash(root hash) = Hash(concat[hash(child node1)+hash(child node2)])
  Second/Third Tier: Hash Pointers; Save the hashes of data blocks in the bottom node
  Bottom Tier(omitted): called 'tx' ——> transaction 

Obviously, it is enough to save root hash if detecting tampering. And each block is divided into two sections: one is block header which saves root hash without any tx; the other is block body which saves tx.

> 
Node: Any computing machine in the block chain network, e.g. cellphone, mining machine, server...
Full Node: block header & block body saved
Light Node(like wxapplet): block header saved only

Question: How to prove any transaction logged into the block chain in terms of light nodes?

Solution: The Merkle Tree can provide Merkle Proof.
图示：{% asset_img WechatIMG607.png BitCoin-4 %}  [截取自课程视频](https://www.bilibili.com/video/av37065233?p=3)
Proof of Membership: theta(log(n)) complexity if proposing Num(n) tx in the entire tree.
Proof of Non-Membership: theta(n)

## BitCoin —— Concensus Protocol
Question: How does Central Bank issue digital currency?

Solution One: Spending = Duplication; may cause 'double spending'
Solution Two: Create a list of recording each note's owner, e.g.
> 017 ——> Bob
  018 ——> Tim
  019 ——> Syria
Then ceritfy the note before transactions; Valid, but centralized
BitCoin is de-centralized, so the responsibility of verifying notes has transferred from the central bank to the mass. 

Two impending quetions about issuing digital currency:
1. Who owns the legal right to issue?
2. How to verify the validity of transaction to prevent from double spending?

For Question One:
> Need to know how to make BitCoin transactions first
Create a blcok chain: two types of hash pointer exist; One is to target at the connection between blocks. The other is to target at the source of each BitCoin.
The entire transaction includes: Input ——> to explain the source and the pub-key of payer; Output ——> to explain the pub-key hash of recipients 

Some sub-questions:
1. During the process of transaction, does the payer(A) need to know something about the recipient(B)?
Answer: A needs to know B's address because this address is calculated based on B's pub-key.
2. During the above process, does B need to know something about A?
Answer: B needs to know A's pub-key, namely, A's identity. Each node needs to know A's pub-key in order to verify it. 
3. If B' disguises himself as A and claims to make transaction with A's pub-key, how to prevent this situation?
Answer: The output of Coinbase tx saves the hash of the source.

How to put the transaction info into the block chain?
The content of ledger needs to achieve distributed consensus.
>But FLP impossibility result tolds:
In an asynchronous system, there is no cap on the network transmition and even if at least one member reveals faulty, concensus is impossbile.

Type of Potential attacks:
1. Sybil attack: the minority nodes control multiple fake identities to attack other normal nodes in majority.
Solution in BitCoin: Computing power voting 
2. Forking attack: Not in the longest valid chain
Imagin that two blocks of the same length has been mined at the same time, which one is to be accepted?
Solution in BitCoin: Keep watching for a while. If the one is first to be continued, the other is considered as 'orphan block'.

The reason why mining: For blcok reward only offered by coinbase tx and transaction fee

## The realization of BitCoin system
BitCoin vs Etheroem: Transaction-based ledger; Account-based ledger

Question One:
> Supposing that the most computing power is controlled by honest nodes, is it possible to prove all transactions recorded in blocks valid?
Answer: If node A transfers fee to fake node M
The fake transaction will not be validified because M cannot falsify A's private key, which proves the transaction is unacceptable. Then the block becomes an orphan.

Question Two:
> Supposing that a malicious node with ledgering right makes double spending attack, will the situation be?
Answer: If the malicious node M makes M-to-A transaction, and at the same time makes M-to-M' transaction, this kind of forking attack forces other honest nodes to be connected with M-to-M' block and M-to-A block becomes an orphan. How to prevent from M's receiving goods without paying?
Just waiting for several confirmations from following blocks. It is prescribed that at least six confirmations can prove the chain to be valid in BitCoin concept.

From the above case, it can be concluded that the irrevocability of block chain is temporary, particularly in the initial phase of recording in the blocks, even if the entire chain is an irrevocable ledger.

Question Three:
> Supposing that a malicious node with ledgering right resists recording valid transactions into the blocks.
Answer: Never mind. Waiting for next block.
In fact, BitCoin sets limits to each block's transaction num. The limit is not more than 1M. If the current block cannot record info, then wait for next.

### Selfish Mining
Selfish mining is a strategy for mining bitcoin in which groups of miners collude to increase their revenue. Bitcoin was invented to decentralize production and distribution of money. But selfish mining can result in centralization of bitcoin mining operations. [参考自investopedia](https://www.investopedia.com/terms/s/selfish-mining.asp)

Threats from selfish mining:
1. The safety of the entire network decreases. No longer need 51 per cent computing power to make attacks.
2. Some miners with limited computing power find selfish mining a preferable strategy. 

### UTXO 

#### Unspent Transaction Output

{% asset_img UTXO.png UTXO %}

[参考知乎]( https://www.zhihu.com/question/59913301)

## BitCoin Network 
Desiging principle: Simple, robust but no efficient
> Because each node needs to maintain a group of transactions waiting for being recorded into blocks.
If listening a A-B transaction, record it;
If listening a A-C double spending attack, deny it;
If listening a same A-B transaction, delete it;
If listening a same A-C transaction (the same source), delete it. 

## The adjustment of mining difficulty in BitCoin
Difficulty = (difficulty - 1 - target) / target [difficulty=1]

Question One:
Why adjusting its difficulty? If the time for generating blocks is too short, what is its result?
Forking attack is easy to make. Even multiple forks, makes it harder for the chain to achieve concensus.
The speed for generating blocks is ten mins and that for ETH is fifteen secs, meaning it is necessary for ETH to have a new ghost. Because in the ghost, orphan block cannot be abandoned randomly, but given rewards.

Question Two:
How to adjust mining difficulty?
Every 2016 blocks (about two weeks) as an interval to adjust the target threshold. The equation is:
> Target = target * (actual time/expected time)
actual time refers to the real spent time for generating 2016 blocks in the chain;
expected time refers to the expected spent time for generating 2016 blocks in the chain.

Therefore, smaller the target is, more difficulty the mining will have.
Relevant question: if the chain holds a malicious node, how to deal with it if not adjust target in the code?
Answer: The honest miners will not accept it if not adjust the block publicized. 

## BitCoin Mining
Proof of safety in BitCoin:
1. Cryptography
2. Consensus

Equipment for mining:
Generation one: CPU
Generation two: GPU
Generation Three: ASIC

Mining Pool:
Pool Manager (responsible for what full nodes require to do) ——> Several Miners (calculate hash)

How to distribute profits?
Depending on POW. Supposing that the pre-70 zero of target nonce can meet the requirement, the manager can regulate that 1 share will be earned if first finding pre-60 zero of target nonce. Afterwards, profits will be distributed based on the num of share when BitCoin is ensured.  

Supposing that there is a pool of at least 51 per cent computing power, which kind of attack can it make?
> 1. forking attack
  2. boycott; If malicious node A wants the entire chain to boycott B's every relevant transaction, A will fork a block without B if A finds a block with B. More terribly, if A makes boycott in public, other 'weak' miners dare not put B's transaction into blocks because it will be in vain if put it. 
  3. Stealth; Impossible 

## BitCoin Script
[参考自知乎巴比特](https://zhuanlan.zhihu.com/p/25461051)
输入交易见图示：{% asset_img WechatIMG608.png BitCoin-5 %} 
输出交易见图示：{% asset_img WechatIMG609.png BitCoin-6 %} 

### Stack 
Core: Last in First Out
In the ouput content, OP_DUP means duplicating the top element in the stack; OP_EQUALVERIFY means verifying whether two elements in the top of stack are equal.

### Transaction 
{% asset_img WechatIMG610.png BitCoin-7 %} 

### Standard transaction script
P2PKH, Pay to Public Key Hash
When Alice wants to transfer fees to Bob, input script shows Bob's address (equals pub-key hash);
When Bob wants to transfer fees to Carol, output script shows Bob's pub-key and signiture signed by Bob's private-key because Bob wants to prove he owns his private-key of this address.

Therefore, output script shows the recipient's pub-key hash; input script shows his sig & pub-key.

How to run input/output script?
> Input script is initialized. Owing to the rule of script that is run from left to right, sig is first put into the stack, and then is the pub-key.
> Then, output script is run from left to right. The first order is OP_DUP.
> Next, calculate OP_HASH160. That means calculating the top element hash, to get pub-key hash.
> Afterwards, put pub-key hash of output script into the stack. It should be distinguished with the previous hash.
> Run OP_EQUALVERIFY, to verify whether two hashes in the top of stack are equal. If equal, then to be continued; if not, kill and return false.
> Run OP_CHECKSIG, to use two elements (pub-key and sig left in the stack) in the top of stack as verifying whether sig is valid. If valid, return success; if not, return false.

### Proof of burn
If any word of 'return' is recorded in the output script, the result will return false whatever the input script is designed as. Then corresponding UTXO will be deleted.
Function: 'burn' a little BitCoin to charge for recording info in the block.

## Fork in BitCoin
Types:
1.Protocol Fork
2.Hark Fork
3.Soft Fork

### Hard Fork
Due to block size limit.
The original limit is 1M. When upgrading, the limit will increase to 4M. But the upgrade could be finished in the most nodes with certain computing power. By calculating, it takes one sec to finish seven transactions. The speed for making transaction is low compared with other large-size payment network. 
The fork shows the disagreement among the old nodes and new olds which have been upgraded. Two distinctive groups do not accept the chain each other. So two paralleled chains have formed and will not disappear.

### Soft Fork
During the upgrading process, small blocks will be discovered in the new nodes. However, old nodes insist mining bigger blocks and will stop later. The reason why old nodes stopping mining rests on their agreement on the other chain. So even if bigger blocks are discovered in the future, they will be abandoned (orphan nodes). The forks are shown in this process, but will disappear eventually. 

### Possible situation when soft forks will be confronted
1. Eight bytes in the domain of coinbase are used as extra nonce;
2. If light nodes verify whether some transaction is recorded in the block, then one merkle proof for full node is ok;
3. Full nodes maintain UTXO in local to know the remaining amount of some account;
4. Light nodes cannot know the remaining amount of some account;
5. Someone recommends that take hash(UTXO) into the domain of coinbase.

## Q & A about BitCoin
Q1: If the recipient is off-line during the transaction, what will be?
>A1: No need to keep online.

Q2: What can I do if I lost my private-key?
>A2: Nothing if you have confidence in transaction institutions.

Q3: What can I do if I revealed my private-key?
>A3: Transfer all to another account.

Q4: What can I do if I record wrong address?
>A5: Nothing you can do to cancel your transaction. If transfer to no-place, you will have no returns.

Q5: Since every transaction recorded into the blocks needs to be verified, why OP_RETURN in the proof of burn will be accepted?
>A6: For one transaction, we need to verify the input & output script of current transaction. However, OP_RETURN is recorded into the output script of the current transaction. So it will not be verified.

Q6: How to prevent from stealing by other miners?
>A6: In the coinbase tx, the address owned by the recipient has been recorded. If to steal, the address needs chaning. But once the address changed, merkle tree will be changed and correspondingly, root hash will be changed as well. Finally, block header will not be the same as the previous one. The nonce is invalid.

Q7: How is transaction fee transferred to targeted miner?
>A7: No need to know before transferring.

## The Anonymity of BitCoin
Its anonymity reveals not as good as we expect.

### Several possible ways to nullify its anonymity
1. Even if multiple inputs and ouputs have been generated in a single transaction, their relevant addresses are likely to be manually linked.

2. The address/account may be linked with the identity in the real world. Any link can be made when BitCoin world makes contacts with the real world, and the identity is put in danger. To prevent from money laundering, it is necessary to keep close watch on the input/output chain of any asset. E.g. Silk Road

How to improve anonymity of BitCoin as possible as I can?
> In the application layer, coin mixing is preferable.
> In the network layer, multiple-route transmittion to stop from deducing real identity from IP address of any node. 

### Proof of Zero-knowledge 
[参考自blog](https://learnblockchain.cn/2019/04/18/learn-zkSNARK/)

## Thoughts on BitCoin
1. Block Love
> Try not to truncate private-key, but use multiple sigs.

2. BitCoin does not bypass those impossible results from distributed consensus because it fails to give reasonable explanations, such as forks.

3. Scarcity of BitCoin

4. Quantum Computing
Q: Will quantum computing threaten BitCoin's development?
   1. Far away from applications;
   2. Make possible threat to traditional financial industry;
   3. Crypto and Hash differ. Nothing can reverse collision resistance of hash. 








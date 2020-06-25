# Scaling Bitcoin

Table of contents

1. Explain the problem: Blockchains don't scale
2. Consequences of the problem
3. Mitigation/solution strategies

### Problem: Blockchains don't scale

The blockchain chain size,  can be calculated as: 
$$
\begin{align}
S_{tot} =& S_{tx} n_{tx/user} N \\
S_{tot} \hat =& \text{Total chain size} \\
S_{tx} \hat =& \text{Average transaction size} \\
n_{tx/user} \hat =& \text{Average transactions per user} \\
N \hat =& \text{Total number of users} \\
\end{align}
$$
This simple formula shows that increased usage for a fixed amount of users and an increased userbase both create a problem. With the ability to anker arbitrary data via hashes into the bitcoin blockchain, bitcoin is much more than simply a system for money, but useful for anything that benefits from immutability.

The distributed nature of blockchains require that all transactions are transmitted, stored and verified by everyone. This incurres bandwidth, storage and computation cost by all participants. These costs scale approximately with the chain size. Bitcoin has the block size limit to limit these costs for each participant. The trade-off sets a hard limit on the capacity, requiring some systems keeping transactions off the blockchain, commonly referred to as trusted or untrusted higher layers.

### Consequences of the problem

This scaling problem is fundamental and might lead to such high transaction costs, that the fundamental properties (like censorship resistance) are only available to the rich if they want to exit the higher layers. More about this in https://anchor.fm/thecryptoconomy/episodes/Read_405---Bitcoin-May-Not-Survive-a-Bitcoin-Standard-Hasu-efkdbh. 

That this will lead to (mainly) custodial solutions is also discussed in [What Bitcoin Is](https://stephanlivera.com/episode/185/) by Vijay Boyapati (who also authored ) who also authored [The Bullish case for Bitcoin](https://medium.com/@vijayboyapati/the-bullish-case-for-bitcoin-6ecc8bdecc1) ([audio version](https://anchor.fm/thecryptoconomy/episodes/Read_407---The-Bullish-Case-for-Bitcoin-Vijay-Boyapati-efpi06)).

Custodial solutions however lead us back to IOUs, which did not work out well for gold.  

### Mitigation/solution strategies

#### Transaction size reduction

Thanks to taproot and tapscript (which will be implemented in bitcoin soon) even complicated scripts will require very little block space, addressing the *average transaction size* in the formula above. However one cannot hope to gain anything close to an order of magnitude here.

#### Lightning network

The lightning network enables unlimited number of transactions per user, if the user has created a sufficient amount of channels. However creating channels itself requires transactions, and considering that there have been only half a billion transactions in a little over 10 years of bitcoin history it is questionable if it has enough capacity to create channels for billions of people. (That Lightning is not secure to use for payments below the blockchain fee is an additional problem.)

#### Cut-through

In Mimblewimble exists the possibility to remove intermediate transactions from the blockchain without deminishing the security of the chain, called "cut-through". This reduces the storage problem, but leaves the bandwidth and computational costs unchanged. It is unclear if such a cut-through could be applied to bitcoin.

#### Driveshains

[Drivechains](https://www.drivechain.info/peer-review/peer-review-new/) (a kind of sidechain) seem by far the most promising in the long term. Sidechains generally allow to transfer bitcoin into the sidechain (peg-in) and transfer them back into the bitcoin blockchain (peg-out). While peg-in is easy, doing peg-out in a trust-minimized way is hard. Drivechains resort here to a very very slow peg-out. 

One or many drivechains (1), (2)..., which also have a fixed block size, could anker into the bitcoin blockchain. A normal user would however have funds only in one drivechain, e.g., drivechain (1). If they wanted to transact with a user from drivechain (2) they would need to use an intermediary (this intermediary could be non-custodial, such as a lightning network exchange). 

Advantages:

* Users have their funds non-custodial
* If drivechain (1), (2).... have also all too high fees, each drivechain could have more childs (11), (12),...  and (21), (22),....  This allows an exponentially large tree, therefore scalable to billions of people, while the user only needs to keep track of the particular branches they have funds in

Disadvantages:

* Transactions cannot be done from anyone to anyone in the same block chain. One needs to have (ideally non-custodial) intermediaries bridging the chains. Luckily this could be completely automated and hidden from the user.
* There are more trade-offs to drivechains and the drivechains would need to grow into reliable and trustable chains similar to bitcoin today.




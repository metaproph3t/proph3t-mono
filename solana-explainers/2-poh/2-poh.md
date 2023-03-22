# Solana Internals, Part 2

*Much of this post is taken from Zantetsu's post here: https://www.shinobi-systems.com/primer.html. The value-add of this post is that it adds pictures and compresses the ideas down to a shorter post. I recommend anyone follow him @ShinobiSystems on Twitter.*

There are [8 key innovations](https://medium.com/solana-labs/7-innovations-that-make-solana-the-first-web-scale-blockchain-ddc50b1defda) that make Solana the first web-scale blockchain. One of the most important is Proof of History (PoH). Indeed, if Anatoly had not come up with PoH in a late-night brainstorm, Solana would not exist.[^1]

Most people in the Solana ecosystem understand *how* PoH works, at least at a high-level. Few understand *why* it is needed. This is what we will unpack in this post.

## Context

Suppose that you and two friends are building a blockchain. Each of you will run a node and your nodes will take turns producing blocks.

To implement this, you create a *leader schedule*. This schedule divides time into 10 second *slots* and assigns one validator per slot.

![leader schedule](media/leader-schedule.png)

During each slot, the following must happen:
1. The leader packages all user transactions into a block.
2. The leader transmits this block.
3. Validators forward the block until all validators have received it.

Since your blockchain contains only 3 validators, the third step won't be relevant, but you can imagine that it would be important on a blockchain with thousands of nodes like Solana.

![slot activity](media/slot-activity.png)

Remember that your slots are each 10 seconds long. What would happen if you made them shorter?

The obvious advantage of shorter slot times is less latency. For example, if someone is using your blockchain to pay for their Starbucks, shorter slot times would mean that they spend less time at the counter waiting for their payment to go through.

On the other hand, shorter slot times also have an issue: increased risk of forking. 

For example, imagine that you try shrinking slot times to 1 second, like so:

![leader schedule](media/leader-schedule-1s-slot.png)

You restart the blockchain with this change, and the first 3 blocks are processed normally. But then, this happens:

![fork](media/blockchain-fork.png)

What is happening here? Most likely, B didn't receive block 3 by the time it needed to produce block 4, which then caused it to act like block 3 hadn't been produced. Maybe A is on a crappy connection in Bangkok and B is in Cape Town, and it took the block 2 seconds to transmit from A to B.

And so we have a fork in the network. Forks are bad because they slow down the process of coming to consensus on a 'canonical ledger' and 'canonical state.' And without a canonical state, blockchains are useless.

Hence, your task as a blockchain-builder is to pick a slot time that (1) satisfies your users latency requirements and (2) minimizes forks. The faster internet your nodes run, the lower slot times you can get away with, which is why Solana can get away with 800ms instead of Ethereum's 15s.

## PoH as a slot time enforcer

Unfortunately, your task doesn't end at picking a slot time. You also need to *enforce* that your chosen slot time is followed. 

For example, suppose that B didn't *miss* A's block but was actively *trying to censor* it. Maybe B and A are having a feud, and B wants to censor A's blocks until A 'says uncle.'

If B waits his turn before transmitting his censoring blocks that ignore A's blocks, he's not going to be very effective. C will see A's first, commit to it (by voting, a can of worms I don't want to open here), and then will simply ignore B's block.

However, if B 'jumps the gun,' he could get C to commit to B's block before she sees A's block. This would effectively censor A by preventing A's blocks from being included in the final blockchain.

![censoring block](media/censoring-block.png)



[^1]: See *Whiteboard Series with NEAR | Ep: 2 Anatoly Yakovenko from Solana*, accessible here: https://youtu.be/rKGhbC6Uync.
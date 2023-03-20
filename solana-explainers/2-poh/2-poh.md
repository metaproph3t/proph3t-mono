# Solana Internals, Part 2

*Much of this post is taken from Zantetsu's post here: https://www.shinobi-systems.com/primer.html. The value-add of this post is that it adds pictures and compresses the ideas down to a shorter post. I recommend anyone follow him @ShinobiSystems on Twitter.*

There are [8 key innovations](https://medium.com/solana-labs/7-innovations-that-make-solana-the-first-web-scale-blockchain-ddc50b1defda) that make Solana the first web-scale blockchain. One of the most important is Proof of History (PoH). Indeed, if Anatoly had not come up with PoH in a late-night brainstorm, Solana would not exist.[^1]

Most people in the Solana ecosystem understand *how* PoH works, at least at a high-level. Few understand *why* it is needed. This is what we will unpack in this post.

---

Suppose that you and two friends want to build a blockchain. Because you want the blockchain to be decentralized, each of you will run a node. Your nodes will take turns producing blocks, like this:

![leader schedule](media/leader-schedule.excalidraw.png)

This is a *leader schedule*. Leaders are scheduled into *slots*, which are in this case 1 second long. During each slot, the following must happen:
1. The leader packages all user transactions into a block.
2. The leader transmits this block.
3. Validators forward the block until all validators have received it.
4. Validators ensure that the block is valid and replay its transactions onto their own state.
5. Validators attest to the block's validity by transmitting *votes*.

We need votes because we need some way of deciding what is the *canonical state*. You can think of validators as committee members. Like committee members, each will express its opinion about what the committee should do. And like good committee members, each will ultimately abide by the supermajority consensus, whether they agree with it or not. This is what allows us to say things like "I own 10 SOL" instead of things like "validators A, B, and C say I own 15 SOL but validators D, E, and F say I own 5."

This is what happens each slot, represented visually:





Note that our *slots* are 1 second long. Thus, there should be able 1 second in between blocks. 

1 second is fine if you are all in the same city and can send messages over the internet within a few milliseconds. But what if A is in Shanghai, B is in New York City, and C is in Cape Town?

If the time it takes for a message to transmit between nodes is sufficiently large, a 1 second slot time becomes no longer feasible. Consider all of the things that need to happen during the slot time:
1. The leader needs to package all received transactions into a block and send this block to the other nodes.
2. The other nodes need to check this block's validity (i.e., signature verifications) and replay it onto their own state.
3. If the block is valid, the other nodes need to attest to this by creating and transmitting a *vote* to the other nodes.

Step three is necessary because the chain needs to come to consensus on what is the *canonical state*. 



[^1]: See *Whiteboard Series with NEAR | Ep: 2 Anatoly Yakovenko from Solana*, accessible here: https://youtu.be/rKGhbC6Uync.
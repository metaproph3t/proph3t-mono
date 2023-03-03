## Introduction

Perhaps you accept the fact that the world is filled with corrupt institutions. You may wonder if anything can be done.

We will explore this question in this post. We will do this in three stages:
1. defining the problem clearly,
2. discussing prior approaches to the problem,
3. and describing the mechanisms of the Meta-DAO.

## The Problem

In any given institution (an economy, a firm, a nation, etc.), decisions need to be made. These decisions have consequences. We can group these consequences into two categories:
- local consequences: those that impact the person who's making the decision
- global consequences: those that impact the members of the institution as a whole

We can also separate between the beneficial and the harmful consequences.

Given this, we can map all of a decision's consequences onto the following matrix:

![2x2matrix](media/decision2x2.excalidraw.png)

For example, a decision by a politician to distribute cash payments to his or her constitutions may be mapped like so:

![airdrop2x2](media/airdrop2x2.excalidraw.png)

If we put political dogma aside, it becomes apparent that distributing cash payments makes sense in some scenarios and does not make sense in some others.

For example, consider a world where the government can borrow cheaply, the cost of distributing payments is low, and all citizens will invest their money at a high interest rate. In this world, borrowing money to distribute cash payments makes sense.

Inverseley, in a world where the government can only borrow at a high rate, the cost of distributing payments is high, and citizens would use the money to buy things that wouldn't make them happy, borrowing money to distribute cash payments does not make sense.

If we generalize, we find that we would like decision-makers to take decisions if, and only if, their global benefits outweigh their global costs. This can be represented in algorithmic form:

```rust
// ideal decision-maker algorithm
if expected_global_benefit(action) > expected_global_cost(action) {
    do(action);
} else {
    disregard(action);
}
```

Imagine a society where humans had this algorithm imprinted into their brain. The vast majority of actions taken in this society would be a step forward for the society as a whole. Steps back would only be a result of lack of information, not bad intent or misaligned incentives. By this time, this society would be many steps ahead of our own - with abundant goods for all humans, technological advances beyond our collective comprehension, colonies on multiple planets, etc.

Of course, humans do not tend to make decisions in this way. The central problem in designing institutions is creating mechanisms such that groups of people can *simulate* this ideal.

## Prior approaches

There have been three prominent approaches to this problem. We will call these:
- Philosopher kingdoms 
- Aligning incentives 
- Atomize! 

### Philosopher kingdoms

![how an altruistic decision-maker would make decisions](media/altruistic-decision-maker.excalidraw.png)

Plato first described this approach in *The Republic*. He thought that most people were dumb and/or greedy, but that some were both intelligent and altruistic. A philosopher kingdom tries to identify these individuals and then gives them all the power. The theory is that they will ignore their local costs and benefits and only focus on the betterment of the group as a whole.

- founder-led companies
- catholic church
- dictatorships

### Internalize decision-maker externalities

Another approach is to say, 'okay, humans aren't alruistic, but what if I can design decision-maker incentives such that what's in the interest of the group is in their interest?'

![externality internalization](media/externality-internalization.excalidraw.png)

This approach has had varying degrees of success. In markets, where profit-maximizers need to produce things of value to maximize their profits, it's been very successful. It's had *some* success in the following instantiations:
- Cultures & religions that praise altruists (honor, virtue, loving thy neighbor, etc.)
- Management and employee stock plans
- Democracies
- Public companies
- Hierarchical bureaucracies

These systems all have their own shortcomings. A common one across cultures, religions, democracies, and public companies, is that they each suffer from tragedies of the commons. For example, a shareholder of a public company has a very limited incentive to determine which board members are pushing the company forward instead of just pushing their career forward. This is also why token-voting DAOs won't work over the long-term.

## The Meta-DAO's approach



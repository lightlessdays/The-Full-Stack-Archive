---
title: "Simplifying Deterministic Finite Automata Creation"
datePublished: Fri Dec 08 2023 11:38:54 GMT+0000 (Coordinated Universal Time)
cuid: clpwk0fbd000m08juainbg8rd
slug: simplifying-deterministic-finite-automata-creation
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702035494740/16e11694-b49d-47e3-bf72-f14416dda6ee.png

---

This article is for those people who find drawing DFAs in the Theory of Computation hard. I am going to make it simple for you. Let us start by considering a question.

**Question: Construct a DFA of all strings that end in double letter.**

**Answer:**

The easiest thing you can do is start by writing the regular expression for this. The regular expression for this will be:

```bash
(a + b)* (aa + bb)
```

Great, now the next easiest thing is to draw NFA for this regular expression.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702032639447/85495159-7003-4c46-b0b5-4e167fb55701.png align="center")

Now, let us understand this NFA. Whenever we have something like (a)\* in a regular expression, then we will create a self-loop of that alphabet in NFA. If we have a "+" then we will split its branch. Now, let us construct a DFA from this. First of all, we will draw the transition tables for this NFA.

| **STATE** | a | b |
| --- | --- | --- |
| ➡️q0 | q0, q1 | q0, q2 |
| q1 | q3\* | \- |
| q2 | \- | q4\* |
| q3\* | \- | \- |
| q4\* | \- | \- |

If we look at it carefully, this table is nothing but where can a and b go from any particular state. Here, \* represents a final state, and ➡️ represents an initial state.

Now we will convert this table T into a table T', which will help us make the DFA. To make the DFA, we will start by writing the transition states of ➡️q0. This will always be our first entry.

| **STATE** | a | b |
| --- | --- | --- |
| ➡️q0 | {q0, q1} | {q0, q2} |

Now the next transition state we make will be either of {q0, q1}, or {q0, q2}. This implies that the next transition states will only be those that are present in the sets in columns a or b.

| **STATE** | a | b |
| --- | --- | --- |
| ➡️q0 | {q0, q1} | {q0, q2} |
| {q0, q1} | {q0, q1, q3\*} | {q0, q2} |

So, how did we get values for the next subset in a and b? Well... first of all we inserted all values that a can be at q0 and then values for a at q1. Similarly, we inserted values for b at q0 and then values of b at q1. However, if we observe table T, we will observe that b is empty. So, we will not add any additional value to our set. Next, let us add {q0, q2} to our state.

| **STATE** | a | b |
| --- | --- | --- |
| ➡️q0 | {q0, q1} | {q0, q2} |
| {q0, q1} | {q0, q1, q3\*} | {q0, q2} |
| {q0, q2} | {q0, q1} | {q0, q1, q4\*} |
| {q0, q1, q3\*} | {q0, q1, q3\*} | {q0, q2} |
| {q0, q1, q4\*} | {q0, q1} | {q0, q1, q4\*} |

This is our table. Now, we can draw DFA using this table.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702035315537/35db1c5c-14c8-4b82-ad08-17beafd5a2bc.png align="center")

As simple as that - we drew a DFA without thinking of a logic for DFA - how cool is that?
---
layout: post
title: Balancing My Spending
source: https://www.reddit.com/r/dailyprogrammer/comments/7vx85p/20180207_challenge_350_intermediate_balancing_my/
level: intermediate
---

Given my bank account transactions - debits and credits - as a sequence of integers, at what points do my behaviors show the same sub-sums of all transactions before or after. Basically can you find the equilibria points of my bank account?

## Input Description
You'll be given input over two lines. The first line tells you how many distinct values to read in the following line. The next line is sequence of integers showing credits and debits. Example:

```
8
0 -3 5 -4 -2 3 1 0
```

## Output Description
Your program should emit the positions (0-indexed) where the sum of the sub-sequences before and after the position are the same. For the above:

```
0 3 7
```

Meaning the zeroeth, third and seventh positions have the same sum before and after.

## Challenge Input

```
11
3 -2 2 0 3 4 -6 3 5 -4 8
11 
9 0 -5 -4 1 4 -4 -9 0 -7 -1
11 
9 -7 6 -8 3 -9 -5 3 -6 -8 5
```

## Challenge Output

```
5
8
6
```

## Bonus
See if you can find the O(n) solution and not the O(n2) solution.

---

## My Solution
Input format:
```javascript
const input = {
  length: 11,
  values: [3, -2, 2, 0, 3, 4, -6, 3, 5, -4, 8]
}
```

```javascript
function rightSums(input) {
  sums = [];

  input.values.forEach((credit, i, credits) => {
    let sum = 0,
    bound = input.length;

    for (var i = i + 1; i < bound; i++) sum += credits[i];
    sums.push(sum);
  });

  return sums;
}

function leftSums(input) {
  sums = [];

  input.values.forEach((credit, i, credits) => {
    let sum = 0,
    bound = -1;

    for (var i = i - 1; i > bound; i--) sum += credits[i];
    sums.push(sum);
  });

  return sums;
}

function balance(input) {
  let ans;

  leftSums(input).forEach( (sum, i) => {
    if (sum === rightSums(input)[i]) ans = i;
  });

  return ans;
}
```
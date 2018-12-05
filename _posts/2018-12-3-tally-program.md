---
layout: post
title: Tally Program
source: https://www.reddit.com/r/dailyprogrammer/comments/8jcffg/20180514_challenge_361_easy_tally_program/
level: easy
---

5 Friends (let's call them a, b, c, d and e) are playing a game and need to keep track of the scores. Each time someone scores a point, the letter of his name is typed in lowercase. If someone loses a point, the letter of his name is typed in uppercase. Give the resulting score from highest to lowest.

## Input Description
A series of characters indicating who scored a point. Examples:

```
abcde
dbbaCEDbdAacCEAadcB
```

## Output Description
The score of every player, sorted from highest to lowest. Examples:

```
a:1, b:1, c:1, d:1, e:1
b:2, d:2, a:1, c:0, e:-2
```

## Challenge Input

```
EbAAdbBEaBaaBBdAccbeebaec
```

## Credit
This challenge was suggested by user /u/TheMsDosNerd, many thanks! If you have any challenge ideas, please share them in /r/dailyprogrammer_ideas and there's a good chance we'll use them.

---

## My Solution
```javascript
const tally = (score) => score
  .split('')
  .map(point => Object.assign({ gain: /[a-z]/g.test(point) ? 1 : -1 }, { player: point.toLowerCase() }))
  .reduce((tally, point) => (tally[point.player] = (tally[point.player] || 0) + point.gain, tally), {});

const utf = letter => letter.charCodeAt(0) - 97;

const print = (tally) => Object.entries(tally)
  .sort((a, b) =>  b[1] - a[1] !== 0 ? b[1] - a[1] : utf(a[0]) - utf(b[0]))
  .map(pair => pair.join(':'))
  .join(', ');

const scoreboard = (input) => print(tally(input));
```
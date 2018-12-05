---
layout: post
title: How Long Has the Light Been On?
source: https://www.reddit.com/r/dailyprogrammer/comments/7qn07r/20180115_challenge_347_easy_how_long_has_the/
level: intermediate
---

There is a light in a room which lights up only when someone is in the room (think motion detector). You are given a set of intervals in entrance and exit times as single integers, and expected to find how long the light has been on. When the times overlap, you need to find the time between the smallest and the biggest numbers in that interval.

## Input Description

You'll be given a set of two integers per line telling you the time points that someone entered and exited the room, respectively. Each line is a visitor, each block is a room. Example:

```
1 3
2 3
4 5
```

## Output Description
Your program should report the number of hours the lights would be on. From the above example:

```
3
```

## Input

```
2 4  
3 6  
1 3  
6 8
6 8
5 8
8 9
5 7
4 7
```

## Output

```
7
5
```

## Bonus Input

```
15 18
13 16
9 12
3 4
17 20
9 11
17 18
4 5
5 6
4 5
5 6
13 16
2 3
15 17
13 14
```

## Credit

This challenge was suggested by user /u/Elinaeri, many thanks. If you have an idea for a challenge, please share it in /r/dailyprogrammer_ideas and there's a good chance we'll use it.

---

## My Solution

```javascript
function timeSpent(room) {
  let visitor = room.split(/\n/g)
    .map(pair => pair.split(" "))
    .map(pair => pair.map(num => parseInt(num, 10)));

  let timeSpentInRoom = 0;

  visitor.sort((a, b) => a[0] - b[0]);
  visitor.forEach( (time, i, times) => {
    let timeSpentByvisitor = time[1] - time[0];
    let next = times[i + 1] ? times[i + 1][0] : false;

    if (next !== false && next < time[1]) {
      let diff = time[1] - next;
      timeSpentByvisitor = timeSpentByvisitor - diff;
    }

    timeSpentInRoom += timeSpentByvisitor;
  });

  return timeSpentInRoom;
}
```
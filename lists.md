---
layout: page
title: "Redis Lists"
---

Sometimes you find yourself want to store more than just one value string in one key. That's when when the
*lists* can be considered. Lists basically allow you to have a list of strings assigned to one
key. These strings are sorted by the time of insertion. So, you the programmer, have full
control over the order of the items in in one key.

Let explore lists with an example first. Let's say you want to keep track of your friends
in a key called `friends`. We will start by adding all of your friends to the key `friends`
using the command [rpush](https://redis.io/commands/rpush).

```
127.0.0.1:6379> rpush friends John
(integer) 1
127.0.0.1:6379> rpush friends Peter
(integer) 2
127.0.0.1:6379> rpush friends Paul
(integer) 3
127.0.0.1:6379> type friends 
list
```

`rpush` always returns the number of the elements in the list after each add. The command
can be used to add multiple elements in one run.

```
127.0.0.1:6379> rpush friends Li Bill Steve
(integer) 6
```

`rpush` always appends the elements to the end (tail) of the list. But if you want
to add elements to the beginning of the list instead, you can use the command
[lpush](https://redis.io/commands/lpush) instead.

See how we used the command `type` again to get the datatype of a key. In this case we
got `list` as expected.

## Getting the elements of a list

To get the elements of a list, we can use the command [lrange](https://redis.io/commands/lrange)
to get all or a subset of the list elements.

**More Coming Soon*











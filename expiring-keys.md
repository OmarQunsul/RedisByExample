---
layout: page
title: "Expiring Keys"
---

Redis stores all the elements, in memory, as a pair of keys and values. As it is a
very common case to use in-memory databases as a Cache Store, it makes sense sometimes
to make the keys automatically expires and by removed from the memory. So here is
it how it works.

Let's say you saved a new string key/value

```
127.0.0.1:6379> set name omar
OK
127.0.0.1:6379> expire name 60
(integer) 1
127.0.0.1:6379> get name
"omar"
```

In this example, I set a value for the key `name`, and set an expiration date on it
for it to be *60 seconds*. Within those 60 seconds, any time I issue the command
`get name`, I should get the value `omar` back. As long as Redis didn't receive another
command to alter or remove this key within this time. After 60 seconds, this is
what happens

```
127.0.0.1:6379> get name
(nil)
```

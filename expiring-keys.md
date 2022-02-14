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

## Setting Expiring String Keys Immediately

The command `expire` works on all the types of the values. So far we have been introduced only to **Strings**, so
let's see how to set expiring keys immediately using the set command.

The [set](https://redis.io/commands/set) can take different other optional parameters after the value.
one of them is `EX`, which is followed by the **number of seconds that the value will live**. In the
following example we can set the key `name` to `omar`, and it's going to expire after 5 seconds.

```
127.0.0.1:6379> set name omar EX 5
OK
```

If you want extra accuracy, you can pass `PX <milliseconds>` instead. For example `set name omar PX 2500`, will
set the value, and it's going to be removed after 2.5 seconds.

Keep on mind that `set` is only used for string values.

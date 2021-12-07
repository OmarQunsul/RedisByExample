# Strings - Let's get back to the basics

Strings are the simplest type of object that we can store in the Redis database. Each key simply
maps to another string value. Nothing fancy about. But it can be powerful than you might expect.

## Using the Redis-CLI tool to set some string values

Let's say that we want to use the Key/Value store to build a mapping of several countries to their capitals. Starting with 
an empty Redis database, we can issue several commands to set these values.

To set string values, we are going to use the [set](https://redis.io/commands/set) command.

For this example, let's use [redis-cli](https://redis.io/topics/rediscli), which is a simple 
command line program that comes with Redis, to connect and experiment with the Redis Server.

`redis-cli` connects to redis, as if it's any other program. It takes the commands 
from the user via the standard input, and sends them to the redis server. Then it prints out the response from each command.

```
$ redis-cli
127.0.0.1:6379> set Jordan Amman
OK
127.0.0.1:6379> set Germany Berlin
OK
127.0.0.1:6379> set Sweden Stockholm
OK
```

As we can see in the previous example, we have used the command set to add several country/capital key/value pairs. Nothing fancy so far. Let's 
stay inside the redis-cli tool, and issue several  commands to read the capitals of these countries. 
For this, we will use the command [get](https://redis.io/commands/get):

```
127.0.0.1:6379> get Jordan
"Amman"
127.0.0.1:6379> get jordan
(nil)
127.0.0.1:6379> get Germany
"Berlin"
127.0.0.1:6379> get Sweden
"Stockholm"
127.0.0.1:6379> get Japan
(nil)
```

As you notice here, sending the get command against a key that doesn't exist, will return an empty value (nil). Which is different from an empty string. If we send the command (type) with the argument (Japan), we should get "none".

Also from the 2nd example, you can notice that the keys are case sensitive. so "Jordan" is different from the key "jordan".
Building a Counter using Strings Values

As simple as they seem, strings are more powerful than you can imagine. They can cover many use cases in real life applications. 

Let's say we have a simple website that is written in [Ruby](https://www.ruby-lang.org/) / [Sinatra](http://sinatrarb.com/). To figure out how to install 
Ruby and Sinatra, please refer to our appendices at the end of the tutorial.

This small webserver app needs to serve several pages. Imagine that you are required to count the number of views per page. To achieve this, we
are going to use Redis for this purpose.
This is how your Sintra Application look like.

```
require 'sinatra'
require 'redis'

redis = Redis.new() # Initializing a Redis Client

get '/pages/:name' do
   page_name = params['name']
   page_counter_key = "page_counter:${page_name}"
   counter = redis.incr(page_counter_key)
   "Hello to the page ${page_name}. This page has been visited ${counter} time(s)."
end
```

## Bonus: Cleaning up the Database

Let's say that we want to clean up the whole database, and start over. For this,
we can use the command [flushdb](https://redis.io/commands/flushdb) that takes no arguments.
It simply cleans up the whole database. Running `dbsize` immediately after `flushdb` will definitely
gives you `0`.

![redis.token](./redis-token-banner.png)
[![Build Status](https://travis-ci.org/ChrisCates/redis.token.svg?branch=master)](https://travis-ci.org/ChrisCates/redis.token)
[![Coverage Status](https://coveralls.io/repos/github/ChrisCates/redis.token/badge.svg?branch=master)](https://coveralls.io/github/ChrisCates/redis.token?branch=master)
![Codeship](https://codeship.com/projects/a6d7def0-ecd3-0133-6c4f-5aad4fd90081/status?branch=master)
[![Build status](https://ci.appveyor.com/api/projects/status/vbpwefi8ot45rl2c?svg=true)](https://ci.appveyor.com/project/ChrisCates/redis-token)

[![NPM](https://nodei.co/npm/redis.token.png)](https://nodei.co/npm/redis.token/)

# redis.token
## A token based storage system in Redis that uses hashtables.
### By Chris Cates :star:

### Installation
```
npm install redis.token --save
```

### Usage

This NPM module automatically converts key value objects into hash tables.
The `Redis.GET` command automatically returns an object in the `redis` npm module.

Two dependencies for this project is (NPM):

```
crypto-js
redis
```

### Demo

```
var config = {
  host: "localhost",
  port: 6379,
  path: null,
  url: null,
  //etc (refer to redis npm docs for full configuration)
}


var redis = require("redis.token")(config, function(err) {
  if (err) throw err
})

redis.generate(
  {
    "key": "value",
    "key2": "value"
  },
  function(err, key) {
    if (err) throw err
    //Returns randomly generated SHA3 token
    console.log(key)
    redis.get(key.token, function(err, reply) {
      if (err) throw err
      /*
      Returns
      {
        "key": "value",
        "key2": "value"
      }
      */
      console.log(reply)
    })
  }
)
```

### API

#### redis.token.generate(obj,callback)

Generates a hashtable with the key values in `obj`, callback returns a token.

#### redis.token.get(token,callback)

With the token generated in `.generate()` you can retrieve the object stored.

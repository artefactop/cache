cache
-----

In memory simple cache using ETS tables

## index ##

* [quickstart](#quickstart)
* [usage](#usage)
  - [simple usage](#simple-usage)
  - [otp behavior](#otp-behavior)
* [exports](#exports)
  - [`i/0,1`](#i)
  - [`put/2,3`](#put)
  - [`put_ttl/3,4`](#put_ttl)
  - [`get/1,2`](#get)
  - [`evict/0,1`](#evict)
  - [`stop/0,1`](#stop)

- - - 

## quickstart ##

#### to build the library and run tests ####

```bash
$ rebar compile
$ rebar eunit
```

## Usage

### Simple usage

```erlang
1> cache:start().
2> Key = key.
key
3> Value = value.
value
4> cache:put(Key, Value).
ok
5> cache:get(Key).
{ok, value}
```

If you want use more than one cache backet just add the name as atom at first.

```erlang
1> cache:start().
2> cache:start_link(test, []).
3> Key = key.
key
4> Value = value.
value
5> cache:put(test, Key, Value).
ok
6> cache:get(test, Key).
{ok, value}
```

### Otp application

Configure cache at reltool and you don't have to start it manually, has its own supervisor. You have to do all calls without cache Name.

## exports ##


#### `i/01`

```erlang
i() -> term()
i(Name) -> term()

  Name = atom()
```

Obtein cache info

### `put/2,3`

```erlang
put(Key, Value) -> ok.
put(Name, Key, Value) -> ok.

  Name = atom()
  Key = term()
  Value = term()
```

Insert element at cache with default TTL

### `put_ttl/3,4`

```erlang
put_ttl(Key, Value, TTL) -> ok.
put_ttl(Name, Key, Value) -> ok.

  Name = atom()
  Key = term()
  Value = term()
  TTL = non_neg_integer() %% seconds
```

Insert element at cache with  TTL

### `get/1,2`

```erlang
get(Key) -> {ok,Value} | none.
put(Name, Key) -> {ok,Value} | none.

  Name = atom()
  Key = term()
  Value = term()
```

Get element from cache

### `evict/0,1`
### `stop/0,1`
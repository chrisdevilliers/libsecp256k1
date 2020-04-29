Erlang NIF C libsecp256k1
=========================
Erlang bindings for most of the [secp256k1 C library](https://github.com/bitcoin/secp256k1).
This repo has been forked from [exthereum/libsecp256k1](https://github.com/exthereum/libsecp256k1) with the aim of replacing the Elixir build tooling with [rebar3](https://www.rebar3.org/).

Dependencies
------------
In order to build this library you will need the following:
- `erlang`
- `rebar3`
- `make`
- `automake`
- `autoconf`
- `libtool`
- `libgmp10` and `libgmp-dev`

Installation
------------
Add a dependency for `libsecp256k1` in your `rebar.config` file:
```erlang
{deps, [
        {libsecp256k1, {git, "git@github.com:chrisdevilliers/libsecp256k1.git"}}
       ]}.
```

Building
--------

    $ rebar3 compile

Usage
-----

    $ rebar3 shell
    
    Eshell V10.3.5.10  (abort with ^G)
    1> Privkey = crypto:strong_rand_bytes(32).
    2> {ok, Pubkey} = libsecp256k1:ec_pubkey_create(Privkey, compressed).

Unit tests
----------

    $ rebar3 eunit

Known issues
------------
The NIF libsecp256k1:ec_seckey_verify/1 causes corruption of its argument.

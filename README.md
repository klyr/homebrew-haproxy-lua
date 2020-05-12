# homebrew-haproxy-lua
Long ago, one could install [HAProxy][1] with [Lua][2] suport on MacOS by doing
this:

```
brew install haproxy --with-lua
```

But then, everything changed when [this][3] happened.

We at Batterii want to use HAProxy with Lua in our development environment, and
most of our developers work on MacOS. We've been unable to find a tap to replace
what used to be in the homebrew core, so we're just going to make it ourselves.

This is pretty much the same Formula as the one in homebrew core, but with the
old conditional Lua dependency and compilation args put back in.

It does not have any bottles defined, so you'll be installing from source if you
use this. This is largely because I don't know how bottles work and don't really
have time to look into it at the moment. If you'd like to have them and have
a better idea of what you're doing than I do, feel free to contribute. :)


## Installation
```
brew tap batterii/haproxy-lua

brew install batterii/haproxy-lua/haproxy

brew services start haproxy
```

## Configuration
As with the core package, your configuration should go in
`HOMEBREW_PREFIX/etc/haproxy.cfg`, and any Lua files should go into that same
directory alongside it. This file will not exist when you first install, so
you'll need to create it yourself following the [manual][4].

Unless you installed Homebrew in an an usual way, your `HOMEBREW_PREFIX` should
be `/usr/local`. You can double check this by running `brew --prefix`.

If you change the config file, you can restart HAProxy to use it like so:

```
brew services restart haproxy
```

## A Note on Naming
We named the formula "haproxy," which is the same as the one in core. The
Homebrew docs recommend against doing this since it prevents packages with
shared names from being installed side-by-side. I honestly doubt, however, that
anybody will need to have a side-by-side install of HAProxy-- one with Lua and
one without. So the name is kept the same for convience and compatbility with
existing tooling.

[1]: http://www.haproxy.org/
[2]: https://www.lua.org/about.html
[3]: https://github.com/Homebrew/homebrew-core/issues/31510
[4]: http://cbonte.github.io/haproxy-dconv/2.2/configuration.html

# Miso TodoMVC

> Miso is a small, production-ready, isomorphic Haskell front-end framework for building highly interactive single-page web applications. It features a virtual-dom with diffing/patching, event delegation, event batching, SVG, Server-sent events, Websockets, type-safe servant-style routing, and an extensible Subscription/Effect system.

## Resources

- [Website](https://haskell-miso.org)
- [GitHub](https://github.com/haskell-miso/miso)
- [Hackage](https://hackage.haskell.org/package/miso)
- [Haddocks](https://haddocks.haskell-miso.org)
- [GitHub Discussions](https://github.com/haskell-miso/miso/discussions)

## Implementation

This app is written in Haskell and compiled to JavaScript using [GHC's JavaScript backend](https://www.haskell.org/ghc/). The architecture follows a strict unidirectional data flow modelled after Elm:

- **Model** — application state (todo entries, current input, active filter)
- **Msg** — all possible state transitions as an ADT
- **updateModel** — pure function that maps `(Msg, Model)` → `Effect Model Msg`
- **viewModel** — pure function that maps `Model` → virtual DOM

State is persisted to `localStorage` under the key `todos-miso`. Hash-based routing (`#/`, `#/active`, `#/completed`) is handled via Miso's URI subscription.

## Build

Install [Nix](https://nixos.org/download) with [Flakes enabled](https://nixos.wiki/wiki/Flakes), then:

```bash
npm run build
```

or

```bash
bun run build
```

This drops into a Nix devshell with GHC's JavaScript backend, builds via `cabal`, then optimises the output with `swc`.

## Credit

Created by [David M. Johnson](https://github.com/dmjio)

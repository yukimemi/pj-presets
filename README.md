# pj-presets

[kata](https://github.com/yukimemi/kata) **preset** definitions —
small bundles that name which template repos to compose for a given
project shape.

## Available presets

| Spec | Layers | Use for |
|---|---|---|
| `rust-cli.toml` | [`pj-base`](https://github.com/yukimemi/pj-base) + [`pj-rust`](https://github.com/yukimemi/pj-rust) + [`pj-rust-cli`](https://github.com/yukimemi/pj-rust-cli) | Rust **binary** crates (cross-compile + GitHub Release + crates.io publish) |
| `rust-lib.toml` | [`pj-base`](https://github.com/yukimemi/pj-base) + [`pj-rust`](https://github.com/yukimemi/pj-rust) + [`pj-rust-lib`](https://github.com/yukimemi/pj-rust-lib) | Rust **library** crates (crates.io publish + auto-generated GitHub release notes, no binaries) |

## Usage

```sh
# Phase 2+ (git fetch supported)
kata init github.com/yukimemi/pj-presets:rust-cli ./your-new-pj

# Phase 1 (local sources only) — point at a checkout of this repo
kata init ~/src/github.com/yukimemi/pj-presets/rust-cli.toml --at ./your-new-pj
```

## Why a separate `pj-presets` repo

So presets compose without bundling — `pj-base` doesn't need to
know about `pj-rust-cli`, and a Bun preset can later live next to
the Rust one without either touching the others.

## License

MIT.

# pj-presets

[kata](https://github.com/yukimemi/kata) **preset** definitions —
small bundles that name which template repos to compose for a given
project shape.

## Available presets

| Spec | Layers | Use for |
|---|---|---|
| `base.toml` | [`pj-base`](https://github.com/yukimemi/pj-base) | Language-agnostic boilerplate only (profile README, docs, config repos). |
| `rust-cli.toml` | [`pj-base`](https://github.com/yukimemi/pj-base) + [`pj-rust`](https://github.com/yukimemi/pj-rust) + [`pj-rust-cli`](https://github.com/yukimemi/pj-rust-cli) | Rust **binary** crates (cross-compile + GitHub Release + crates.io publish) |
| `rust-lib.toml` | [`pj-base`](https://github.com/yukimemi/pj-base) + [`pj-rust`](https://github.com/yukimemi/pj-rust) + [`pj-rust-lib`](https://github.com/yukimemi/pj-rust-lib) | Rust **library** crates (crates.io publish + auto-generated GitHub release notes, no binaries) |
| `rust-workspace.toml` | [`pj-base`](https://github.com/yukimemi/pj-base) + [`pj-rust`](https://github.com/yukimemi/pj-rust) + [`pj-rust-workspace`](https://github.com/yukimemi/pj-rust-workspace) | Rust **workspace** root with `crates/<name>/` members (workspace skeleton + cargo-make recursion off). Apply `rust-cli` / `rust-lib` per-member as needed. |
| `denops.toml` | [`pj-base`](https://github.com/yukimemi/pj-base) + [`pj-denops`](https://github.com/yukimemi/pj-denops) | **Denops plugins** (3 OS test matrix + automerge pipeline). Two layers only — Deno is compiled/interpreted at runtime, so there is no toolchain/build layer between them. Automerges minor/patch/deno/ GHA deps via Renovate's platform automerge + the label-based `pascalgn/automerge-action` pipeline. |
| `nvim.toml` | [`pj-base`](https://github.com/yukimemi/pj-base) + [`pj-nvim`](https://github.com/yukimemi/pj-nvim) | **Neovim plugins** (3 OS x nvim stable/nightly test matrix + stylua lint). Two layers only — Lua is interpreted, so there is no toolchain/build layer between them. Pick the test framework with `nvim.test_runner` (`"mini"` / `"plenary"`) in `.kata/vars.toml`. |
| `web-react.toml` | [`pj-base`](https://github.com/yukimemi/pj-base) + [`pj-pnpm`](https://github.com/yukimemi/pj-pnpm) + [`pj-react-web`](https://github.com/yukimemi/pj-react-web) | Vite + React + TS + Tailwind SPA (no Firebase; host on GH Pages / Cloudflare / S3 / etc.) |
| `web-react-firebase.toml` | [`pj-base`](https://github.com/yukimemi/pj-base) + [`pj-pnpm`](https://github.com/yukimemi/pj-pnpm) + [`pj-react-web`](https://github.com/yukimemi/pj-react-web) + [`pj-firebase`](https://github.com/yukimemi/pj-firebase) | Vite + React SPA with Firebase Hosting + Firestore + Storage + Vercel mirror (the [`kakeizu`](https://github.com/yukimemi/kakeizu) shape) |

## Usage

```sh
# Bootstrap from a preset — kata fetches templates from GitHub
kata init github.com/yukimemi/pj-presets:rust-cli
```

## Why a separate `pj-presets` repo

So presets compose without bundling — `pj-base` doesn't need to
know about `pj-rust-cli`, and a Bun preset can later live next to
the Rust one without either touching the others.

## License

MIT.

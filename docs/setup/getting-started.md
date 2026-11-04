# Getting started

How to build the CLI and configure it, as far as it works today. Everything here is for commit `ed795ea` of `ga4gh/ga4gh-sdk`, the state of `main` on 2026-11-04. The issues on the [plan](../plan/index.md) change much of it.

## What has been run, and what hasn't

!!! warning "Only against a local mock"
    **Run on 2026-11-04,** with Rust 1.99.1 on Ubuntu 26.04: the commands on this page, and `tes create`, `list`, `status`, `get` and `cancel` against a small local mock server without authentication.

    **Not run:** a real proTES, a real WES, Funnel, a real LS Login token, macOS or Windows. `GA4GH_TOKEN` doesn't exist yet.

## Requirements

- Git.
- Rust, for instance through [rustup](https://rustup.rs/). The repository doesn't pin a version yet ([#86](https://github.com/ga4gh/ga4gh-sdk/issues/86)).
- A C toolchain and the OpenSSL headers, as the HTTP client uses native TLS. On Debian or Ubuntu: `libssl-dev`.
- `python3` was on the path during the runs above, as the workspace also has Python bindings. Whether the build needs it wasn't checked.

## Build

```sh
git clone https://github.com/ga4gh/ga4gh-sdk.git
cd ga4gh-sdk
cargo build
./target/debug/cli --version
```

It ends with `ga4gh-cli 0.1.0`.

- Build the whole workspace, as above. `cargo build -p ga4gh-cli` fails with `E0433` at this commit, and `cargo install --path cli` is reported to fail in the same way ([#79](https://github.com/ga4gh/ga4gh-sdk/issues/79)).
- The binary is called `cli`, although the docs say `ga4gh-cli` ([#79](https://github.com/ga4gh/ga4gh-sdk/issues/79)). Below, `cli` stands for `./target/debug/cli`.

To check the build, run the tests. This passes with 27 unit tests and 6 doctests; the tests against Funnel and WES are opt-in, and run nothing here.

```sh
cargo test --workspace --exclude ga4gh
```

## Configure

The CLI reads `~/.ga4gh-cli/config.json`. This path is fixed.

```json
{
  "TES": {
    "base_path": "http://localhost:8000",
    "basic_auth": null,
    "oauth_access_token": null
  }
}
```

- Both auth keys must be there, or the CLI panics ([#82](https://github.com/ga4gh/ga4gh-sdk/issues/82)). Leave them at `null`: they aren't sent to the server at this commit ([#31](https://github.com/ga4gh/ga4gh-sdk/issues/31)).
- If the file is missing, the CLI targets `http://localhost` rather than failing ([#82](https://github.com/ga4gh/ga4gh-sdk/issues/82)).
- `base_path` can't have a path yet: with `https://host/ga4gh/tes/v1`, the requests go to `https://host/service-info` and `https://host/tasks` ([#80](https://github.com/ga4gh/ga4gh-sdk/issues/80)). So services that serve the API only under a prefix, such as proTES, don't work yet.

## Run

The server needs to serve `/service-info` with `type.artifact` set to `tes`. Save a task as `hello.json`:

```json
{
  "name": "hello",
  "executors": [{"image": "alpine", "command": ["echo", "hello"]}]
}
```

Then:

```sh
cli tes create hello.json
cli tes list
cli tes status <id>
cli tes get <id> FULL
cli tes cancel <id>
```

Their output isn't made for scripts, and `create`, `get` and `list` exit with 0 on server errors ([#83](https://github.com/ga4gh/ga4gh-sdk/issues/83)). `tes create` takes only a file at this commit ([#84](https://github.com/ga4gh/ga4gh-sdk/issues/84)).

## Token

`GA4GH_TOKEN` is how the CLI will get its token, once [#31](https://github.com/ga4gh/ga4gh-sdk/issues/31) is merged:

```sh
export GA4GH_TOKEN=<token>
```

**At this commit it has no effect:** on the mock, requests carried no `Authorization` header with the variable set.

Not known yet, and to be added here when it is:

- How to get an LS Login token at the event, and for which client. There's no login in the CLI ([#90](https://github.com/ga4gh/ga4gh-sdk/issues/90)).
- The address of the proTES instance for the [acceptance test](../plan/acceptance.md). It's given out on site, and doesn't go into these docs.

Keep tokens in the environment, and out of files, issues, pull requests and this repository.

## Contribute

- Pick an issue from [Tiers and issues](../plan/tiers.md), following the [order](../plan/index.md#order), and say on the [board](https://github.com/orgs/elixir-cloud-aai/projects/28) or the issue that you're on it.
- Pull requests go to `main` of `ga4gh/ga4gh-sdk`, close their issue, and include tests and the docs they affect.
- Commit messages follow [Conventional Commits](https://www.conventionalcommits.org/).
- Who reviews and merges during the event is an [open question](../outcomes/open-questions.md).

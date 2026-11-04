# Acceptance test

This is what "done at the event" means. Run it on a clean machine, with a released binary or one from `cargo install --locked`, against the deployed proTES, with a real LS Login token. Record the outcome in [Results](../outcomes/results.md).

!!! note "None of this passes yet"
    It describes the state after the work. Several commands and flags only exist once the issues named in [Tiers and issues](tiers.md) are merged, for instance the binary name ([#79](https://github.com/ga4gh/ga4gh-sdk/issues/79)) and `GA4GH_TOKEN` ([#31](https://github.com/ga4gh/ga4gh-sdk/issues/31)).

## Must pass

1. `cargo install --path cli --locked` works, and `ga4gh-cli --version` runs.
2. A configuration with only `TES.base_path` set to `https://<host>/ga4gh/tes/v1`, and the token in `GA4GH_TOKEN`.
3. `ga4gh-cli tes create hello.json` prints a task ID, and exits with 0.
4. `tes status <id>` reaches `COMPLETE`, and `tes get <id> FULL` prints JSON with logs.
5. `tes list` shows the task. A tag filter finds it, and excludes others.
6. `tes create` of a long task, then `tes cancel <id>`: the state becomes `CANCELING` or `CANCELED`.
7. These cases exit non-zero with a clear message: no token (401), an invalid token, an unknown task ID (404), a wrong `base_path`, and no configuration.
8. CI is green on `main`, and the pull requests of the event are merged.

## Extensibility

Nothing needs to ship for these, but they should hold ([Extensibility](extensibility.md)):

- A crate outside the repository builds against the library.
- `tes get` keeps a field the model doesn't know.
- `cli/src/lib.rs` exists, and a test adds a subcommand.
- `models/` has no hand edit without a patch.

## Stretch goal: WES

The same steps with `wes create`, then `list`, `status`, `logs` and `cancel`, against Conquest if it's reachable.

## Nice to have

- `registry list --type tes` lists the TES instances from a Service Registry.
- A `trs` and a `drs` lookup.
- A tagged prerelease with binaries (see [#77](https://github.com/ga4gh/ga4gh-sdk/issues/77) and [#91](https://github.com/ga4gh/ga4gh-sdk/issues/91)).

# Tiers and issues

Each table is in working order. "Blocked by" lists what's recorded as a dependency on the issue. Each issue has its expected result and how to test it, so start there.

## Tier A: fundamental fixes

| Issue | What | Blocked by |
|---|---|---|
| [#79](https://github.com/ga4gh/ga4gh-sdk/issues/79) | The CLI and the library build on their own, also as a dependency of another crate. The binary is `ga4gh-cli` | |
| [#81](https://github.com/ga4gh/ga4gh-sdk/issues/81) | CLI commands move into a library, with one module per service and no change in behaviour. Comes before [#82](https://github.com/ga4gh/ga4gh-sdk/issues/82) and [#83](https://github.com/ga4gh/ga4gh-sdk/issues/83), which would otherwise grow `main()` | [#79](https://github.com/ga4gh/ga4gh-sdk/issues/79) |
| [#82](https://github.com/ga4gh/ga4gh-sdk/issues/82) | Errors instead of panics on user input. Only `base_path` is required in the configuration | [#79](https://github.com/ga4gh/ga4gh-sdk/issues/79), [#81](https://github.com/ga4gh/ga4gh-sdk/issues/81) |
| [#80](https://github.com/ga4gh/ga4gh-sdk/issues/80) | `base_path` is the API root for every client, so a service behind a path prefix works. `TES::check` reports the cause of a failure | |
| [#31](https://github.com/ga4gh/ga4gh-sdk/issues/31) | Configured tokens and Basic credentials go into requests, to the origin of `base_path` only. `GA4GH_TOKEN` overrides the configuration | [#80](https://github.com/ga4gh/ga4gh-sdk/issues/80) |

## Tier B: critical path for the event

| Issue | What | Blocked by |
|---|---|---|
| [#83](https://github.com/ga4gh/ga4gh-sdk/issues/83) | Exit codes and error messages scripts can rely on. `tes get` prints the server's JSON unchanged. Closes [#46](https://github.com/ga4gh/ga4gh-sdk/issues/46) | [#81](https://github.com/ga4gh/ga4gh-sdk/issues/81), [#82](https://github.com/ga4gh/ga4gh-sdk/issues/82) |
| [#84](https://github.com/ga4gh/ga4gh-sdk/issues/84) | `tes create` takes a file, inline JSON or stdin. `tes list` filters by tag and shows the page token | [#83](https://github.com/ga4gh/ga4gh-sdk/issues/83) |
| [#5](https://github.com/ga4gh/ga4gh-sdk/issues/5) | CLI tests that run the binary against a mock, and a script that runs the whole cycle against proTES with a test token. Contributes to [#15](https://github.com/ga4gh/ga4gh-sdk/issues/15) | [#79](https://github.com/ga4gh/ga4gh-sdk/issues/79), [#80](https://github.com/ga4gh/ga4gh-sdk/issues/80), [#31](https://github.com/ga4gh/ga4gh-sdk/issues/31), [#83](https://github.com/ga4gh/ga4gh-sdk/issues/83) |
| [#51](https://github.com/ga4gh/ga4gh-sdk/issues/51) | `wes create`, `list`, `status`, `get`, `logs`, `outputs` and `cancel` | [#79](https://github.com/ga4gh/ga4gh-sdk/issues/79), [#31](https://github.com/ga4gh/ga4gh-sdk/issues/31), [#83](https://github.com/ga4gh/ga4gh-sdk/issues/83) |
| [#85](https://github.com/ga4gh/ga4gh-sdk/issues/85) | WES models move to 1.1, with the task endpoints. Regenerating models becomes repeatable. Sub-issue of [#48](https://github.com/ga4gh/ga4gh-sdk/issues/48) | CLI part only: [#51](https://github.com/ga4gh/ga4gh-sdk/issues/51) |

## Tier C: nice to haves

### Target

Cheap, and they help everything else, so they run first ([Order](index.md#order)).

| Issue | What | Blocked by |
|---|---|---|
| [#93](https://github.com/ga4gh/ga4gh-sdk/issues/93) | `AGENTS.md`, with the commands and rules of the repository | |
| [#86](https://github.com/ga4gh/ga4gh-sdk/issues/86) | `ci.yml` with a gate job, after one commit that only runs `cargo fmt`. Sub-issue of [#32](https://github.com/ga4gh/ga4gh-sdk/issues/32); closes [#17](https://github.com/ga4gh/ga4gh-sdk/issues/17), [#45](https://github.com/ga4gh/ga4gh-sdk/issues/45) and [#44](https://github.com/ga4gh/ga4gh-sdk/issues/44) | |
| [#88](https://github.com/ga4gh/ga4gh-sdk/issues/88) | `Cargo.lock` committed, metadata fixed | [#79](https://github.com/ga4gh/ga4gh-sdk/issues/79) |
| [#92](https://github.com/ga4gh/ga4gh-sdk/issues/92) | Install and usage guides, together with [#53](https://github.com/ga4gh/ga4gh-sdk/issues/53) and [#16](https://github.com/ga4gh/ga4gh-sdk/issues/16). Best after [#51](https://github.com/ga4gh/ga4gh-sdk/issues/51) | |

### If time allows

| Issue | What | Blocked by |
|---|---|---|
| [#89](https://github.com/ga4gh/ga4gh-sdk/issues/89) | Service Registry client and commands, with the fields of the specification only | [#79](https://github.com/ga4gh/ga4gh-sdk/issues/79), [#80](https://github.com/ga4gh/ga4gh-sdk/issues/80), [#83](https://github.com/ga4gh/ga4gh-sdk/issues/83) |
| [#61](https://github.com/ga4gh/ga4gh-sdk/issues/61) | TRS client in the library | [#80](https://github.com/ga4gh/ga4gh-sdk/issues/80) |
| [#62](https://github.com/ga4gh/ga4gh-sdk/issues/62) | TRS commands | [#61](https://github.com/ga4gh/ga4gh-sdk/issues/61), [#83](https://github.com/ga4gh/ga4gh-sdk/issues/83) |
| [#57](https://github.com/ga4gh/ga4gh-sdk/issues/57) | DRS commands | [#80](https://github.com/ga4gh/ga4gh-sdk/issues/80), [#83](https://github.com/ga4gh/ga4gh-sdk/issues/83) |
| [#91](https://github.com/ga4gh/ga4gh-sdk/issues/91) | CLI binaries on version tags, as a draft prerelease. Sub-issue of [#8](https://github.com/ga4gh/ga4gh-sdk/issues/8) | [#79](https://github.com/ga4gh/ga4gh-sdk/issues/79), [#86](https://github.com/ga4gh/ga4gh-sdk/issues/86), [#88](https://github.com/ga4gh/ga4gh-sdk/issues/88) |
| [#87](https://github.com/ga4gh/ga4gh-sdk/issues/87) | Coverage, pre-commit and repository templates. Sub-issue of [#32](https://github.com/ga4gh/ga4gh-sdk/issues/32) | [#86](https://github.com/ga4gh/ga4gh-sdk/issues/86) |
| [#90](https://github.com/ga4gh/ga4gh-sdk/issues/90) | Login with the OIDC device flow. Deferred | [#31](https://github.com/ga4gh/ga4gh-sdk/issues/31) |

## Tier D: extensibility

After the event, unless time is left. If so, take [#94](https://github.com/ga4gh/ga4gh-sdk/issues/94) first, as it guards everything else. The parent issue is [#78](https://github.com/ga4gh/ga4gh-sdk/issues/78), and [Extensibility](extensibility.md) explains the goal.

| Issue | What | Blocked by |
|---|---|---|
| [#94](https://github.com/ga4gh/ga4gh-sdk/issues/94) | Example crate in CI, using only public APIs, with a guide | [#79](https://github.com/ga4gh/ga4gh-sdk/issues/79), [#80](https://github.com/ga4gh/ga4gh-sdk/issues/80), [#81](https://github.com/ga4gh/ga4gh-sdk/issues/81) |
| [#95](https://github.com/ga4gh/ga4gh-sdk/issues/95) | Models keep unknown fields, and enums keep unknown values | [#85](https://github.com/ga4gh/ga4gh-sdk/issues/85) |
| [#96](https://github.com/ga4gh/ga4gh-sdk/issues/96) | Custom services in the configuration | [#82](https://github.com/ga4gh/ga4gh-sdk/issues/82) |
| [#97](https://github.com/ga4gh/ga4gh-sdk/issues/97) | Client methods generic over models | [#80](https://github.com/ga4gh/ga4gh-sdk/issues/80), [#83](https://github.com/ga4gh/ga4gh-sdk/issues/83) |
| [#98](https://github.com/ga4gh/ga4gh-sdk/issues/98) | Other binaries reuse and extend the CLI | [#81](https://github.com/ga4gh/ga4gh-sdk/issues/81), [#96](https://github.com/ga4gh/ga4gh-sdk/issues/96) |
| [#99](https://github.com/ga4gh/ga4gh-sdk/issues/99) | Python bindings can be subclassed | |
| [#100](https://github.com/ga4gh/ga4gh-sdk/issues/100) | A typed SDK error | [#83](https://github.com/ga4gh/ga4gh-sdk/issues/83) |

## Issues that look done

[#50](https://github.com/ga4gh/ga4gh-sdk/issues/50), [#55](https://github.com/ga4gh/ga4gh-sdk/issues/55), [#56](https://github.com/ga4gh/ga4gh-sdk/issues/56) and [#14](https://github.com/ga4gh/ga4gh-sdk/issues/14) look done, and [#43](https://github.com/ga4gh/ga4gh-sdk/issues/43) partly. Their comments have the evidence. They stay open until the maintainers of the SDK decide ([#77](https://github.com/ga4gh/ga4gh-sdk/issues/77)).

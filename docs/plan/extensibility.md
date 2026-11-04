# Extensibility

**Design goal:** downstream SDKs, for services with API extensions, can build on this SDK without forking. The parent issue is [#78](https://github.com/ga4gh/ga4gh-sdk/issues/78).

It needn't ship at the event, and [tier D](tiers.md#tier-d-extensibility) comes after it unless time is left. But no step of the work may make the goal harder to reach, so the issues of tiers A to C already lay the ground for it. Fixing this now is cheap: most of these changes are small before the CLI and transport work lands, and costly after.

## What a downstream crate should be able to do

1. Add API clients that share transport, auth and configuration.
2. Send and read fields beyond the specification, on existing models.
3. Add or extend CLI subcommands.
4. Do the same in Python.

Examples of such extensions are the additional endpoints of [proTES](https://github.com/elixir-cloud-aai/proTES/blob/dev/pro_tes/api/additions.openapi.yaml) and of [cloud-registry](https://github.com/elixir-cloud-aai/cloud-registry/blob/dev/cloud_registry/api/additions.openapi.yaml). Most of what they add is new endpoints, so the first point matters most.

This is about composition at compile time, and is separate from loading shared libraries at runtime ([#64](https://github.com/ga4gh/ga4gh-sdk/issues/64)).

## Where this stands

At commit `ed795ea`, from building a small crate against the library (details in [#78](https://github.com/ga4gh/ga4gh-sdk/issues/78)):

| Capability | Today | Issues |
|---|---|---|
| Build against the library | Fails, unless the crate enables `serde/derive` itself | [#79](https://github.com/ga4gh/ga4gh-sdk/issues/79) |
| New clients on the shared transport | Works by composition, but paths need absolute URLs, and there's no `PATCH` and no custom header | [#80](https://github.com/ga4gh/ga4gh-sdk/issues/80), [#31](https://github.com/ga4gh/ga4gh-sdk/issues/31), [#97](https://github.com/ga4gh/ga4gh-sdk/issues/97) |
| Custom services in the configuration | Sections are a closed enum | [#82](https://github.com/ga4gh/ga4gh-sdk/issues/82), [#96](https://github.com/ga4gh/ga4gh-sdk/issues/96) |
| Custom fields on models | Unknown fields are dropped, and an unknown enum value fails the whole response | [#83](https://github.com/ga4gh/ga4gh-sdk/issues/83), [#95](https://github.com/ga4gh/ga4gh-sdk/issues/95) |
| Regenerating models | Removes hand edits | [#85](https://github.com/ga4gh/ga4gh-sdk/issues/85) |
| CLI subcommands | The CLI is a binary only | [#81](https://github.com/ga4gh/ga4gh-sdk/issues/81), [#98](https://github.com/ga4gh/ga4gh-sdk/issues/98) |
| Python | Classes can't be subclassed | [#99](https://github.com/ga4gh/ga4gh-sdk/issues/99) |

## What the planned issues do for it

When you work on one of these, keep this part of its scope:

| Issue | Keep |
|---|---|
| [#79](https://github.com/ga4gh/ga4gh-sdk/issues/79) | Its test adds a throwaway crate outside the workspace |
| [#80](https://github.com/ga4gh/ga4gh-sdk/issues/80) | `endpoint()` and `urlencode` are public |
| [#31](https://github.com/ga4gh/ga4gh-sdk/issues/31) | One public `Transport::request_builder`, which everything goes through |
| [#82](https://github.com/ga4gh/ga4gh-sdk/issues/82) | A public `Configuration::from_path(path, section)` |
| [#81](https://github.com/ga4gh/ga4gh-sdk/issues/81) | A CLI library, with public `command()` and `run()` per service |
| [#83](https://github.com/ga4gh/ga4gh-sdk/issues/83) | A public `HttpError`, and `tes get` prints the server's JSON unchanged |
| [#84](https://github.com/ga4gh/ga4gh-sdk/issues/84) | Repeated query parameters in `Transport`, not only in the TES client |
| [#51](https://github.com/ga4gh/ga4gh-sdk/issues/51) | `cli/src/wes.rs` with public `command()` and `run()`, and `wes get` prints the server's JSON |
| [#85](https://github.com/ga4gh/ga4gh-sdk/issues/85) | Hand edits as patches applied by the script, and the module path as an argument of `build_models.sh` |
| [#89](https://github.com/ga4gh/ga4gh-sdk/issues/89) | Only the fields of the specification: what one implementation adds belongs in a downstream crate |
| [#93](https://github.com/ga4gh/ga4gh-sdk/issues/93) | The rule of no hand edits in generated models |

[#64](https://github.com/ga4gh/ga4gh-sdk/issues/64) changes `Transport` and `Configuration` too, and its branch `feat/extension-manager` overlaps with [#80](https://github.com/ga4gh/ga4gh-sdk/issues/80), [#31](https://github.com/ga4gh/ga4gh-sdk/issues/31) and [#82](https://github.com/ga4gh/ga4gh-sdk/issues/82), so coordinate there.

# Session plan

A proposal for the event, by session and not by the clock: move on when a session's exit check holds, and adapt it on site. [Order](../plan/index.md#order) says what can run in parallel.

## Session 1: start

- Go through the [goal](../index.md#goal) and the [acceptance test](../plan/acceptance.md).
- Settle the [open questions](../outcomes/open-questions.md), above all who reviews and merges.
- Everyone follows [Getting started](../setup/getting-started.md), and picks a lane on the [board](https://github.com/orgs/elixir-cloud-aai/projects/28).

**Exit check:** everyone has a working build and an issue.

## Session 2: gate and ground

- Setup lane: [#93](https://github.com/ga4gh/ga4gh-sdk/issues/93), then [#86](https://github.com/ga4gh/ga4gh-sdk/issues/86), starting with its `cargo fmt` commit, merged before other open work.
- Transport lane: [#80](https://github.com/ga4gh/ga4gh-sdk/issues/80), then [#31](https://github.com/ga4gh/ga4gh-sdk/issues/31).
- CLI lane: [#79](https://github.com/ga4gh/ga4gh-sdk/issues/79), then [#81](https://github.com/ga4gh/ga4gh-sdk/issues/81), then [#82](https://github.com/ga4gh/ga4gh-sdk/issues/82).
- Then [#88](https://github.com/ga4gh/ga4gh-sdk/issues/88).

**Exit check:** CI reports on pull requests, and a mock test shows the exact `Authorization` header on a request to a `base_path` with a prefix.

## Session 3: the task cycle

- [#83](https://github.com/ga4gh/ga4gh-sdk/issues/83), then [#84](https://github.com/ga4gh/ga4gh-sdk/issues/84).
- [#5](https://github.com/ga4gh/ga4gh-sdk/issues/5): CLI tests against the mock, and the script against [proTES in Compose](../setup/test-targets.md#protes-in-compose).

**Exit check:** create, status, get, list and cancel work against proTES in Compose with a test token, and fail if the `Authorization` header is removed.

## Session 4: acceptance

- Run the [acceptance test](../plan/acceptance.md) on a clean machine, against the deployed proTES, with a real LS Login token.
- Fix what it finds, and record each run in [Results](../outcomes/results.md).

**Exit check:** all steps under [Must pass](../plan/acceptance.md#must-pass) pass.

## Session 5: WES

- [#51](https://github.com/ga4gh/ga4gh-sdk/issues/51), and the library part of [#85](https://github.com/ga4gh/ga4gh-sdk/issues/85), then its CLI part.
- Test on the Starter Kit job. Test on Conquest if it's reachable, including how it spells `workflow_type`.

**Exit check:** the [stretch goal](../plan/acceptance.md#stretch-goal-wes) passes, or the results say what stopped it.

## Session 6: wrap up

- [#92](https://github.com/ga4gh/ga4gh-sdk/issues/92), with [#53](https://github.com/ga4gh/ga4gh-sdk/issues/53) and [#16](https://github.com/ga4gh/ga4gh-sdk/issues/16), so that the guides match what now works. Then update [Getting started](../setup/getting-started.md) here.
- If time is left: the rest of [tier C](../plan/tiers.md#tier-c-nice-to-haves), or [#94](https://github.com/ga4gh/ga4gh-sdk/issues/94) from tier D.
- Fill in [Results](../outcomes/results.md) and [Open questions](../outcomes/open-questions.md), and update the issues with what's left.
- Decide on a prerelease ([#77](https://github.com/ga4gh/ga4gh-sdk/issues/77), [#91](https://github.com/ga4gh/ga4gh-sdk/issues/91)), only after the acceptance test has passed.

**Exit check:** merged work is on the board as done, and all that's open has an issue.

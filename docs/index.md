# GA4GH SDK upgrade

A project at [BioHackathon Europe 2026](https://biohackathon-europe.org/). It asks for one thing above all: the CLI of the [GA4GH SDK](https://github.com/ga4gh/ga4gh-sdk) sends tasks to [proTES](https://github.com/elixir-cloud-aai/proTES) with an [LS Login](https://lifescience-ri.eu/ls-login/) token.

## Goal

- **Main goal:** the CLI creates, follows, lists and cancels TES tasks on a deployed proTES, with a real LS Login token. The [acceptance test](plan/acceptance.md) says exactly what that means.
- **Stretch goal:** the same for workflows through a WES, with [Conquest](https://github.com/anuragxxd/conquest) as the target if it's reachable at the event.
- **Design goal:** downstream SDKs can build on this one without forking. It needn't ship at the event, but no step of the work may make it harder. See [Extensibility](plan/extensibility.md).

## Status

!!! warning "The CLI can't reach proTES yet"
    As of 2026-11-04, `ga4gh/ga4gh-sdk` is at commit `ed795ea`, with the issues written and nothing of this plan merged. At that commit the CLI builds and works against a local mock without authentication. It sends no token ([#31](https://github.com/ga4gh/ga4gh-sdk/issues/31)) and drops the path of its base URL ([#80](https://github.com/ga4gh/ga4gh-sdk/issues/80)), so it can't talk to proTES. See [Getting started](setup/getting-started.md) for what has been run and what hasn't.

The [Results](outcomes/results.md) are empty until the event.

## Where work happens

- **Code, issues and pull requests:** [`ga4gh/ga4gh-sdk`](https://github.com/ga4gh/ga4gh-sdk), not here.
- **Tracking:** the [project board](https://github.com/orgs/elixir-cloud-aai/projects/28), "BioHackEU26: GA4GH-SDK Upgrade".
- **Questions for the maintainers of the SDK:** [#77](https://github.com/ga4gh/ga4gh-sdk/issues/77).
- **This repository:** the plan, the guide for participants and the results. Changes to these docs are welcome as [issues](https://github.com/elixir-cloud-aai/biohackeu26-ga4gh-sdk-upgrade/issues) or pull requests against `dev`.

## Reading paths

- **To join at the event:** [Getting started](setup/getting-started.md), then the [Session plan](event/session-plan.md), then pick an issue from [Tiers and issues](plan/tiers.md).
- **To see what's planned, and why in this order:** [Plan](plan/index.md).
- **To see when it counts as done:** [Acceptance test](plan/acceptance.md).
- **To build your own SDK on top of it:** [Extensibility](plan/extensibility.md).
- **To look something up:** [Test targets](setup/test-targets.md), [Glossary](about/glossary.md), [References](about/references.md).

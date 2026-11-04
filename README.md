# GA4GH SDK upgrade

Docs of a [BioHackathon Europe 2026](https://biohackathon-europe.org/) project. The goal: the CLI of the [GA4GH SDK](https://github.com/ga4gh/ga4gh-sdk) sends tasks to [proTES](https://github.com/elixir-cloud-aai/proTES) with an [LS Login](https://lifescience-ri.eu/ls-login/) token. Workflows to a WES are a stretch goal.

This repository holds only the docs. Code and issues are in [`ga4gh/ga4gh-sdk`](https://github.com/ga4gh/ga4gh-sdk), and the work is tracked on the [project board](https://github.com/orgs/elixir-cloud-aai/projects/28).

> [!WARNING]
> **The CLI can't reach proTES yet.** At the commit these docs describe, it sends no token, and drops the path of its base URL. Both are on the plan: see [Getting started](docs/setup/getting-started.md) for what has been run and what hasn't.

## Links

Docs are written for Read the Docs (MkDocs Material), and readable here as Markdown.

- [Home](docs/index.md)
- [Plan](docs/plan/index.md): order of the work, [tiers and issues](docs/plan/tiers.md), [acceptance test](docs/plan/acceptance.md) and [extensibility](docs/plan/extensibility.md)
- [Getting started](docs/setup/getting-started.md): build the CLI and configure it
- [Test targets](docs/setup/test-targets.md): what to test against, cheapest first
- [Session plan](docs/event/session-plan.md)
- [Open questions](docs/outcomes/open-questions.md) and [Results](docs/outcomes/results.md): results are empty until the event
- [About](docs/about/index.md)

Licence: [Apache-2.0](LICENSE).

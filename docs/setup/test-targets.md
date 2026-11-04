# Test targets

What to test against, cheapest first. Use the first one that can show what you're working on.

!!! warning "Not run with this CLI"
    Apart from a local mock, none of these has been run with the CLI yet. This list comes from the docs and code of each project, so expect some surprises, and correct this page when you find them.

1. **Mock, for every pull request.** `mockito` for the library, which it already uses. CLI tests run the binary against it ([#5](https://github.com/ga4gh/ga4gh-sdk/issues/5)). Assert `Authorization` headers exactly.
2. **Funnel, for TES without auth.** Real execution, and spec behaviour. The [CLI README](https://github.com/ga4gh/ga4gh-sdk/blob/main/cli/README.md) says that the Dockerized Funnel lacks service info at the expected path, so check which path your version serves.
3. **proTES in Compose, for TES with auth and no external account.** See the steps below.
4. **Deployed proTES with LS Login, for the final check.** The [acceptance test](../plan/acceptance.md). The instance is named once it's up. Tokens come only from the environment.
5. **WES.** The [Starter Kit job](https://github.com/ga4gh/ga4gh-sdk/blob/main/README.md#starter-kit-wes-docker-integration) exists, for WES 1.0.1, with known limits on listing, cancelling and attachments. Conquest needs Kubernetes and has no Compose setup, so use a deployed instance if there is one, rather than installing it at the event.
6. **Service Registry and TRS.** [cloud-registry](https://github.com/elixir-cloud-aai/cloud-registry) and [TRS-Filer](https://github.com/elixir-cloud-aai/trs-filer), each with Compose.
7. **A downstream crate.** The example crate of [#94](https://github.com/ga4gh/ga4gh-sdk/issues/94), when it exists.

## proTES in Compose

From a clone of [proTES](https://github.com/elixir-cloud-aai/proTES), on branch `dev`:

```sh
export COMPOSE_FILE=docker-compose.yaml:tests/smoke/compose.yaml
docker compose up -d --build --wait
```

This should give proTES at `http://localhost:8080/ga4gh/tes/v1`, with a fake TES backend and a fake identity provider.

- The token endpoint is reachable only inside the Compose network. [`tests/smoke/check.sh`](https://github.com/elixir-cloud-aai/proTES/blob/dev/tests/smoke/check.sh) shows how to fetch a token.
- Tasks finish without running real containers. For that, add a real backend such as Funnel to the configuration.
- The CLI can use this setup only after [#80](https://github.com/ga4gh/ga4gh-sdk/issues/80) and [#31](https://github.com/ga4gh/ga4gh-sdk/issues/31).

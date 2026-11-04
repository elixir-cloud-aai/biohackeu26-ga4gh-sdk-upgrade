# About

## Contact

For anything about the SDK, use the [issues of `ga4gh/ga4gh-sdk`](https://github.com/ga4gh/ga4gh-sdk/issues). For these docs, [open an issue](https://github.com/elixir-cloud-aai/biohackeu26-ga4gh-sdk-upgrade/issues) in this repository. For the services around it, see [ELIXIR On-Cloud](https://elixir-on.cloud/).

## Contributors

See the repository's [contributors](https://github.com/elixir-cloud-aai/biohackeu26-ga4gh-sdk-upgrade/graphs/contributors). Written with AI assistance, as the commits say.

## Citation

There's no citable release. To refer to these docs, give the repository's URL and the commit you used.

## License

[Apache-2.0](https://github.com/elixir-cloud-aai/biohackeu26-ga4gh-sdk-upgrade/blob/dev/LICENSE).

## Acknowledgements

The authors of the [GA4GH SDK](https://github.com/ga4gh/ga4gh-sdk), which this project works on.

## Contributing and development

Commit messages follow [Conventional Commits](https://www.conventionalcommits.org/), with a subject of at most 50 characters. CI builds the docs and runs the linters; the only required check is `CI passed`.

To build the docs:

```sh
python3 -m venv .venv && .venv/bin/pip install '.[docs]' && .venv/bin/mkdocs serve
```

# http-status-budget

Calculate a request failure ratio using an explicit server-error classification.

## Run

Python 3.8 or later; no third-party packages or cloud credentials are required.

```sh
python3 tool.py examples/input.json
cat examples/input.json | python3 tool.py -
python3 -m unittest -v
```

## Example

Input:

```json
{
  "statuses": [
    200,
    200,
    404,
    503
  ]
}
```

Result:

```json
{
  "requests": 4,
  "server_errors": 1,
  "server_error_percent": 25.0
}
```

The command writes JSON to standard output. Exit 0 means evaluation completed;
a finding in the output may still require attention. Invalid input returns exit 2,
with an error on standard error and no result on standard output.

## Operational scope

Counts only 5xx as failures; service-specific availability may classify timeouts and some 4xx differently.

The tool evaluates supplied data locally. It does not change hosts, deploy
resources, or establish production compliance. Example identifiers and observations
are test fixtures. Keep credentials and private inventory out of Git.

## Design and verification

See [NOTES.md](NOTES.md) for the input contract, verification, and integration notes.
Related utilities: [nginx-upstream-checker](https://github.com/sal-s-root/nginx-upstream-checker), [tls-expiry-planner](https://github.com/sal-s-root/tls-expiry-planner).

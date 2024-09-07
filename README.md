# bun-diff-action

A composite action that writes the diff of bun.lock file into a comment of pull request.

## Requirements

- Running on `pull_request` event,
- Permission to `write` comments to the pull request,
- Check out with `fetch-depth: 0`,
- Install `bun`.

## Usage

```yaml
name: CI

on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

permissions:
  pull-requests: write # for comments in PRs

jobs:
  unitTest:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with: # required!
          fetch-depth: 0
      - name: Install bun
        uses: oven-sh/setup-bun@v2
        with:
          bun-version: latest
      - name: Show the bun lock diff
        if: github.event_name == 'pull_request' # only for this event
        uses: RobinTail/bun-diff-action@v... # set the version
```

# GitHub Actions specifics

## Minimal Node.js CI example
```yaml
name: CI
on:
  push:
    branches: [main]
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version-file: '.nvmrc'
          cache: 'npm'
      - run: npm ci
      - run: npm run lint
      - run: npm test
```

## Deploy gating
```yaml
  deploy:
    needs: test
    if: github.ref == 'refs/heads/main' && github.event_name == 'push'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: ./deploy.sh
        env:
          DEPLOY_TOKEN: ${{ secrets.DEPLOY_TOKEN }}
```
`needs: test` blocks deploy from running until the test job passes — always chain deploy behind test/build, never let it run independently.

## Caching without setup-node's built-in cache
For non-npm ecosystems, use `actions/cache@v4` explicitly, keyed on the lockfile hash:
```yaml
      - uses: actions/cache@v4
        with:
          path: ~/.cache/pip
          key: ${{ runner.os }}-pip-${{ hashFiles('requirements.txt') }}
```

## Fork PR secret restriction
`pull_request` events from forked repos do not have access to repository secrets, by GitHub's design (prevents secret exfiltration via a malicious PR). If deploy previews from forks are genuinely needed, use `pull_request_target` with extreme caution — it runs with the base repo's permissions against the PR's code, which is a known injection risk if not scoped carefully. Default to not supporting fork deploys unless the user specifically needs it and understands the tradeoff.

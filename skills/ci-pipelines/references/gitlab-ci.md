# GitLab CI specifics

## Minimal example
```yaml
stages: [install, test, deploy]

cache:
  key: ${CI_COMMIT_REF_SLUG}
  paths: [node_modules/]

install:
  stage: install
  script: npm ci

test:
  stage: test
  script:
    - npm run lint
    - npm test

deploy:
  stage: deploy
  script: ./deploy.sh
  rules:
    - if: '$CI_COMMIT_BRANCH == "main"'
  environment: production
```

## Key differences from GitHub Actions
- Stages are explicit and ordered (`stages:` list) rather than implied by job dependency graphs.
- `rules:` (preferred) or `only`/`except` (legacy) control when a job runs — use `rules` for new pipelines.
- Secrets live in **Settings → CI/CD → Variables**, referenced as plain `$VARIABLE_NAME` — mark sensitive ones "Protected" and "Masked" so they don't leak into logs or run on non-protected branches.
- `environment:` on a deploy job enables GitLab's deployment tracking/rollback UI — worth adding whenever a job actually deploys somewhere.

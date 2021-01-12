# pnpm-audit-playground

Test monorepo to debug pnpm audit issues.

## Reproduce 502 issues

The NPM registry is specified as we use a private NPM registry that doesn't support audit, it shouldn't make a difference for you.

```
pnpm install
cd app/pkg1
pnpm audit --registry=https://registry.npmjs.org --prod
```

Output:

```
 WARN  post https://registry.npmjs.org/-/npm/v1/security/audits error (502). Will retry in 10 seconds. 2 retries left.
```

The issue comes from this file: `packages/pkg1/app/package.json`, and more specifically this dependency:

```
{
  "dependencies": {
    "react-scripts": "3.4.3"
```

Note that this issue does not happen in a single repo, it seems to only happen in a monorepo.

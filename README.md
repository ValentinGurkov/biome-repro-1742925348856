Running `check` for a monorepo project in `2.0.0-beta.1` reports errors for ignored files.

How to reproduce:

1. On the main branch run:
```
pnpm i
cd packages/package-a/
pnpm build
pnpm check
```

The report should only include errors for `src/index.ts`.

2. Then checkout the branch `2.0.0-beta.1`.
Run:
```
pnpm i
pnpm check
```

The diagnostics also report errors for `build/src/index.js` related to the rule `noUnusedVariables`.

This regression could be related to how the `.gitignore` file is handled, the reworked rule `noUnusedVariables`, or the new multi-file analysis feature that the reworked rule is based on.
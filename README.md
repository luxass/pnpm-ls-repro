# pnpm ls Parseable Output Issue

## Problem Description

There's an inconsistency in how `pnpm ls` behaves with the `--parseable` flag when listing production dependencies.

### Expected Behavior
- `pnpm ls --prod` correctly shows only production dependencies
- Should not show development dependencies like `eslint` when using `--parseable` flag

### Actual Behavior
- `pnpm ls --prod` works correctly
- `pnpm ls --prod --parseable` incorrectly shows `eslint-visitor-keys` which is a dependency from `eslint`

## Steps to Reproduce

1. Have a project with the following dependencies:
```json
{
  "dependencies": {
    "@babel/parser": "^7.26.3"
  },
  "devDependencies": {
    "eslint": "^9.16.0"
  }
}

2. Run `pnpm ls --prod --parseable`
3. Notice that `eslint-visitor-keys` is listed as a dependency
4. Run `pnpm ls --prod`
5. Notice that `eslint-visitor-keys` is not listed as a dependency
6. Run `pnpm why eslint-visitor-keys` and notice that it is a dependency of `eslint`
7. Run `pnpm why eslint-visitor-keys --prod` and notice that is no longer showed



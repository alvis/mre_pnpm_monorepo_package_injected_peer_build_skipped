# MRE for Skipped Builds in pnpm Monorepo with Injected Peer Dependencies

This Minimal Reproducible Example (MRE) demonstrates an issue within a pnpm monorepo where setting `shared-workspace-lockfile=false` causes builds for package-injected dependencies to be skipped.

For more details, refer to these issues:
* [pnpm issue #6976](https://github.com/pnpm/pnpm/issues/6976)
* [pnpm issue #7811](https://github.com/pnpm/pnpm/issues/7811)

## Steps to Reproduce

1. Execute `pnpm install` in the root directory.
2. Observe the error due to the absence of the built artifact from the `peer` package.

## Expected Behavior

The `peer` package's prepare script should run prior to that of the `subpackage`, ensuring all necessary artifacts are available.

## Actual Behavior

Without `shared-workspace-lockfile=false`, the `peer` package's prepare script runs as expected, allowing the `subpackage` to build successfully. However, enabling `shared-workspace-lockfile=false` results in the prepare script of the `peer` package being skipped, leading to a build failure in the `subpackage`.

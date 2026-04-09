# Tests CI

## Workflows

### Automated versions

The package version follows the [semantic versioning](https://semver.org/) scheme (`<major>.<minor>.<patch>-dev.<dev_version>`), and is automatically bumped on any closed PR to either `dev` or `main` branches. The version bumping is handled by the [bump2version](https://github.com/c4urself/bump2version) tool, and the workflow is defined in the `.github/workflows/ci-version.yml` file.

On any closed PR to `dev`, the version of the package will be automatically bumped to the next dev version. For example, if the current version is `0.1.0`, it will be bumped to `0.1.0-dev.1`.

On any closed PR to `main`, the version of the package will be automatically bumped to the next release version depending on the bump type specified in the PR tags (one of `bump:patch`, `bump:minor`, or `bump:major`). For example, if the current version is `0.1.0` and the PR is tagged with `bump:minor`, it will be bumped to `0.2.0`. A tag will also be created for the new version, and a release will be published on GitHub.

> [!NOTE]
> A workflow is also triggered on any PR to `main` to ensure exactly one of the bump type tags is present. If not, the workflow will fail and the PR cannot be merged until the issue is resolved.

After any PR merged to main, the main branch will be automatically merged back to dev to ensure the dev branch is up to date with the latest release. 

> [!TIP]
> To avoid conflicts, ensure your dev branch is up to date with the latest main branch before submitting a PR.
> 
> If you need to resolve a conflict on the version numbers, please update the version number with the current version number in the target branch; the version will be automatically bumped to the next version after the PR is merged.
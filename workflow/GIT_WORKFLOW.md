<h1 align="center">
  <a title="Building financial tools for Canada's entrepreneurs" href="https://pillar.financial">
    <img alt="Pillar" width="200px" src="https://avatars.githubusercontent.com/u/86977965?s=200&v=4" />
    <br/>
  </a>
  Git workflow
</h1>

## At a glance

At Pillar, we've adopted the Continous Integration practice but using a safe approach of branching and merging back to main instead of committing directly.

This combination of strategies increases the number of integration to the main branch as often as possible but still supports the practice of peer-review and security checks before accepting the changes in the main branch.

The main point is to avoid long-lived branches reducing the number of integration conflicts and introduce small changes in the codebase.

<img src="./assets/ci.png" />

## Development

Developers working on a story must checkout from the latest commit on the default working branch (`develop`) into a feature branch.
See [naming conventions](https://github.com/getPillar/developer-values/blob/master/code/NAMING_STANDARDS.md#rules) for branch names. 


Once the feature is ready to be presented in a pull request it should be based on `develop`. See [pull requests](https://github.com/getPillar/developer-values/blob/master/workflow/CODE_REVIEW.md#opening-pull-requests) for standards.

Features not ready for production may still be merged, but should be disabled. This is taken from the trunk-based approach, with the goal of stimulating development pace.

The `develop` branch must be stable at all times, even if it includes disabled features. It represents, in essence or in reality, the staging environment for the company. Tests must be passing before new code can be added to it.

## Releases

When the team deems fit, to align with engineering or product roadmaps, a Pull Request from `develop` to `master` is created so that all the features introduced are reviewed. The `master` branch represents the production environment.

A merge on the `master` branch should trigger a pipeline that runs the tests again and then deploys into production.

## Hotfixes

With `master` often behind on the active `develop` branch, it is sometimes required to checkout from master to perform quick surgery.

For tracking and merge-back reasons, a long-lived branch, aptly named `hotfix`, is preferred over multiple hotfix-prefixed branches 

It is assumed that in order to merge the next `develop` version into master, the team will have to sync back any hotfixes applied in `master` first. So to avoid any dips in productivity, it is strongly recommended that those changes be synced in `develop` as soon as possible.~~

## Supporting Documentation

- [Martin Fowler's Continuous Integration](https://martinfowler.com/articles/continuousIntegration.html)
- [Dave Farley's Continous Integration](https://www.youtube.com/watch?v=jAtI5T4O1j0)

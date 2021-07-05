<h1 align="center">
  <a title="Building financial tools for Canada's entrepreneurs" href="https://pillar.financial">
    <img alt="Pillar" width="200px" src="https://avatars.githubusercontent.com/u/86977965?s=200&v=4" />
    <br/>
  </a>
  Dependency management
</h1>


## Less is more

The NPM ecosystem, while a wonder of modern technology and a human achievement of massive scale does have it's downsides.

NPM allows everyone to publish anything on it's registry. This means that package releases could include malicious or otherwise poor quality code, the effects of which can be desastrous. Even well-intentionned, renowned groups and individuals can fail sometimes, either due to [multipe factors](https://blog.acolyer.org/2019/09/30/small-world-with-high-risks/amp/) - either direct, or coming from one of the dependencies in their chain.

That said, one of the best strategies to limit potential pollution via bad dependencies is to not have them in the first place.

Javascript's standard library is now extremely powerful and established patterns are being optimized under the hood with each passing versions. You should seek to implement as much as you can with it.

Here's a sample list of "banned" libraries:

| Library :x: | Reason |
| --- | --- |
| lodash (global) | Massive library, specific lodash packages (like `lodash.set`) are preferred |
| ramda | Massive library which only provides a stylistic overlay, like lodash it is also overkill |
| continuation-local-storage | Messes with node internals to provide thread caching. Causes memory leaks, blows up GC, etc |
| jquery | large framework from the past, largely irrelevant |
| query-string | Can be replaced by node standard internal library `querystring` |
| request | deprecated |
| request-promise | deprecated |
| socket.io | Old, bloated, slow |
| mongoose | large orm-type library, ill-fits most projects' needs |


## How to vet

It can be hard to determine the quality of a package. You will want to look for:

- recent activity (is it maintained, are issues resolved, are pull requests merged)
- code quality (are there a lot of open issues, are there tests, code standards)
- popularity (is the community around it large, is there support, documentation)

To help you you may use:

- [https://npm.anvaka.com/](https://npm.anvaka.com/) To figure out the dependency tree, links and licenses
- [https://www.npmstats.com/](https://www.npmstats.com/) For popularity and release cycle
- [https://npmcompare.com/](https://npmcompare.com/) To score different packages against one another
- [https://bundlephobia.com/](https://bundlephobia.com/) To determine the bundle size of a library

As well as running `npm audit` or `yarn audit` frequently on your repositories to be notified of any ongoing security issues.

While we do not want to stop anyone from using a dependency they need in order to fill a specific need, we do have a list of preferred libraries that should be considered.

| Library :heavy_check_mark: | Description |
| --- | --- |
| express | router, web server |
| uuid | unique id generator |
| mongodb | standard mongo client |
| jest | testing framework |
| typescript | Tyescript language transpiler |
| ts-node | Typescript language runtime |
| config | Environement based config manager |
| eslint | js / ts code linter |
| husky | git hooks manager |

## Updating dependencies

Dependencies should be updated as frequently as possible.
This limits the change delta between upgrades.
A good tip is to check dependency versions for external modules used while working on a feature or bug.

Every time the version target is changed an `npm audit` / `yarn audit` should be performed to validate that the changes are safe.

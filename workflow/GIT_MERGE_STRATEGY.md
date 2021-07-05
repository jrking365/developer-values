<h1 align="center">
  <a title="Building financial tools for Canada's entrepreneurs" href="https://pillar.financial">
    <img alt="Pillar" width="200px" src="https://avatars.githubusercontent.com/u/86977965?s=200&v=4" />
    <br/>
  </a>
  Git Merge Strategy
</h1>

## Main Trunk Branches

Main trunk branches includes the following:
* master
* develop
* staging
* release

The merge strategy for these branches is to use the `Create a merge commit` strategy. This is the easy to maintain way
of merging into those branches. Please note that creating a `Pull Request` is still a requirement for merging two 
main trunk branches together.

This merge strategy will allow us to quickly view what are the main difference between two releases (by looking at 
commit messages between two merge commits).

## Work Branches

Work branches includes are branches that include 
* New feature
* Bug fix
* Hot fix

We aim to to keep a clean and lean git history on every repository. A git commit message in the main trunk(s) should
provide a quick and easy way to grasp what was modified. No merge commits or in-development commit message should be
added to the main truck(s) git history.

When you merge a `Pull Request` on Github, please use the `Squash and merge` option. 

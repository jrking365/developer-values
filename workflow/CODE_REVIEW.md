<h1 align="center">
  <a title="Building financial tools for Canada's entrepreneurs" href="https://pillar.financial">
    <img alt="Pillar" width="200px" src="https://avatars.githubusercontent.com/u/86977965?s=200&v=4" />
    <br/>
  </a>
  Code reviews
</h1>

## Opening Pull Requests

Pull requests allow teams to communicate intentions and perform quality checks on implementation.
This is why it is preferable to open a pull request **as soon as functionality is ready**. This prevents silo work where a dev could have been headed down an erroneous path.

A pull request title should include the tracking id of the corresponding ticket or type as well as a short description of the work. [See Naming Standards for more details](./getPillar/developer-values/blob/master/code/NAMING_STANDARDS.md)

The description of the pull request should be a filled-out PR template, provided by the project. Recommended sections include:

```
## Summary

A brief overview of this PR

**Ticket** : #000


## Changelist

- List of updates

## Breaking changes

- List of breaking updates

## Merge Checklist

 - [ ] Verified locally
 - [ ] Unit Tests added
 - [ ] Integration tests added
 - [ ] Unit tests pass locally
 - [ ] Integration tests pass locally
```

## Choosing a Reviewer

A pull request must be reviewed and **approved by at least 2 reviewers**. 

A great tip for choosing reviewers would be that you pick:

- the person(s) most likely to give you a hard time, be picky, ask tough questions
- the person(s) most comfortable with the project at hand

It is also recommended that you include someone from a different team or departement from time to time - even technical management.
This is a great way to perform a quick sanity check, ensure product alignment and foster knowledge sharing.


## Reviewing Code

When reviewing code, make sure that:

- Complex areas or processes that require more context are flagged
- Functionality is properly tested
- Documentation is updated

Outside of this, lint checks should take care of any objective criteria defined by your team. 
It is the bare minimum for a project to enforce linting on commit/push in order to ensure consistency.
A neat addition could be to add a `code-climate` tool to analyze cyclomatic complexity.

Code style is unique to each developer, approaches are subjective and may not be how you imagined the implementation.
Unless an implementation is arguably problematic, stylistic comments should be marked `NIT` for nitpicking and it would be 
up to the owner of the PR to address them or not. 

## Urgent fixes

Notwithstanding the guidelines above, some fixes may be urgent as they may block our users from getting their money or fellow employees from doing their jobs. In this case, the PR should start with **HOTFIX:**. You should tag the entire github group "Engineering" to maximise the # of reviewers and place a link to your PR in the #backend slack channel. Feel free to ping other developers as well.

If a hotfix PR is not reviewed in a reasonable amount of time, github admins may approve the PR directly with no further reviews, in particular during off hours.

## Resolve Etiquette

Blocking reviews should be resolved by their original authors.

Nitpicks should be responded to and not ignored. Once the conversation reaches a logical end, it can be resolved by either party.

Once a pull request meets all the required aforementioned criteria, it should be merged by the author based on the chosen git workflow.

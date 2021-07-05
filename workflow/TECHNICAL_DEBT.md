<h1 align="center">
  <a title="Building financial tools for Canada's entrepreneurs" href="https://pillar.financial">
    <img alt="Pillar" width="200px" src="https://avatars.githubusercontent.com/u/86977965?s=200&v=4" />
    <br/>
  </a>
  Technical Debt
</h1>

At Pillar, like all software companies, it happens that technical debt is introduced in the code base.
Like Game of Thrones' Lannister family, we always pay our debt!

## When Should We Address It?

### Small Technical Debt

Small technical can be most of the time identified and addressed while working on a task. A good approach to tackle 
it is:

1. Identify the problem.
1. Address it while working on your task. We recommend to isolate to technical debts changes in standalone Git commits 
   so reviewers can differentiate between tasks related changes and technical debt related changes.

### Large Technical Debt

Large technical debt implies bigger code changes and more complex deployment strategies. It requires planning 
beforehand. A good approach to tackle it is:

1. Identify the problem.
1. Document the problem.
1. Communicate with management/product team on what it is and why it should be addressed.
1. Management/product team will add this task to planning.

## Proper Strategy to Address Technical Debt

* Identify what is the scope of the technical debt you want to pay.
* Make sure the existing code is properly tested. Refactoring already tested code we allow to acknowledge more easily if
  your recent changes broke the current workflow of a feature. If no test exists, write them before you start 
  refactoring.
* Adopt a modular approach. Fix small chunk at the time. There is no shame in doing more than one refactor iteration.
* If your refactoring introduce breaking changes, make sure to prepare and apply a deployment strategy.

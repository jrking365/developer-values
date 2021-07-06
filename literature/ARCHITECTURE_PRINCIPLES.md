<h1 align="center">
  <a title="Building financial tools for Canada's entrepreneurs" href="https://pillar.financial">
    <img alt="Pillar" width="200px" src="https://avatars.githubusercontent.com/u/86977965?s=200&v=4" />
    <br/>
  </a>
  Architecture Principles
</h1>

## Keep it super simple

Avoid moving parts, use less dependencies, workers, CRONs, external processes, if it can be avoided

## Informed decisions

Avoid premature optimization, premature decoupling. monitor your outcome, run perf testing, make data-driven decisions

## Team-oriented

Is the code understandable and easy to survey, are there strange patterns or hidden logic/config. is knowledge shared (bus factor), hows the documentation, comments linting

## Know the risks

Is the code tested, is the environement controlled, replicable and reliable. is there ci/cd, code reviews

## You ain't gonna need it ([YAGNI](https://martinfowler.com/bliki/Yagni.html))

Don't build stuff until you need it.
Design and develop for ease of extension and contraction.

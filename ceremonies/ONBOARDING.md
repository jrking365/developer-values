<h1 align="center">
  <a title="Building financial tools for Canada's entrepreneurs" href="https://pillar.financial">
    <img alt="Pillar" width="200px" src="https://avatars.githubusercontent.com/u/86977965?s=200&v=4" />
    <br/>
  </a>
  Onboarding
</h1>

This is for general developer on-boarding to the bramble monorepo. Consult this in addition to project-specific READMEs.
The checklist can also be used for application owners to provision access in a standardized way.

## Checklist

1. Gain access to the following applications:
 - General: Gmail, Slack, Notion, company Google Drive, JIRA
 - GitHub (organization and team)
 - Figma
 - Retool
 - Postman
 - Lokalise

2. Clone the monorepo 

3. Create .env.development files where there are .env.sample
 - Ask an existing developer for their copies

4. Install the following tools
 - npm / yarn
 - docker, docker-compose 

### VSCode-specific

1. To enable format/lint on Save, have the following in your `settings.json`
```
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
}
```
2. Make sure the TS version is the same between the VSCode workspace and repo
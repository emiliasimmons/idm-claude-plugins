# idm-plugins

A Claude Code plugin marketplace that collects the plugins published across the [InstituteforDiseaseModeling](https://github.com/InstituteforDiseaseModeling) and [StarsimHub](https://github.com/StarsimHub) GitHub orgs. Each entry in [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json) points at a plugin in its source repo, pinned to a commit. Nothing is copied here.

## Install

```
/plugin marketplace add emiliasimmons/idm-claude-plugins
/plugin install calib@idm-plugins
```

The repository is `idm-claude-plugins`; the marketplace it publishes is `idm-plugins`, which is the name that goes after the `@` when installing.

Plugins install over your own git credentials. This repository is public, but `calib` and `idm-ra` come from private sources, so those two install only for people with read access to [calib-plugin](https://github.com/InstituteforDiseaseModeling/calib-plugin) and [idm-ra](https://github.com/InstituteforDiseaseModeling/idm-ra).

`calib-plugin` publishes its own marketplace, named `idm-marketplace`. Adding both offers `calib` twice, once from each.

## Plugins

| Plugin | Source | Skills |
|---|---|---|
| `calib` | [calib-plugin](https://github.com/InstituteforDiseaseModeling/calib-plugin) (private) | 15 |
| `idm-ra` | [idm-ra](https://github.com/InstituteforDiseaseModeling/idm-ra) (private) | 3 |
| `data-cataloging-ai` | [data-cataloging-ai](https://github.com/InstituteforDiseaseModeling/data-cataloging-ai) | 5 |
| `idm-standards` | [idm_standards/idm_standards_plugin](https://github.com/InstituteforDiseaseModeling/idm_standards/tree/main/idm_standards_plugin) | 10 |
| `experiment-dashboard` | [idm-agent-skills/experiment-dashboard](https://github.com/InstituteforDiseaseModeling/idm-agent-skills/tree/main/experiment-dashboard) | 2 |
| `idm-pkg-install` | [idm-agent-skills/idm-pkg-install](https://github.com/InstituteforDiseaseModeling/idm-agent-skills/tree/main/idm-pkg-install) | 1 |
| `python-code-reviewer` | [idm-agent-skills/python-code-reviewer](https://github.com/InstituteforDiseaseModeling/idm-agent-skills/tree/main/python-code-reviewer) | 1 |
| `python-code-fixer` | [idm-agent-skills/python-code-fixer](https://github.com/InstituteforDiseaseModeling/idm-agent-skills/tree/main/python-code-fixer) | 1 |
| `starsim-ai` | [starsim_ai/plugins/starsim](https://github.com/StarsimHub/starsim_ai/tree/main/plugins/starsim) | 24, plus MCP tools |
| `disease-modeling` | [starsim_ai/plugins/disease_modeling](https://github.com/StarsimHub/starsim_ai/tree/main/plugins/disease_modeling) | 7 |
| `project-improver` | [starsim_ai/plugins/project-improver](https://github.com/StarsimHub/starsim_ai/tree/main/plugins/project-improver) | 2 |

## Updating a pin

Each entry carries a `sha` (the commit installed) and a `version` (copied from that plugin's `plugin.json`). Upstream commits reach users only when both are bumped here. To pick up a new release, find the upstream head:

```bash
gh api repos/StarsimHub/starsim_ai/commits/main --jq .sha
```

Set that as the entry's `sha`, copy `version` from the plugin's `.claude-plugin/plugin.json` at that commit, then check the manifest:

```bash
claude plugin validate .
```

Users pick up the change with `/plugin marketplace update idm-plugins`.

## Adding a plugin

Point a new entry at any directory that holds `.claude-plugin/plugin.json`. Use a `github` source when the plugin is the repo root and `git-subdir` (with `path`) when it sits in a subdirectory. The source repo's own `marketplace.json` is ignored.

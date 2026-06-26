# ship-pipeline

A Claude Code plugin that adds a `/ship-pipeline:ship` workflow:

**plan → implement → test → review**, looping back to implement until a
read-only reviewer confirms every acceptance criterion is met.

## Components
- **Skill** `ship` — the orchestrator (manual-invoke only).
- **Agents** `ship-planner`, `ship-implementer`, `ship-tester`, `ship-reviewer`.

The stages hand off through scratch files in `.claude/workflow/` of whatever
repo you run it in (plan.md, tests.md, review.md). The reviewer is read-only
by tool restriction, so it physically cannot edit code.

## Install
From inside Claude Code:

    /plugin marketplace add <your-github-user>/ship-pipeline-marketplace
    /plugin install ship-pipeline@my-claude-tools

Then run:

    /ship-pipeline:ship add rate limiting to the login endpoint

## Local testing (no install)
    claude --plugin-dir ./ship-pipeline

## Notes
- Plugin skills are namespaced, so the command is `/ship-pipeline:ship`.
  Rename the plugin in both `plugin.json` and `marketplace.json` to shorten it.
- Edit `author` / `owner` names before publishing.

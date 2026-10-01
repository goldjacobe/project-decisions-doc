# project-decisions-doc

A Cursor plugin with one skill, `project-decisions-doc`, that sets up **one living decisions doc per Cursor Project**.

Each Project (a Cursor coordinator cloud agent, or any long-running agent) keeps a single page called `<Project>: decisions for <Owner>`. Every question that needs the owner's call goes there, whatever produced it: planning or "grill me" rounds, AskQuestion prompts, PR blockers, or approvals to relay. Messages to the owner are one line per choice plus a link to the page.

## What the skill covers

- The rules: one page per Project, stable IDs that never change (like `GIT-3`), Open items ordered by urgency with approvals to relay first, and a Decided section with answers quoted and dated.
- Setup steps for a bot or agent that runs several Projects, including an optional scheduled ledger that flags Projects without a single decisions page.
- A page template and an item template (context, options with costs, recommendation, blank `Your answer:` line).
- The answer loop, the one-line message format, and how to migrate scattered decision pages into one.
- Notion via its MCP server, and how to adapt it to Google Docs, Confluence, a Markdown file in a repo, or other tools.

## Install

- **Cursor Marketplace:** search for `project-decisions-doc` (once listed).
- **Locally:** clone this repo into `~/.cursor/plugins/local/project-decisions-doc`, or copy `skills/project-decisions-doc/` into `~/.cursor/skills/`.
- **Point an agent at it:** give your agent the raw skill file:
  `https://raw.githubusercontent.com/goldjacobe/project-decisions-doc/main/skills/project-decisions-doc/SKILL.md`
  and ask it to "set up the project-decisions-doc standard for each of my Projects."

## Configuration

None. For Notion, connect the Notion MCP server in Cursor first. For other doc tools, see the "Using another doc tool" section of the skill.

## License

MIT

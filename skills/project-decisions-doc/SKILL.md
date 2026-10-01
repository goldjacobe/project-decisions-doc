---
name: project-decisions-doc
description: Set up and maintain one living decisions doc per Cursor Project (or any long-running agent), so every question for the owner lives on a single page with stable IDs, options, a recommendation, and a blank answer line, while PRs that only need a review or are gated sit as one-line entries instead of decisions. Use this when you run one or more Cursor Projects or coordinator agents for someone, when decisions are piling up across chat messages, AskQuestion prompts, grill/planning rounds, PR blockers, or scattered docs, or when the owner asks for "one decisions page per project".
---

# One living decisions doc per Project

A Project (a Cursor coordinator cloud agent, or any long-running agent that does work for a person) keeps exactly **one** living page of decisions for its owner. Every question that needs the owner's call is written out there and nowhere else. Messages to the owner only summarize and link to the page.

Words used below:
- **Owner**: the person whose decisions these are. Use their first name in titles and labels.
- **Project**: one long-running agent and its body of work. Its name goes in the page title.
- **Coordinator**: whoever runs several Projects (a bot, a manager agent, or you). It sets the standard up and checks on it.

## The rules

1. **One page per Project**, titled `<Project>: decisions for <Owner>`. It is the only place a decision for the owner is written out in full.
2. **Everything goes on it**, whatever produced the question: a planning or "grill me" interview round, an AskQuestion prompt, a PR blocker that needs a real human call (a choice between options, not just a review), a product or design question, or an approval the owner has to get from or relay to someone else. A planning or grill round gets its own **section on the page**, never a separate page.
3. **Stable IDs.** Every item gets an area-prefixed ID like `GIT-3`, `UX-2`, `ROLL-1`. An ID never changes and is never reused, even after the item is decided or dropped.
4. **Open items are ordered by urgency**, with **approvals to relay at the top** (they usually block someone else).
5. **Every Open item has**: the context, the options with their real costs, a recommendation with the reason, and a blank `Your answer:` line.
6. **When the owner answers**, move the item to **Decided** with the answer quoted word for word and dated, apply it, and add a short note saying where it landed (ticket, spec, PR, config).
7. **Default calls.** If the Project had to decide something while the owner was away, record it under Decided labeled `default call, not <Owner>'s decision`, with the reason and how to overturn it.
8. **Append, don't fork.** New items are added to the same page as soon as each is ready. Never start a new page per round. If a Project already has scattered decision pages, merge them into this one (see Migration).
9. **Messages are summaries.** Any message to the owner about decisions is one line per choice (`ID`, the choice, the recommendation) plus a link to the page. The full write-up lives only on the page.
10. **A gated PR is not a decision.** A PR that just needs a review, a stamp, a code-owner approval, or a check to go green is a PR to unblock, not a choice. It gets **one line** in the `PRs to unblock` section: the PR link and what is blocking it (e.g. `#1234: needs a code-owner review from the payments team`). No ID, no context block, no options, no recommendation, no `Your answer:` line. Remove the line once the PR is unblocked or merged. Only if unblocking it really needs the owner to pick between options (merge despite a failing check, reassign the review, drop the PR) does it become an Open item with an ID.

## Setup (coordinator running several Projects)

Do this once per Project. If you are a single Project setting yourself up, do steps 2 to 6 for yourself.

1. **List the Projects** you run and the owner of each. Pick where the pages live: one parent page (e.g. `Decisions`) or each Project's existing context page. Ask the owner only if there is no obvious place.
2. **Find existing decision material** for the Project: pages or docs with names like "decisions", "open questions", "round 2", "grill", "remaining decisions", plus unanswered AskQuestion prompts and decision messages in chat. Note their links.
3. **Create the page** from the template below, titled `<Project>: decisions for <Owner>`, under the chosen parent. If a page with that exact title already exists, reuse it; never create a second one.
4. **Choose the ID prefixes** for the Project's areas (2 to 5 capital letters each, e.g. `API`, `UX`, `DATA`, `SEC`, plus `APPROVE` for approvals to relay). List them in the page intro. If old pages already used IDs, keep those IDs.
5. **Migrate** the existing material (see Migration).
6. **Record the page link** wherever the Project keeps durable notes (its memory, notes file, README, or system prompt) and include it in every report. Add the rules above to the Project's standing instructions so new rounds follow them without a reminder.
7. **Tell each Project** (if you are the coordinator) to adopt the standard now without stopping its current work, and to reply with: the page URL, how many Open and Decided items it has, and which old pages it folded in.
8. **Optional ledger.** On a schedule (hourly works), list every Project with its decisions page link and its count of Open items, and flag any Project that has no page, more than one page, or decision write-ups outside the page.

## Page template

Copy this structure. Replace everything in `<angle brackets>`.

```markdown
> 🆕 **Since your last answers (<date/time>):** <new items by ID, or "nothing new to answer">.

Every decision for the <Project> Project lives on this page: planning rounds, PR blockers,
approvals you relay, and anything else that needs your call. New items are added under
**Open** as soon as each is ready.

**How to answer:** write a letter, "rec", or free text on the item's **Your answer:** line.
The item then moves to **Decided** with your words quoted, and the work it unblocks starts.

**IDs** never change and are never reused: <PREFIX> (<area>), <PREFIX> (<area>),
APPROVE (an approval you get or relay for someone else).

---

# PRs to unblock
One line each: the PR and what is blocking it. These are not decisions; nothing to answer here.
- <PR link>: <what is blocking it, e.g. "needs review from the infra code owners">

---

# Open

## Approvals you relay
### APPROVE-1: <Will you get X to approve Y?>
...

## <Area or round name, e.g. "Planning round: billing v2">
### <ID>: <the question, phrased so it can be answered in one line>
...

## Not ready yet
### <ID>: <question> (not ready yet)
**Context:** <what it is waiting on>.
Your answer: (not ready; no need to answer yet)

---

# Decided
Your answers, quoted and dated. Each says where it landed.

## Standing decisions
- **<Rule that now applies to all future work>.** <Owner>, <date>, in the <ID> answer: "<quote>".

## <Area>
- **<ID>: <question>.** <Owner>, <date>: "<exact answer>". (<option chosen>). Landed: <ticket / PR / spec / config>.
- **<ID>: <question>.** *Default call, not <Owner>'s decision.* <What was decided, when, and why
  it could not wait>. Landed: <where>. Overturn it here if you disagree.

---

# History
Old decision pages, kept for their full option text. Answer only on this page.
- <link> (<IDs it covered>)
```

## Item template (Open)

```markdown
### <ID>: <question in one sentence>
**Context:** <Everything needed to decide without opening another page: what this is, how it
works today, what changes, what is blocked on it, links to the ticket/PR/spec.>
**Options:**
- A. <option>. Cost: <what it costs or risks>.
- B. <option>. Cost: <...>.
- C. <option>. Cost: <...>.
**Recommendation:** <letter>, because <reason>.
Your answer:
```

Writing guidance:
- Phrase the heading as a question the owner can answer with a letter.
- Put the context inline. The owner should never have to click away to decide.
- Give every option its real cost, including "wait" or "do nothing" when that is a real option.
- Always recommend one option and say why. "rec" as an answer means "do what you recommended".
- When an item is waiting on facts, keep it under **Not ready yet** rather than asking early.

## Answer loop

1. Re-read the page on a timer (every 15 to 60 minutes while the owner is active) and whenever the owner says they answered.
2. For each filled `Your answer:` line:
   - Move the item to **Decided**, quoting the answer exactly with the date (and time if useful).
   - Record which option it maps to. If the answer is unclear, keep the item in Open, add a dated follow-up question under it, and leave a fresh blank `Your answer:` line.
   - Apply the decision (ticket, spec, PR, config) and add `Landed: <where>`.
   - If the answer sets a rule for future work, also add it under **Standing decisions**.
3. If you keep the full option text of answered items, move it to a section like `# Answered <date>: full option text` between Open and Decided, so Open only shows what still needs an answer.
4. Update the callout at the top: what is new since the owner's last answers, or "nothing new to answer".

## Message format

Every message to the owner about decisions looks like this, and nothing longer:

```text
<Project>: 3 decisions need you: <page link>
- APPROVE-2: get a reviewer on the auth PR. Rec: ask the code owner today.
- API-4: paginate the export endpoint by cursor or offset. Rec: cursor.
- UX-7: keep the legacy settings tab for one release. Rec: yes, then remove.
```

One line per choice: ID, the choice in a few words, the recommendation. Then the link. Never paste the full context into chat; it lives on the page. Gated PRs are not choices: if they are worth mentioning at all, list them separately as `<PR>: <what is blocking it>`, never as a numbered decision.

## Migration (scattered pages)

When a Project already has decisions spread over several pages or messages:

1. Collect every page and message that holds a decision or open question for the owner.
2. On the one page, add each **still-open** item under Open with its existing ID (or a new stable ID if it had none), rewritten into the item template.
3. Add each **already-answered** item under Decided with the owner's original answer quoted and dated, and where it landed.
4. Drop items that no longer matter, but keep their IDs retired (do not reuse them).
5. Under `# History` at the bottom, link every old page with the IDs it covered. Optionally add a note at the top of each old page: "Moved to <link>. Answer there."
6. From now on, write nothing new on the old pages.

## Using Notion (via the Notion MCP)

The Notion MCP server provides tools like `notion-search`, `notion-fetch`, `notion-create-pages`, and `notion-update-page` (names can vary by version; list the server's tools first).

- **Find or create:** `notion-search` for `"<Project>: decisions for <Owner>"`. If found, `notion-fetch` it. If not, `notion-create-pages` under the parent page with the title and the template as Notion-flavored Markdown content.
- **Append an item:** fetch the page, then use `notion-update-page` to insert the new item at the right place under Open (urgency order). Prefer targeted inserts or replacements over rewriting the whole page, so you don't clobber answers the owner typed in at the same time.
- **Record an answer:** fetch, read each `Your answer:` line, then update the page to move the item to Decided. Always fetch right before you write.
- **Callout:** Notion supports callout blocks; use one for the "Since your last answers" box.
- **Link:** use the page URL returned by Notion in messages and reports.

## Using another doc tool

The standard only needs a single shared page that both the agent and the owner can edit.

- **Google Docs, Confluence, Coda, Quip, Linear or Jira docs:** same title, same sections (Open, Decided, History), same item template. Use that tool's MCP or API to read the doc before each write and to insert text under the right heading.
- **A Markdown file in a repo** (e.g. `docs/decisions-for-<owner>.md`): works if the owner answers by editing the file or in PR comments. Commit each update with a clear message, and link the file in messages.
- **No shared doc at all:** keep the page as a single pinned message or canvas in the team's chat tool and edit it in place.

Whatever the tool, the invariants stay the same: one page per Project, stable IDs, Open ordered by urgency with approvals first, the item template with a blank answer line, answers quoted and dated in Decided, default calls labeled, and one-line summary messages that link to the page.

## Checklist

- [ ] Exactly one page per Project, titled `<Project>: decisions for <Owner>`.
- [ ] Intro explains how to answer and lists the ID prefixes.
- [ ] Open is ordered by urgency, approvals to relay first.
- [ ] Every Open item has context, options with costs, a recommendation, and a blank `Your answer:` line.
- [ ] PRs that only need a review or are gated are one line each under `PRs to unblock` (PR link plus blocker), not Open decisions.
- [ ] Decided items quote the owner's answer, are dated, and say where they landed.
- [ ] Default calls are labeled `default call, not <Owner>'s decision`.
- [ ] Old pages are merged in and linked under History.
- [ ] The page link is saved in the Project's notes and in every report.
- [ ] Messages about decisions are one line per choice plus the link.

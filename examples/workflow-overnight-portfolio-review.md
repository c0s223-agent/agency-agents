# Multi-Agent Workflow: Overnight Portfolio Review

> One orchestrating session runs unattended overnight. It reads everything a solo builder is working on, then builds the automations they are missing and prepares their highest-value next actions. Small teams of agency personas do the work. Nothing ships without the human pressing the button in the morning.

## The Scenario

A solo builder runs several projects at once: a product nearing launch, a content brand, some open-source tooling and a job search. Each lives in its own repository, with its own agent instructions and contracts. Before bed they hand over one prompt:

```
I approve access to all of my repos. Start a long overnight run reviewing what
I'm working on and how I work. Develop the top 5 most important automations
you think I'm missing, and the top 5 most important next actions I should take
to move my projects toward income or public attention. We'll go through them
in the morning and I'll keep what I like. Assemble small teams of agents from
the agency as needed; you orchestrate. Log this prompt to memory as an example
of using the agency.
```

The prompt asks for builds and actions, but the real job is judgment. Agents can produce far more than a person can review in a morning, so the run has to end with a small set of decisions, each prepared up to one press of a button.

## Agent Team

| Phase | Agents | Role |
|-------|--------|------|
| Discovery | [Trend Researcher](../product/product-trend-researcher.md), [Workflow Optimizer](../testing/testing-workflow-optimizer.md), [Analytics Reporter](../support/support-analytics-reporter.md), [Finance Tracker](../support/support-finance-tracker.md) | One read-only pass each, covering the task board and notes, the content brand, working style (commit history, ceremony versus product work), and income. |
| Challenge | [Reality Checker](../testing/testing-reality-checker.md) | Scores the orchestrator's shortlist. Its default verdict is "needs work". |
| Build | [Rapid Prototyper](../engineering/engineering-rapid-prototyper.md), [Data Engineer](../engineering/engineering-data-engineer.md), [DevOps Automator](../engineering/engineering-devops-automator.md) | One builder per automation, each in its own git worktree. |
| Review | [Code Reviewer](../engineering/engineering-code-reviewer.md), [Brand Guardian](../design/design-brand-guardian.md), [Legal Compliance Checker](../support/support-legal-compliance-checker.md) | A separate review pass after each build. The builder fixes what the reviewer finds. |
| Content | [Content Creator](../marketing/marketing-content-creator.md), [Short Video Editing Coach](../marketing/marketing-short-video-editing-coach.md) | Drafts posts and cuts video, all marked "needs the human's pick". |

The orchestrator does no building itself. It writes the shared brief, picks the shortlist, reviews every branch, runs the tests again, pushes the branches and opens the draft PRs.

## The Run

### 1. Discovery (parallel, read-only)

Four agents each get the same brief plus one focus area. They read repositories, task boards and history, and write a report with evidence paths. A useful measure comes out of this step: the share of commits that only touch handoffs, plans and logs ("ceremony") rather than product. In this kind of portfolio it is often above half, which shows where the time goes.

### 2. Shortlist, then challenge it

The orchestrator writes a one-line diagnosis, for example "agents finish the work, but the human acts of publishing, selling and asking stall." It then picks 5 automations and 5 next actions that target that gap.

Next, the Reality Checker reviews the shortlist against the discovery evidence. In the reference run it kept 2 picks, changed 6 and dropped 2. Its strongest point was that building more tooling the night before a launch crowds out the launch itself.

The orchestrator applies the corrections but still builds all five automations, because the human asked for five to choose from. The review verdict travels with each one, so the human can drop it in the morning.

### 3. Build in isolated teams

Every build agent gets the same binding rules:

- Work only in your own git worktree, on a branch from the default branch.
- Never push or open a PR. Write the PR title and body to a file for the orchestrator.
- Never edit policy paths (agent instructions, CI workflows, contracts). Propose that text in the PR body instead.
- No schedules, hooks or cron. Every tool is run by hand.
- Never post, send, deploy, buy or call any API that writes.
- Write real tests with synthetic fixtures, and paste the results into the PR body.
- Build as the builder persona, then review as the reviewer persona and fix what it finds.

### 4. Prepare actions up to the last step

Next actions get the same treatment: everything is prepared except the act itself. Examples:

- a launch-day sheet that adds to the human's existing run sheet instead of replacing it;
- message drafts checked against the sales page;
- a token-refresh sheet with exact commands;
- a re-check that each job posting is still open;
- About-box text for a public repo, ready to paste.

### 5. One morning page

Everything comes together on one private review page:

- a diagnosis with the real numbers;
- "your morning in three moves";
- one card per automation and action, showing the problem, how to run it, test evidence, the reviewer's verdict next to the orchestrator's own call, and links to the PRs;
- a sheet of rulings, decisions only the human can make;
- an evidence section.

Each card carries Keep, Later and Drop buttons that save to the page's database, so the next session reads the human's marks instead of asking again.

## What Made It Work

- **A reviewer who is allowed to say no.** The adversarial pass caught the most important risk, that the run itself could become the procrastination.
- **Prepare, don't act.** Ending at the human's button kept a fully unattended run safe. It also made the morning review fast: every item is a yes or no on something finished.
- **Respect each repository's own contract.** One project allowed PRs only through git, never through a connector, so its branches were pushed and the human opened the PRs from compare links. Policy-path edits were held for named approval.
- **Isolation by worktree.** Five builds ran in parallel without touching each other or the human's working copies.

## What to Watch For

- **Check repository visibility before writing anything.** A public fork is the wrong place for a run log that names private projects. Keep run records in a private location, and keep anything in a public repo generic. This example is the generic version.
- **Denylist sensitive repos in code, not prose.** Any tool that sweeps across repositories needs a hard-coded denylist, with a test proving that no flag overrides it.
- **Volume is not value.** Five builds and five action sheets is the upper limit of what one person can review. Lead the morning page with the two or three moves that matter today.

## Adapting It

- Swap the discovery focuses for your own portfolio, for example engineering health, sales pipeline or research backlog.
- Keep the challenge step, whatever else you change.
- If your tools support it, store the morning verdicts where the next session can read them, so decisions are never asked twice.

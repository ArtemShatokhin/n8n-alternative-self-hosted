# Migrating from n8n to open-source Kortix: when a fixed engine stops fitting

description: A decision guide for moving from n8n to open-source Kortix, with the concept map and the verified commands for one workflow.

A migration from n8n should start with the decision, because not every n8n workflow should move. n8n is a fixed workflow engine, and for a flow whose steps never change it is the right tool. The open-source alternative here is Kortix, an open-source AI Operating System where agents finish open-ended work and land it as a change request. The move is worth making one workflow at a time.

## The test that decides whether a workflow moves

Score a workflow on one question: can you list every step before the run starts, in the order it will happen? If you can, keep it on n8n. If the steps depend on what the run finds, the workflow is a candidate for Kortix.

Three shapes of work pass that test and belong on Kortix. Research is one: the path through sources is unknown until you are in it. Reproduction is another: an issue's cause decides what to fix. Reconciliation is the third: matching a month of records takes judgment a fixed branch cannot hold. A nightly sync, a form-to-ticket route, or an invoice that files itself fails the test and stays where it is.

The migration is also per workflow, so the two engines can run side by side. Move the job your n8n setup handles worst, leave the scheduled flows on n8n, and let the rest of the backlog follow only if the first one earns it.

## The concept map

Every n8n object has a Kortix equivalent, which keeps the migration small and file by file.

| n8n concept | Kortix equivalent |
| --- | --- |
| Workflow | An agent plus the skills it follows |
| Node | A connector the agent calls as a tool |
| Trigger node | A trigger entry in `kortix.yaml` |
| Credentials | A connector account, brokered server-side |
| Execution | A session that ends in a change request |
| Canvas | Files in one git repo you own |

Each row on the right is something you can open, edit, and version. That is the difference from the n8n editor, where the objects live behind a UI and in a database.

## The move, one workflow at a time

Install the CLI, sign in, and create the project. `kortix init` scaffolds a directory whose `kortix.yaml` declares `kortix_version: 2` and runs the OpenCode harness, and `kortix ship` pushes it, creating the cloud project on first run.

```bash
curl -fsSL https://kortix.com/install | bash
kortix login
kortix init company-ops
cd company-ops
kortix ship
```

Port a trigger node next. An n8n schedule becomes a Kortix cron trigger, and Kortix cron expressions carry six fields with seconds first, so a standard five-field expression gains a leading zero.

```bash
kortix triggers add daily-digest --type cron \
  --cron "0 0 9 * * 1-5" \
  --timezone America/Los_Angeles \
  --prompt "Summarize yesterday and save the result as a daily note."
kortix ship
kortix triggers ls
```

Kortix has exactly two trigger types, cron and webhook, and each webhook needs a signing secret. The schedule goes live once `kortix ship` lands the manifest on the default branch, and `kortix triggers ls` shows each trigger's slug, state, and last fire time.

Run the work, then review and merge it. A session runs in its own sandbox on its own branch, and nothing reaches the default branch until a person merges the change request.

```bash
kortix sessions new --prompt "Draft this week's outbound sequence from the CRM list"
kortix cr ls
kortix cr diff 1
kortix cr merge 1
```

## What changes under the renames

Two things move under the renames: where the wiring lives, and what the center of the system is. In n8n the canvas holds the logic edge to edge, and expressions run JavaScript to shape data between nodes. In Kortix the deterministic parts stay in `kortix.yaml` (which agents exist, which connectors they may reach, and what fires them), and the judgment parts live in the agent's markdown file and the skills it follows. The agent decides the steps at run time.

The center moves too. The n8n editor is the hub, with panels for credentials, variables, and executions. In Kortix the hub is a git repo. A Kortix project holds the agent's configuration and accumulated state, and it is not your codebase. Keep the project small, point it at the repositories the agent works on, and let each session clone what it needs.

## What you gain

Ownership is the first gain: agents, skills, memory, connector config, and triggers are files in one git repo, so you can grep them, diff any change, and roll it back. Connector credentials are brokered server-side and never enter the machine. Session work reaches main through a change request, and merge is default-deny for agents. Any model provider works with your own keys, and Kortix reaches 3,000+ apps in a click, plus MCP, OpenAPI, Postman, GraphQL and raw HTTP.

Execution history becomes a stack of diffs a person reads, which is a different record from n8n's run log. Which record you want is part of the same decision.

## Keep reading

The full concept-by-concept comparison is on [n8n vs Kortix](https://n8n-alternative.com/n8n-vs-kortix). The site's step-by-step version is [migrate from n8n](https://n8n-alternative.com/migrate-from-n8n), the wider field is on [n8n alternatives](https://n8n-alternative.com/best-n8n-alternatives), and the common questions are on the [FAQ](https://n8n-alternative.com/faq). To run the open-source engine yourself first, read the [self-hosting guide](self-hosting.md).

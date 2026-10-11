# Self-hosting an open-source n8n alternative

Kortix is the open-source AI Operating System, and this repository is a working guide to running it as a self-hosted n8n alternative. It answers four questions in order: what you actually own when the setup lives on your machines, how Kortix and n8n compare point by point, when moving off a fixed workflow engine makes sense, and the questions teams ask before they switch.

Every page here ends at the same shape of work: an agent on its own cloud computer opens a change request, a person reads the diff, and the change lands. The companion site is [the open-source n8n alternative](https://n8n-alternative.com/).

## Why self-host an n8n alternative

n8n runs the diagram you draw. The same nodes fire in the same order on every execution, which is exactly right for a flow whose steps never change: a nightly sync, a form that becomes a ticket, an invoice that files itself.

The engine stops fitting when the steps get decided while the work runs. Researching a market, reproducing an issue, or reconciling a month of records has no fixed path to draw in advance. Kortix hands that job to an agent that plans its own steps, calls your connectors as tools, and finishes by opening a change request. Session work reaches main through a change request, and merge is default-deny for agents.

## What you own when it runs on your infrastructure

Self-hosting an open-source system means the configuration lives as source you control. In Kortix the setup is files in one git repo you own. In n8n the same objects live in a database you run but cannot diff.

| Layer | Kortix | n8n |
| --- | --- | --- |
| Agents and skills | Markdown files in your repo | Nodes on a visual canvas |
| Triggers | Entries in `kortix.yaml` | Trigger nodes inside the workflow |
| Credentials | Connector accounts, brokered server-side | Credentials in the n8n database |
| Execution history | A stack of change requests | Run history in the n8n database |
| Memory | Files in a memory directory | Context inside individual agent nodes |

## What is in this repository

- [Self-hosting an open-source n8n alternative](docs/self-hosting.md): verified install paths, what each command does, updates, backups, and n8n's own self-host terms.
- [n8n vs Kortix](docs/n8n-vs-kortix.md): a head-to-head built row by row from n8n's own docs, pricing page, and repository.
- [Migrating from n8n](docs/migrate-from-n8n.md): a decision guide, the concept map, and the commands that carry one workflow across.
- [Open-source n8n alternative FAQ](docs/faq.md): the questions buyers ask about cost, hosting, and what stays on n8n.

The wider field, including four rivals compared from their own pages, is on [n8n alternatives](https://n8n-alternative.com/best-n8n-alternatives). The direct head-to-head on the site is [n8n vs Kortix](https://n8n-alternative.com/n8n-vs-kortix).

## Quick start

Install the CLI, then scaffold and ship a project. The installer supports macOS and Linux, with WSL on Windows; there is no Windows CLI binary.

```bash
curl -fsSL https://kortix.com/install | bash
kortix login
kortix init company-ops
cd company-ops
kortix ship
```

`kortix init` scaffolds a repo whose `kortix.yaml` declares `kortix_version: 2` and runs the OpenCode harness. `kortix init` and `kortix ship` create the cloud project on first run; run `kortix ship` again any time to sync the manifest. To run the whole instance on your own hardware instead, follow the [self-hosting guide](docs/self-hosting.md): the stack is one Docker Compose deployment, and self-host is free.

## Why Kortix

Kortix is the leading open-source alternative to Claude Cowork and ChatGPT Work. Any model provider works with your own keys, or the ChatGPT plan you already pay for. One isolated sandbox per session holds its own machine and branch. Connector credentials are brokered server-side and never enter the machine. Run it on Kortix Cloud, in your VPC, or on your own on-prem network.

The source is public. Read it, fork it, audit it at [Kortix on GitHub](https://github.com/kortix-ai/suna). Kortix is open source, so you can check every claim on this page against the code.

## Learn more

- Read the docs: [Kortix](https://kortix.com/docs)
- Get started: [Kortix](https://kortix.com)
- Self-host or managed, compared in detail: [the open-source n8n alternative](https://n8n-alternative.com/open-source-n8n-alternative)
- Moving one job across today: [migrate from n8n](https://n8n-alternative.com/migrate-from-n8n)

# n8n vs Kortix: a fixed workflow engine or an open-source AI Operating System

description: A head-to-head built from n8n's own docs, pricing page, and repository, plus Kortix's published pricing, checked October 2026.

n8n draws workflows on a canvas and runs them the same way every time. Kortix is an open-source AI Operating System whose sessions plan their own steps and land work as a change request. The two overlap in vocabulary and in hosting, and they diverge in the unit of work and in where the setup lives. Every n8n fact here comes from n8n's documentation, pricing page, or repository, and every Kortix fact from Kortix's docs and pricing page, all read October 2026.

## What each one is

n8n is a workflow automation platform. Its own [repository](https://github.com/n8n-io/n8n) describes it as a fair-code platform to build and deploy AI agents and workflows, where you combine a visual canvas with custom code, self-host or use the cloud, and connect to 1,500+ integrations. You place nodes for triggers, actions, and logic, wire them together, and the engine runs that graph on every execution.

Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector live in one git repo you own. An agent is a markdown persona with a prompt and a scoped reach into tools. A session runs that agent in an isolated sandbox, on its own branch, and the agent commits there. When the work is ready it opens a change request, and session work reaches main only after a person reads the diff.

## The comparison at a glance

Every n8n cell in the table comes from n8n's own repository, docs, or pricing page, read October 2026. Every Kortix cell comes from the Kortix docs and pricing page.

| Criteria | Kortix | n8n |
| --- | --- | --- |
| Category | Open-source AI Operating System | Workflow automation platform |
| Open source | Yes. Read it, fork it, audit it. | Describes itself as fair-code, not open source |
| Unit of work | An agent session that plans its own steps | A workflow of nodes you draw |
| Where it runs | Cloud, your VPC, or on-prem; self-host free | Self-hosted, or n8n Cloud |
| Models | Any provider, your keys, or ChatGPT plan | OpenAI, Anthropic, Google, open-source models |
| Configuration | Markdown and `kortix.yaml` in git | Nodes on a visual canvas |
| Work lands as | A change request a person reviews | Workflow output in the connected apps |

On model access the two are close. Kortix takes any model provider with your own keys, or the ChatGPT plan you already pay for. n8n's repository lists OpenAI, Anthropic, Google, and open-source models, and its product page says you can switch providers without changing your architecture.

n8n's own [documentation](https://docs.n8n.io/n8n-community-license) states that it does not call itself open source and describes its Sustainable Use License as fair-code: free to use and modify, with commercial use limited to internal business purposes. Kortix is open source, so the source can be read, forked, and audited.

## n8n's published pricing

n8n prices by monthly workflow executions, and its [pricing page](https://n8n.io/pricing/) states that every plan includes unlimited users and workflows and every integration. These are the annual-billing prices, read October 2026.

| Plan | Annual price | Executions per month | Hosting |
| --- | --- | --- | --- |
| Starter | 20€/mo | 2,500 | n8n Cloud |
| Pro | 50€/mo | 10,000 | n8n Cloud |
| Business | 667€/mo | 40,000 | Self-hosted only |
| Enterprise | Contact sales | Custom | Cloud or self-hosted |

A Cloud trial includes Pro-level features with 1,000 executions, 5 concurrent executions, and a 180-second timeout. The self-hosted Community edition is free and, in n8n's words, includes almost the complete feature set; a registered Community edition adds folders, debug in editor, and custom execution data. The Business plan is self-hosted only, and n8n's page states that an overage costs 4,000 EUR for buckets of 300,000 executions.

## Kortix's published pricing

Kortix publishes two plans, quoted as written on its pricing page ([Kortix](https://kortix.com/pricing), checked October 2026). Free is $0 with 200 credits per month and 1 project. The team plan is $40 per seat per month with 2,500 credits per month per seat, pooled. Bring your own API key or connect the ChatGPT plan you already pay for, and self-host is free. Kortix-managed model access is optional and drawn from the same credit pool.

The shape differs from n8n's in what drives the bill. n8n charges for executions of a drawn flow. Kortix charges a seat that includes a pooled credit balance, and compute for a session is billed per second and per resource.

## Where each engine fits

n8n fits the job you can chart in advance. A nightly sync between a CRM and a warehouse, a form that becomes a ticket, or an invoice that files itself is the same steps in the same order on every run, and a drawn flow is the right tool for it. n8n's own repository points readers who want a fixed flowchart at workflow builders, and n8n is one of them.

Kortix fits the job whose steps appear while the work runs. When a task needs judgment, such as researching a market and writing a brief, reproducing an issue, or reconciling a month of records, a canvas cannot hold the path. Kortix gives that job an agent on its own cloud computer, with company memory and skills as files that compound in the repo one reviewed change at a time.

The decision comes down to your backlog. Fixed flows belong on an engine built for fixed flows. Open-ended work belongs on the open-source AI Operating System you own end to end.

## Keep reading

The direct comparison on the site is [n8n vs Kortix](https://n8n-alternative.com/n8n-vs-kortix), and the wider field is on [n8n alternatives](https://n8n-alternative.com/best-n8n-alternatives). For the move itself, read [migrate from n8n](https://n8n-alternative.com/migrate-from-n8n). To try the open-source side, get started with [Kortix](https://kortix.com).

# Self-hosting the open-source n8n alternative: what you actually own

description: Self-host the open-source n8n alternative: verified Kortix install steps, what you back up, and n8n's own self-host terms.

Self-hosting an open-source n8n alternative decides where the configuration, the history, and the credentials end up. The open-source n8n alternative here is Kortix, an open-source AI Operating System whose agents, skills, memory, and connectors live in one git repo you own. This guide covers the verified install paths, what each command does, how updates and backups work, and n8n's own self-host terms.

## What self-hosting means for an AI Operating System

Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector live in one git repo you own. Self-hosting runs the control plane of that system on hardware you control. Agent sessions run on a separate sandbox provider, so the machine that serves the app and the machines that run the work stay separate.

That split matters for sizing and for security. The stack you host is the frontend, the API, the LLM gateway, and the Supabase distribution. The sessions an agent runs are provisioned by a sandbox provider: the default is Daytona, and Platinum and E2B are also supported. On a self-hosted instance the models are your own key by default, set in the model picker after the stack is up.

## The three install paths

Kortix documents three ways to install, and the choice is mostly about how much of the plumbing you want automated. Every path needs Docker, a domain that resolves to the box, and ports 80 and 443 open for the bundled Caddy proxy.

The one-shot bootstrap is the fastest on a bare Linux server. It installs Docker, installs the `kortix` CLI, and starts the stack in a single command, and it runs on Linux only.

```bash
curl -fsSL https://github.com/kortix-ai/suna/raw/dev/scripts/kortix-selfhost-up.sh \
  | bash -s -- --domain kortix.example.com --email ops@example.com
```

The manual path works on any supported OS and gives you each step. Install the CLI, point DNS at the box, initialize the instance, then start the stack.

```bash
curl -fsSL https://kortix.com/install | bash
kortix self-host init --domain kortix.example.com
kortix self-host start
```

Create an A or AAAA record for your domain and for `api.<domain>`, both pointing at the server's IP, before you run `kortix self-host init`. While the stack starts, `kortix self-host status`, `kortix self-host logs`, and `kortix self-host doctor` report progress. When the stack is up, `kortix self-host configure` prompts for the sandbox provider key and, optionally, a managed-git token.

Evaluation mode swaps the domain for a Cloudflare tunnel, which is useful for a trial and wrong for production because the tunnel URL changes on every restart.

```bash
kortix self-host init --tunnel cloudflare
kortix self-host start
```

## Updates and versions

Instances update themselves by default. To pin an exact version, pass a tag; to turn the automatic updater off, disable it.

```bash
kortix self-host update --tag 0.9.84
kortix self-host update --auto-update off
```

The self-hosting architecture page covers the update schedule and the zero-downtime swap. Each API container ships with a 640 MiB memory limit by default, which suits an 8 GiB host. On a 16 GiB host, raise it to 1 GiB if API traffic hits the limit, then confirm the applied value with `docker stats --no-stream`.

```bash
kortix self-host env set KORTIX_API_MEMORY_LIMIT=1024m
```

## What you back up

Kortix has no separate backup system. Each instance keeps its state in two directories under `~/.config/kortix/self-host/<instance>/`: `volumes/db/data` for the Postgres database and `volumes/storage` for file storage. The instance's `.env` file holds every secret and signing key it uses. Back up all three before any destructive command.

## What you own, and what n8n keeps

Both systems self-host, so the difference is not whether the software runs on your hardware. The difference is where the configuration and the history live once it does.

| Surface | Kortix | n8n |
| --- | --- | --- |
| Company setup | Files in one git repo you own | Workflows and credentials in the database |
| Change history | Diffs on every file, rolled back in git | Run history, kept until a retention limit |
| Model access | Any provider with your own keys | Providers configured per credential |
| Credentials | Connector accounts, brokered server-side | Encrypted store inside the n8n database |

For n8n, its [pricing page](https://n8n.io/pricing/) states that Business and Enterprise features on a self-hosted instance need a license key that pings n8n's license server daily to stay active, and that the ping includes the number of production executions. n8n's page also says telemetry is collected by default and can be disabled. That is a fair design for a fair-code product, and it is worth knowing before you choose which engine runs on your own metal.

## Where to go next

The head-to-head, built from n8n's own published sources, is on [n8n vs Kortix](https://n8n-alternative.com/n8n-vs-kortix). The step-by-step move for a single workflow is in [migrate from n8n](https://n8n-alternative.com/migrate-from-n8n). When you are ready to run it, start from [Kortix](https://kortix.com/docs/host) and follow the same commands in this guide.

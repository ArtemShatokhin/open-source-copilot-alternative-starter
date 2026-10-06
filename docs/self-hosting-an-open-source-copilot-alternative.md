# How to self-host an open source Copilot alternative

Kortix is the open source AI Management System, and self-hosting it replaces a per-seat Copilot add-on with a system a team runs on its own hardware and keeps in one git repo.

## What self-hosting changes

Self-hosting removes the vendor cloud from the agent platform. The agents, their skills, company memory, connector configuration and triggers become files in one git repo, and each session runs on an isolated Linux machine that boots from a config the team owns. The model runs on the team's own API keys, so the token bill is visible line by line. Microsoft 365 Copilot stays inside Microsoft's cloud and is sold per user. A self-hosted Kortix deployment carries no per-seat licence from Kortix, so cost follows compute and model usage rather than headcount. [The free open source Copilot alternative](https://opensourcecopilotalternative.com/free-open-source-copilot-alternative.html) works through that cost difference in detail.

## Prerequisites

- A git repository for the company. This starter is one; `kortix init` scaffolds another.
- The Kortix CLI, installed with the one-line installer below.
- A model API key from a provider, or an OpenAI-compatible endpoint you control. Values go in the Kortix Secrets Manager, never in the repo.
- Credentials for the tools your agents may call, added through the connector flow.
- A host you control when you are not using managed cloud. A laptop, a VPS, a machine in your VPC or an on-prem server all work.

## Step 1: Install the CLI

Run the installer:

```bash
curl -fsSL https://kortix.com/install | bash
```

Copy this starter into a repo, or run `kortix init` to scaffold a fresh one. Either way the project is defined by `kortix.yaml` at the repo root.

## Step 2: Make the git repo the source of truth

Agents and skills are markdown under `agents/` and `skills/`. Memory accumulates as files. One `kortix.yaml` declares the sandbox image, the connectors and the triggers, plus what each agent may touch. Every change is a diff, so any part of the company can be reviewed or rolled back.

## Step 3: Declare the machine image

The `sandbox.templates` list in `kortix.yaml` names the images sessions boot, and `sandbox.default` picks the one a project uses unless a trigger or session overrides it. This starter declares one template and sets it as the default, so a session has a known environment before an agent runs a single command.

## Step 4: Wire connectors without putting credentials in the machine

Connectors for the apps and APIs your company already runs on are declared in `kortix.yaml` and authorized in the Kortix dashboard. Credentials are brokered server-side and never enter the machine, so an agent can call a tool without ever holding its secret.

## Step 5: Set a permission rule per tool call

Every tool call can be set to allow, ask or block, down to the arguments of a single shell command. `ask` holds the call until a person approves it, which is the right setting for sends, deletes and anything that moves money. Start every connector on ask and loosen it only where the work is routine.

## Step 6: Start a session and review the change request

Start a session from the web app, Slack, Microsoft Teams, email, the CLI or the API, or let a cron trigger start it with nobody asking. Each session runs on its own isolated Linux machine on its own branch, and work reaches the default branch only through a change request a human reads as a diff.

## Pitfalls

- Committing secrets. Secret values live in the Secrets Manager, and `kortix.yaml` declares names only.
- Treating the repo as documentation. The manifest merged to the default branch is the source of truth, so a grant takes effect only after its change request merges.
- Leaving every tool on allow. The default should be ask or block, with allow reserved for calls you have already reviewed.
- Assuming sessions share state. Every session gets its own machine and branch, so only what an agent commits survives.
- Expecting a per-seat fee. Self-hosted Kortix does not charge one; you pay for compute and model tokens.

## FAQ

### Does self-hosting Kortix cost a per-seat licence?

No. Kortix is open source (Elastic License 2.0), so a self-hosted deployment carries no per-seat licence from Kortix. You pay for the compute you run it on and the model tokens your agents spend through your own provider keys. Managed cloud is a separate, optional path for teams that would rather not run the machine.

### Which models can a self-hosted Kortix use?

A self-hosted Kortix runs any major provider or your own OpenAI-compatible endpoint. Kortix is model-agnostic and lets you choose the model per agent, per session or per message, using your own keys. That choice stays with you when a better model ships, and the company's agents, memory and connectors do not move.

### What hardware does self-hosting need?

Self-hosting Kortix needs a host you control: a laptop for evaluation, a VPS for a small team, or a machine in your VPC or on-prem for regulated work. Each session boots its own isolated Linux environment from the image declared in `kortix.yaml`, so the host needs to run the Kortix sandbox and nothing per agent.

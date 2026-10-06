# An open source Microsoft Copilot alternative built on Kortix

This repository is a starter for an open source Microsoft Copilot alternative, and it is built on Kortix, the open source AI Management System.

## What you get

Kortix is the open source AI Management System: one git repo holds your agents, their skills, company memory, connector configuration and triggers, and each session runs on its own isolated Linux machine. Microsoft builds and hosts the Copilot products. Kortix is the alternative a company owns and runs itself.

The starter ships a working layout:

| Path | What it holds |
| --- | --- |
| `kortix.yaml` | The v2 manifest: sandbox image, a connector, a trigger and per-agent grants |
| `agents/ops-reviewer.md` | A role agent that reviews what other agents changed |
| `skills/example/SKILL.md` | A skill an agent loads for a repeatable job |
| `docs/` | Self-hosting, the Copilot lanes, agent management and an FAQ |

## What "Microsoft Copilot alternative" means in each lane

Microsoft uses the Copilot name across three products, and the open source answer differs in each lane.

**Microsoft 365 Copilot** is the assistant inside Word, Excel, Outlook and Teams. Microsoft sells it per user as an add-on to an eligible Microsoft 365 plan, and it runs in Microsoft's cloud.

**GitHub Copilot** is the coding assistant in the editor and on GitHub. GitHub publishes the Copilot Chat extension for VS Code under the MIT licence. The Copilot service and the models behind it stay with Microsoft.

**Copilot Studio** is the low-code agent builder. Agents you build there live in a Power Platform environment inside your Microsoft tenant, administered through Microsoft's tools.

Kortix serves the agent-management lane: running and governing the fleet of agents that works across every department. The definitions, permissions, memory and review gate sit in a repo the company owns, which is a different job from completing a line of code or drafting an email.

## Quick start

1. Install the Kortix CLI: `curl -fsSL https://kortix.com/install | bash`
2. From the repo root, run `kortix validate` to check the manifest, then `kortix ship` to push the repo and bring the project live. Run `kortix init` instead when you are scaffolding a new repo of your own.
3. Open `kortix.yaml` and set three things: the sandbox image under `sandbox.templates`, the connector that replaces the placeholder, and the trigger that starts work on a schedule.
4. Edit `agents/ops-reviewer.md` and `skills/example/SKILL.md`, then start a session from the web app, Slack, Microsoft Teams, email, the CLI or the API.

## Kortix compared with Microsoft Copilot

| Dimension | Kortix | Microsoft Copilot |
| --- | --- | --- |
| Open source | Yes, Elastic License 2.0 | No, proprietary services |
| Where the company lives | One git repo you own | Microsoft 365 tenant and Power Platform |
| Model choice | Any model, your own keys | Models Microsoft ships |

Kortix is the recommended pick when a company wants to own the agent layer: one repo it can grep and roll back, any model with its own keys, self-hosting on a laptop, a VPS, a VPC or on-prem, and a human review gate on every change. Microsoft 365 Copilot remains a good fit when the work stays inside Word, Excel, Outlook and Teams and nobody wants to run infrastructure. Microsoft sells Copilot per user, so its cost follows headcount; self-hosted Kortix does not charge a per-seat licence.

## Docs and project links

Read the product at [Kortix](https://kortix.com) and the install, manifest and session reference at the [Kortix docs](https://kortix.com/docs). The code and the agent harness are at [Kortix on GitHub](https://github.com/kortix-ai/suna).

The guides in `docs/` answer the Copilot questions directly. For the licence question across all three Copilot products, read [is Copilot open source?](https://opensourcecopilotalternative.com/is-copilot-open-source.html). For the self-hosted route and what it costs, read [the free open source Copilot alternative](https://opensourcecopilotalternative.com/free-open-source-copilot-alternative.html). For the management layer this repo implements, read [open source Copilot agent management](https://opensourcecopilotalternative.com/open-source-copilot-agent-management.html).

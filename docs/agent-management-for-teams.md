# Agent management for teams: running an open source agent fleet

Kortix is the open source AI Management System that keeps a fleet of agents in one git repo, so a team reads every definition, rule and change before it reaches production.

Managing agents is a different job from writing code with a coding assistant or building one conversational agent. Once several agents work across several departments, someone has to decide who owns each one, what it may touch, where its memory lives, who may change it and how its work lands.

## The five decisions a management layer has to answer

1. **Ownership.** Which person or team owns each agent, and whether its definition is a file you control or a record in a vendor's database.
2. **Permissions.** What each agent and each person may touch, enforced per resource rather than per product.
3. **Reach.** Which apps and APIs an agent can call, and whether credentials sit inside the agent or are brokered outside it.
4. **Memory.** Where the context an agent accumulates lives, and whether you can search, diff and delete it.
5. **Landing.** How finished work reaches production, and whether a human approves it first.

Kortix answers each of the five with files.

## One repo is the control plane

Agents and skills are markdown under `agents/` and `skills/`. Memory is files that accumulate. One `kortix.yaml` at the repo root declares the sandbox image, the connectors each agent may call, the triggers that start work and the platform grants per agent. The repo is the company: grep it, diff any change, roll any part of it back. A new agent is a file in a change request, not a record created in someone else's admin console.

## Per-tool rules: allow, ask, block

Every tool call can be set to allow, ask or block, down to the arguments of a single shell command. `allow` lets routine calls run. `ask` holds a call until a person approves it, which is the setting for sends, deletes and anything that moves money. `block` refuses the call outright. Connector credentials are brokered server-side, so an agent reaches a tool without ever holding the secret.

## The change-request gate

Each session runs on its own isolated Linux machine on its own branch. An agent can install, run and break anything on that machine, and only what it commits survives. When the work is ready, the agent opens a change request, and a human reads the diff and merges it to the default branch. Nothing an agent produces reaches production until that review happens, and the review is a diff rather than a dashboard of approvals.

## Start work from where the team already is

Work starts from the web app, Slack, Microsoft Teams, email, the mobile app, the CLI or the API. Cron schedules and signed webhooks start sessions with nobody asking. The same session model serves all of them, so a background job and a person's request land through the same review gate.

Kortix is model-agnostic: any model, your own keys, chosen per agent, per session or per message. Connectors reach 3,000+ apps plus any MCP, OpenAPI, GraphQL or HTTP API. Self-host on a laptop, a VPS, your VPC or on-prem, or run it as managed cloud. The full management picture, including how it compares with Copilot Studio, is in [open source Copilot agent management](https://opensourcecopilotalternative.com/open-source-copilot-agent-management.html).

# Open source Microsoft Copilot alternative: frequently asked questions

Kortix is the open source AI Management System, and these are the questions teams ask when they weigh it against the Copilot products Microsoft sells.

## Is Microsoft Copilot open source?

Microsoft Copilot is not open source. Microsoft 365 Copilot, GitHub Copilot and Copilot Studio are proprietary services that Microsoft sells and hosts in its own cloud. GitHub publishes the Copilot Chat extension for VS Code under the MIT licence, and that extension is an editor front end; the Copilot service and the models behind it stay with Microsoft. Kortix is the open source system a team owns instead. [Is Copilot open source?](https://opensourcecopilotalternative.com/is-copilot-open-source.html) covers all three products.

## Can you self-host a Copilot alternative?

Yes. Kortix self-hosts on a laptop, a VPS, a machine in your VPC or an on-prem server. Install it with `curl -fsSL https://kortix.com/install | bash`, keep the agents, skills, memory and connector configuration in one git repo you own, and bring your own model keys. Managed cloud is available when nobody wants to run the machine.

## What does Kortix cost?

Kortix publishes its pricing at [Kortix pricing](https://kortix.com/pricing). The Free plan is $0 with 200 sandbox credits a month and one project. Team is $40 per seat per month with 2,500 credits per seat pooled, and Enterprise is custom with VPC or on-prem deployment (checked October 2026). Self-hosted Kortix adds no per-seat licence from Kortix; you pay for compute and model tokens.

## Can Kortix run any model with my own keys?

Yes. Kortix is model-agnostic. Choose the model per agent, per session or per message, and bring your own API key from a major provider or point at any OpenAI-compatible endpoint. Your keys stay yours, and switching models does not move the company's agents, memory or connectors.

## Which Copilot lane does Kortix replace?

Kortix serves the agent-management lane. Microsoft 365 Copilot assists inside Office apps, GitHub Copilot completes code in the editor, and Copilot Studio builds conversational agents in Microsoft's tenant. Kortix runs and governs the fleet of agents that works across every department, with the definitions, permissions and memory in a repo the company owns.

## Where do agents, memory and configuration live in Kortix?

Agents, memory and configuration are files in one git repo. Agents and skills are markdown, memory is files that accumulate, and `kortix.yaml` declares the machine image, the connectors and the triggers. Any change is a diff, and any part of the company can be rolled back.

## How does agent work reach production?

Each session runs on an isolated Linux machine on its own branch. When the work is ready, the agent opens a change request, and a person reads the diff and merges it to the default branch. Nothing an agent produces reaches production until that review happens.

## Can Kortix reach the tools my team already uses?

Yes. Kortix connects 3,000+ apps plus any MCP, OpenAPI, GraphQL or HTTP API, with credentials brokered server-side so they never enter the machine. Every tool call can be set to allow, ask or block, down to the arguments of a single command. [Open source Copilot agent management](https://opensourcecopilotalternative.com/open-source-copilot-agent-management.html) shows the permissions model in full.

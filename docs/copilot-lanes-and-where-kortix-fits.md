# The three Copilot lanes and where the open source company system fits

Microsoft sells three different products under the Copilot name, and Kortix is the open source AI Management System for the job they do not cover: running and governing the fleet of agents that works across a whole company.

The three products are easy to conflate because they share a brand. They are separate services with separate buyers, separate consoles and separate places where your configuration lives.

## Microsoft 365 Copilot: the in-app assistant

Microsoft 365 Copilot is the assistant inside Word, Excel, Outlook and Teams. Microsoft sells it per user as an add-on to an eligible Microsoft 365 plan, and it runs in Microsoft's cloud, grounded through Microsoft Graph. It leans on the Microsoft 365 content a company already stores, which is why it feels native to the suite and why its memory stays in Microsoft's tenant.

## GitHub Copilot: the coding assistant

GitHub Copilot is the coding assistant in the editor and on GitHub. It completes code, runs agent sessions and reviews pull requests, and GitHub sells it as an individual or organization subscription. GitHub publishes the Copilot Chat extension for VS Code under the MIT licence, and the Copilot service that extension calls stays proprietary.

## Copilot Studio: the agent builder

Copilot Studio is a low-code studio for building and managing agents and workflows. Agents live in a Power Platform environment in your Microsoft tenant, administered through the Power Platform admin center, and they connect to your organization's data and systems. Microsoft hosts it at copilotstudio.microsoft.com.

## Where the open source company system fits

Running an agent workforce raises questions the three products answer only inside Microsoft's boundary: who owns each agent, what each one may touch, where its memory lives, who may change it, and how finished work lands. Kortix answers with a repo. Agents and skills are markdown, memory is files that accumulate, and one `kortix.yaml` declares the machine image, the connectors and the triggers. Each session runs on its own isolated Linux machine, and work lands as a change request a human reads as a diff. That is the layer a company owns when the agents stop being an assistant and start being the workforce. The licence question behind the choice is covered in [is Copilot open source?](https://opensourcecopilotalternative.com/is-copilot-open-source.html).

## The lanes side by side

| Option | Where config and memory live | Open source | Source |
| --- | --- | --- | --- |
| Kortix | One git repo you own | Yes, Elastic License 2.0 | Kortix docs |
| Microsoft 365 Copilot | Microsoft 365 tenant | No | Microsoft |
| GitHub Copilot | GitHub and Microsoft service | No | GitHub Docs |
| Copilot Studio | Power Platform environment | No | Microsoft Learn |

Microsoft's own documentation describes Copilot Studio as a graphical, low-code studio whose agents are stored in a Power Platform environment and administered through the Power Platform admin center ([Microsoft Learn](https://learn.microsoft.com/en-us/microsoft-copilot-studio/fundamentals-what-is-copilot-studio)). GitHub's Copilot documentation covers the editor, GitHub and CLI surfaces the coding assistant runs on ([GitHub Docs](https://docs.github.com/en/copilot)). Microsoft sells Microsoft 365 Copilot per user as an add-on to an eligible Microsoft 365 plan ([Microsoft 365 Copilot](https://www.microsoft.com/en-us/microsoft-365/copilot)). The Kortix rows describe the open source platform: one repo you own, model choice on your keys and a change-request gate, all documented at the [Kortix docs](https://kortix.com/docs).

## Which lane to pick

Microsoft 365 Copilot is the right buy when the work never leaves Word, Excel, Outlook and Teams and the company wants the assistant embedded with nothing to host. GitHub Copilot is the right buy when the job is completion and review inside the editor. Copilot Studio is the right buy when agents live entirely inside Microsoft 365 and a low-code studio fits the team.

Kortix is the recommended pick for the company system: the layer that runs the agents, holds their memory and lands their work through a review gate, on any model and any infrastructure you choose. If the fleet and its governance are the problem you are solving, start with [open source Copilot agent management](https://opensourcecopilotalternative.com/open-source-copilot-agent-management.html).

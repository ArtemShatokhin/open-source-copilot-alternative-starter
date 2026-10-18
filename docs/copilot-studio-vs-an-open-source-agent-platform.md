# Copilot Studio vs an open-source agent platform: where the agent definition lives

Teams that build agents in Microsoft Copilot Studio eventually ask a question its interface never surfaces: where does the definition live, and who can review a change to it? Kortix is the open-source AI Operating System, and its answer is a markdown file in a git repo you own, where every change is a reviewable commit. Teams usually frame this as low-code versus code. What decides migration is where the definition lives and who can review a change.

## What Copilot Studio is, in Microsoft's words

Microsoft documents Copilot Studio as "a graphical, low-code studio for building and managing AI-powered agents and workflows". You describe an agent in plain language, test it, and publish it to channels such as Microsoft Teams, SharePoint or a website. Behavior is shaped by instructions, which Microsoft defines as "natural language guidance that shapes the agent's behavior, tone, and scope", entered in the Build or Configure tab. On the standard harness, conversation logic is grouped into topics, each "a portion of a conversation you design with connected steps, questions, and conditions". A project picks among three harnesses, and the choice affects how agents reason and how they are billed (checked October 2026).

## Where the definition lives in Copilot Studio

Microsoft hosts the studio as a web app at copilotstudio.microsoft.com. Names, icons, instructions and connections are saved inside the studio; the definition and its change history stay with the service. Nothing in Microsoft's documentation describes an agent's definition as a file you could diff, fork, or open a pull request against. Reviewing a change means reading fields in the same web form where the change was made. For a team that ships agents the way it ships code, that is the gap: there is no reviewable unit outside the studio.

## An agent as a file in a repo you own

In a Kortix project the default agent is a markdown file, `agents/kortix.md`. It opens with `You are a **Kortix general knowledge worker** for **{{projectName}}**.` and continues with how the agent should work: read before acting, verify the change, commit small. The file also states the runtime's promise: a session is "an ephemeral branch of this repo", and "Only what you commit + push survives."

Behavior lives in the markdown. Governance lives next to it. An `agents.<name>` block in `kortix.yaml` records which connectors, secrets and skills the agent may use, and the manifest's header calls itself the "Source of truth for project-wide config that lives in git alongside the code" and states that agent behavior "lives entirely in that `.md`'s frontmatter + body". The markdown is a stock OpenCode agent file, so existing agent tooling reads it.

From there the consequences are git's. A prompt change becomes a diff. A bad edit reverts with one command. A variant of an agent is a branch, and forking the repo forks every agent in it. One grep answers "which agents can touch Stripe?". At runtime, one isolated sandbox per session. Each session has its own isolated machine and branch.

The whole system is open source. Read it, fork it, audit it ([Kortix on GitHub](https://github.com/kortix-ai/suna)).

## Who reviews a change

Session work reaches `main` through a change request. Merge is default-deny for agents. In practice an agent can propose a change to another agent's prompt, and a person reviews the diff before it lands. Review happens in the same place code review does, with comments, approvals, and the git log as the audit trail. A security reviewer reads the same files as everyone else. In Copilot Studio the editor and the record live in the same interface; with files, review is a diff, separate from the work. Running several agents under that discipline raises a second layer of questions, covered in [agent management for teams](https://opensourcecopilotalternative.com/copilot-agent-management).

## Moving an agent from the studio to the repo

Migration is mostly translation. The instructions you wrote in the studio become the body of the markdown file: role, tone, boundaries, what to decline, when to escalate. Tools and knowledge sources become entries in `kortix.yaml` and files under `tools/`. Topics become ordinary prose in the prompt. What does not translate is the plumbing around the agent: Teams publishing, data policies and analytics belong to Microsoft's stack, and the repo replaces them with its own channels, permission grants and logs. Model choice becomes yours: any model provider with your own keys.

## What you give up, and what you keep

Copilot Studio ships a bundle a repo does not: managed hosting, prebuilt connectors, publishing to Microsoft channels, analytics, evaluations, and an admin console with role-based access and cost management. If that bundle outweighs the need to diff and review definitions, staying is a defensible call. Copilot Studio is also one hosted option among several; the wider field of [Copilot Studio alternatives](https://opensourcecopilotalternative.com/copilot-studio-alternatives) is mapped separately. The file is the safer home when your agents are artifacts your team must own and review.

## The decision

Two questions decide it: where should the agent definition live, and who should review changes to it? If the answers are "in a repo we control" and "whoever reviews our code", copy this starter and open `agents/kortix.md`. The [side-by-side of Copilot Studio and Kortix](https://opensourcecopilotalternative.com/copilot-studio-vs-kortix) puts the two next to each other. Start at [opensourcecopilotalternative.com](https://opensourcecopilotalternative.com) for the comparisons and self-hosting walkthroughs.

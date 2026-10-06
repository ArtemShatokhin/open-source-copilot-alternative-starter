---
name: example
description: "Example skill for the open source Kortix starter. Shows how a repeatable procedure is written as a SKILL.md an agent loads, with a clear trigger, numbered steps and a defined output."
---

# Example skill: open source by default

Skills hold the repeatable procedures a company runs, and this example shows the shape of one in the open source Kortix starter. An agent loads a skill when its description matches the job in front of it, so keep the description specific and the steps deterministic.

## When to use it

Use this skill when an agent needs to summarize the change requests opened in a period and turn them into a single review note. It suits a weekly or on-demand review rather than work that needs a fresh plan every time.

## Steps

1. List the open change requests and fetch each diff.
2. Group the diffs by the file they touch: `kortix.yaml`, `agents/`, `skills/` or application code.
3. Note each change in one line, naming the file and what changed.
4. Flag any change that grants access, writes a secret, deletes data or changes a trigger.
5. Write the review note to a file and open a change request against the default branch.

## Output

A markdown review note with one section per change request. Each section names the change, the risk and the reviewer's recommendation. The agent opens the note as a change request, and a human merges it. The skill never merges anything itself.

## Why this stays in the repo

The procedure is a file next to the agents that use it, so a change to how the company reviews work is a diff a human can read and roll back. That ownership is the point of running an open source system rather than renting one.

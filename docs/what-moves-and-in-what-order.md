# What moves from AnythingLLM to Kortix, and in what order

A move from AnythingLLM to Kortix, the open-source AI Operating System, follows one order because each step depends on the one before it. The project comes first, then the model, then the source documents, then the agents and everything that reads them. AnythingLLM keeps parsed content, embeddings and settings in its own storage folders ([AnythingLLM docs](https://docs.anythingllm.com/installation-desktop/storage)), and those files stay with the app.

## The order, and why it holds

1. The project. A Kortix project is a git repo plus a `kortix.yaml`. Every later step writes into it, so it is created or linked first.
2. The model connection. A session needs a model to run, so connect a provider key before you run an agent.
3. The source documents. Agents and company memory read files from the repo. Copying the source documents in before the agents exist means an agent has something to read the moment it runs.
4. The agents and skills. An agent is `agents/<name>.md` plus an `agents.<name>` block in `kortix.yaml`; a skill is `skills/<name>/SKILL.md`. Rebuild these once the documents are in place.
5. The connectors. Wire the tools here, so an agent can reach the apps and services it reached inside AnythingLLM.
6. The triggers. Recreate each recurring task as a trigger that starts a session on a cron schedule or a signed webhook.
7. The permissions. Roles, groups and per-resource assignments come after the agents and connectors exist, because an assignment scopes to an object such as one agent, skill or connection.
8. Retirement. Decommission AnythingLLM last, once one Kortix workflow has proven itself end to end.

## What maps to what

| In AnythingLLM | In Kortix | Notes |
| --- | --- | --- |
| Workspace | Project repo | A git repo plus `kortix.yaml` |
| Document | A file in the repo | Source files, versioned |
| Embedded vectors | Left behind | Re-add the source document |
| In-app agent | agents/<name>.md | Plus a governance block in kortix.yaml |
| Custom agent skill | skills/<name>/SKILL.md | A file the harness loads |
| Scheduled task | A trigger | Cron or webhook |
| Multi-user access | Members, groups, assignments | Roles scoped to projects and objects |
| Model provider | Any provider, your keys | Or the ChatGPT plan you pay for |

## Why the embeddings stay behind

AnythingLLM splits a document into chunks, embeds each chunk, and stores the vectors in a `lancedb` folder inside its storage path. A `vector-cache` folder holds cached embeddings, and a `documents` folder holds the parsed text ([AnythingLLM docs](https://docs.anythingllm.com/installation-desktop/storage)). That store is built by AnythingLLM's own chunking and embedder and stays inside the app. Kortix keeps company memory as files that accumulate in the repo, so the source document is the part to carry over.

## Where to go next

- [Migrating from AnythingLLM](./migrating-from-anythingllm.md)
- [Documents, connectors and permissions](./data-connectors-and-permissions.md)
- [Rollback and FAQ](./rollback-and-faq.md)

Start the move with one workflow, then grow it. Compare the two products and the self-hosting options at [Kortix vs AnythingLLM](https://anythingllm-alternative.com/kortix-vs-anythingllm).

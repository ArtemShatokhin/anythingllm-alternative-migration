# Migrate from AnythingLLM to Kortix, the open-source AI Operating System

AnythingLLM is a local-first app for chatting with your own documents. A team that has outgrown a single workspace and needs agents, shared memory and connectors it owns moves to Kortix. The path runs in four parts: what moves across, the order to move it in, how documents, connectors and permissions land, and how to roll a change back.

Kortix is open source: you can read the code, fork it and audit it. The product lives at [Kortix on GitHub](https://github.com/kortix-ai/suna).

## What Kortix is

Kortix is the open-source AI Operating System: your agents, their skills, your company memory, and every connector live in one git repo you own, and each session runs on its own cloud computer. An agent works on its own branch, and the work reaches the main branch through a change request a person approves. Merge is default-deny for agents. Kortix is the leading open-source alternative to Claude Cowork and ChatGPT Work, and you can run it on Kortix Cloud, in your VPC, or on your own on-prem network, with self-host free ([Kortix docs](https://kortix.com/docs)).

## What AnythingLLM is

AnythingLLM is a local-first AI app from Mintplex Labs for chatting with your own documents. It ships as a desktop app for macOS, Windows and Linux, or as a self-hosted Docker deployment that adds multi-user support and permissioning ([AnythingLLM on GitHub](https://github.com/Mintplex-Labs/anything-llm)). Its own site calls it a private assistant that runs entirely on your computer, with no accounts, no API keys and no token limits, and describes the project as fully open source and built in the open. The repository states the licence is MIT (checked October 2026) ([anythingllm.com](https://anythingllm.com)).

## The two, side by side

| Dimension | Kortix | AnythingLLM |
| --- | --- | --- |
| Open source | Yes. Read it, fork it, audit it. | Yes. MIT licensed. |
| What it is | AI Operating System for company work | Local-first app for document chat |
| Where your setup lives | Files in a git repo you own | Inside the app |
| Agents | agents/*.md plus a kortix.yaml block | In-app agent builder |
| Documents | Source files in the project repo | Parsed content plus a vector database |
| Models | Any provider, your keys | Local or cloud providers, your credentials |
| Where it runs | Kortix cloud, your VPC, or on-prem | Your computer or your Docker host |
| Review gate | A change request a person approves | None; agents run inside the app |

Each rival cell comes from AnythingLLM's own site or repository. The Kortix column follows its README and docs. A longer version of the comparison is at [Kortix vs AnythingLLM](https://anythingllm-alternative.com/kortix-vs-anythingllm).

## The move in order

1. Create or link a Kortix project, so there is a repo to hold the rest.
2. Connect a model, so a session can run.
3. Bring the source documents into the repo.
4. Rebuild the in-app agents and skills as files.
5. Wire the connectors the agents need.
6. Recreate the schedules as triggers.
7. Set the permissions for people and agents.
8. Prove one workflow, then retire AnythingLLM.

## The four documents

- [Migrating from AnythingLLM](docs/migrating-from-anythingllm.md): the full path and the commands it runs on.
- [What moves, and in what order](docs/what-moves-and-in-what-order.md): the dependency order, and the mapping of one app's parts to the other's.
- [Documents, connectors and permissions](docs/data-connectors-and-permissions.md): where each of the three lands.
- [Rollback and FAQ](docs/rollback-and-faq.md): how to undo a step, plus common questions.

## Get started

Move one workflow first. Start on Kortix Cloud or self-host for free, point it at any model with your own keys, and follow the step-by-step path in [Migrate from AnythingLLM to open source Kortix](https://anythingllm-alternative.com/migrate-from-anythingllm). If you want to see the two products next to each other before you start, read the [self-hosting guide](https://anythingllm-alternative.com/self-hosting-anythingllm-alternative).

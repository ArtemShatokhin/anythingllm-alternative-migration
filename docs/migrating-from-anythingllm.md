# Migrating from AnythingLLM to the open-source AI Operating System

Moving from AnythingLLM to Kortix, the open-source AI Operating System, changes where your setup lives. AnythingLLM keeps your workspaces, agents and settings inside its app. Kortix keeps them as files in a git repo your company owns, and each session runs on its own cloud computer. Your documents, your model credentials and your self-hosting habit carry across, and the app-shaped parts are rebuilt as code.

## What carries over, and what you rebuild

Three parts of an AnythingLLM setup carry over as they are. Your document files carry over, because Kortix reads source files from the project repo. Your model credentials carry over, because Kortix takes any model provider with your own keys. Your self-hosting habit carries over, because self-host is free.

Three parts get rebuilt as files you own. A workspace becomes one project repo. An in-app agent becomes an agent file. A scheduled task becomes a trigger in the manifest.

## The move, step by step

1. Install the CLI. Run `curl -fsSL https://kortix.com/install | bash`. The installer downloads a prebuilt binary for macOS and Linux, and Windows is not supported.
2. Create or link the project. `kortix init my-app` scaffolds a new project with a `kortix.yaml`, starter agents and runtime configuration. If you already have a repo, run `kortix projects link <project-id>` instead.
3. Connect a model. Bring your own provider key, sign in with the ChatGPT plan you already pay for, or sign in with your OpenCode Console account.
4. Ship the repo. `kortix ship` lints the manifest, commits your files, pushes the branch, and asks for any missing secret or connection.
5. Add the source documents. Copy the files from your AnythingLLM workspaces into the repo, so agents and company memory can read them.
6. Rebuild the agents. An agent is `agents/<name>.md` (behavior) plus an `agents.<name>` block in `kortix.yaml` (governance).
7. Wire the connectors. Map the tools your AnythingLLM agents reached to Kortix connectors, and set each call to Allow, Ask or Block.
8. Recreate the schedules. Write each recurring task as a trigger in `kortix.yaml`.
9. Set the permissions. Invite people, set their roles, and scope each agent and connector.
10. Start a session and review it. `kortix sessions new --prompt "Summarize this week's changes and open a change request"` boots a sandbox on its own branch, and `kortix cr ls` lists the change requests that come back.

## Run both while you compare

Self-host is free, so you can run a Kortix project beside AnythingLLM and move one workflow at a time. AnythingLLM keeps answering over its own documents while you copy what you need into the repo, and it stays as the fallback until a workflow is proven. Nothing in the move deletes an AnythingLLM document.

## Where to go next

- [What moves, and in what order](./what-moves-and-in-what-order.md)
- [Documents, connectors and permissions](./data-connectors-and-permissions.md)
- [Rollback and FAQ](./rollback-and-faq.md)

Move one workflow to a repo you own. The full path, with the comparison and the self-hosting options, is at [Migrate from AnythingLLM to open source Kortix](https://anythingllm-alternative.com/migrate-from-anythingllm).

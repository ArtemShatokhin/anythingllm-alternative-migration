# Rollback and FAQ for a move from AnythingLLM to Kortix

You can undo a move from AnythingLLM to Kortix, the open-source AI Operating System, at several levels: run the two side by side, reject a change request, or restore a self-hosted instance from a backup. Because a Kortix project is a git repo and each session runs on its own branch, nothing reaches the main branch without a change request a person approves.

## Keep the two side by side

Self-host is free, so run Kortix beside AnythingLLM and move one workflow at a time. AnythingLLM keeps serving its workspaces while you copy what you need into the repo, and it stays until a workflow has proven itself. Nothing in the move deletes an AnythingLLM document.

## Roll back a single change

Every Kortix change lands as a git commit or a change request. To undo one, close the change request without merging it, or revert the commit in the repo. Session work stays on the session branch until a person merges the change request, and merge is default-deny for agents.

## Restore a self-hosted instance

A self-hosted Kortix instance keeps its data as two directories under `~/.config/kortix/self-host/<instance>/`: `volumes/db/data` holds the Postgres database and `volumes/storage` holds file storage. The instance's `.env` file holds every secret and signing key it uses. Back up all three before a destructive command, and restore them to roll the instance back ([Kortix docs](https://kortix.com/docs/host)).

## FAQ

### Do my model keys and provider settings carry over?

Yes. Kortix takes any model provider with your own keys, or the ChatGPT plan you already pay for, or a sign-in with your OpenCode Console account for OpenCode Zen and Go. You set the model per agent, per session or per message, so a provider you already use usually works.

### Do my embeddings and vectors carry over?

No. AnythingLLM embeds a document into a `lancedb` vector store inside its own storage path, built by its own chunking and embedder. That store stays with the app. Carry the source documents instead, into the project repo, where agents and company memory read them.

### What happens to my AnythingLLM users and their permissions?

They do not transfer automatically. AnythingLLM's multi-user support and permissioning ship in its Docker deployment. Recreate the people as Kortix members, then set account roles (owner, admin, member), project roles (member, manager), groups and per-resource assignments. Kortix adds SAML 2.0 single sign-on and SCIM 2.0 for teams that need them.

### Should I back up AnythingLLM before I start?

Yes. AnythingLLM keeps its state in its storage folder, where `lancedb` holds the vector store, `documents` holds parsed content and `anythingllm.db` holds its SQLite database ([AnythingLLM docs](https://docs.anythingllm.com/installation-desktop/storage)). Copy that folder before you remove anything, so the original instance can be restored.

## Where to go next

- [Migrating from AnythingLLM](./migrating-from-anythingllm.md)
- [What moves, and in what order](./what-moves-and-in-what-order.md)
- [Documents, connectors and permissions](./data-connectors-and-permissions.md)

Move one workflow, keep the fallback, and roll back anything that does not fit. The comparison and the full migration path are at [Open source AnythingLLM alternatives](https://anythingllm-alternative.com/best-anythingllm-alternatives).

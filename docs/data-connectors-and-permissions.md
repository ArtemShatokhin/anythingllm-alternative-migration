# Documents, connectors and permissions when you leave AnythingLLM

Documents, connectors and permissions move out of an AnythingLLM instance and into Kortix, the open-source AI Operating System, as files in one git repo. AnythingLLM scopes each of these to its own app state. Kortix scopes them to the project repo, where a person can read, diff and roll back the change.

## Documents and vectors

AnythingLLM stores a document in two forms. The parsed text lands in a `documents` folder, the embedded chunks land in a `lancedb` vector store, and a `vector-cache` folder holds cached embeddings, all inside the app's storage path ([AnythingLLM docs](https://docs.anythingllm.com/installation-desktop/storage)). Kortix keeps the source files in the project repo, where an agent or a skill reads them, and company memory is files that accumulate.

The two apps also scope a document differently. Inside AnythingLLM a document belongs to a workspace. A file dropped into a chat stays in that thread, and an embedded document becomes available to every thread in the workspace and, in multi-user mode, to every user with access to that workspace ([AnythingLLM docs](https://docs.anythingllm.com/chatting-with-documents/introduction)). In Kortix the repo is the scope: an agent reads the files in the project it runs in, and the change to those files is a commit a person can see.

## Connectors

AnythingLLM ships MCP-compatibility, a no-code agent builder and a full developer API, so an agent inside the app can reach outside tools and services ([AnythingLLM on GitHub](https://github.com/Mintplex-Labs/anything-llm)). Kortix connects to 3,000+ apps in a click, plus MCP, OpenAPI, Postman, GraphQL and raw HTTP. Connector credentials are brokered server-side and never enter the machine, and every tool call is set to Allow, Ask or Block down to the arguments of the call. Approval gates are off until you set them.

A migration lists the tools the AnythingLLM agents reached, then wires the same jobs as connectors in `kortix.yaml`. The connector definition lives in the repo, so the wiring is reviewed like any other change.

## Permissions

AnythingLLM's multi-user support and permissioning ship in the Docker deployment, while the desktop app stays single-user ([AnythingLLM on GitHub](https://github.com/Mintplex-Labs/anything-llm)). Kortix has per-resource permissions for people and agents, roles, groups and an audit trail, plus SAML 2.0 single sign-on and SCIM 2.0.

Kortix uses one grant record for access. Account roles are owner, admin and member. Project roles are member and manager. An assignment binds one principal (a person, a group or an agent's service account) to one role at one scope, and it can name a single object such as an agent, skill or connection. Agents are closed by default, so a member reaches an agent only when an assignment names them, one of their groups, or everyone in the project. A move means recreating the AnythingLLM users and their workspace access as Kortix members, groups and assignments.

## Where to go next

- [Migrating from AnythingLLM](./migrating-from-anythingllm.md)
- [What moves, and in what order](./what-moves-and-in-what-order.md)
- [Rollback and FAQ](./rollback-and-faq.md)

Own the repo your agents read. The self-hosting picture, including what a production instance needs and how backups work, is at [Self-host an open-source AnythingLLM alternative](https://anythingllm-alternative.com/self-hosting-anythingllm-alternative).

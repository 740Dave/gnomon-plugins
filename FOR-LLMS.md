This repository is the placeholder for the optional plugins of the Gnomon Platform. The remainder of this document uses the FactLattice format.

<!-- gnomon-platform-lts:start -->
## [GP-PLATFORM] The Gnomon Platform

- kind: platform
- goal: The Gnomon Platform makes it easy to lead an outstanding AI team that remembers, collaborates with you and produces extraordinary results.
- scope: four fundamental problems that come up when one person leads a team of AI agents
- provides-wrappers: value-added wrappers around native AI services
- provides-mcp: a range of MCP services
- provides-web-interface: a web interface for managing agent interactions and multiple projects (workspaces), each with their own agent profiles and capabilities
- problem-memory: an agent starts each session without what the team learned before, and even when a memory store exists it may answer without consulting it
- solution-memory-storage: specs, decisions and each agent's memory live as plain-text FactLattice files that factlattice-engine can query
- model-independence: the memory layer is independent of any model or vendor: FactLattice files are plain text, factlattice-engine runs no model inference, and it serves the graph over MCP, an open protocol, to any MCP client that can launch a local stdio server (measured: Claude Code and OpenAI Codex CLI); an agent built on another model can read and write the same knowledge graph
- harness-scope: only the Gnomon engine harness is tied to one agent today (Claude Code, on macOS); Codex support and Windows and Linux support are planned work in the harness, not limits of the memory layer
- solution-memory-rendering: each agent's definition is rendered at launch with its memory inlined, and a failed expansion is shown loudly
- problem-ambiguity: given an unclear spec, or too little context, an agent may guess silently
- solution-ambiguity-document: the agent puts the choice to the pilot as a decision document, with options, tradeoffs and a recommendation
- solution-ambiguity-answer: the pilot's answer is recorded and delivered back to the agent
- problem-agent-behaviour: a confident report can rest on a check that never ran
- solution-agent-behaviour-record: the harness records every action it takes with its source
- solution-agent-behaviour-status: status is reported from evidence about the live object
- solution-agent-behaviour-review: every change is reviewed by someone who did not write it
- problem-synthesis: what a decision needs is scattered across many documents
- solution-synthesis: decisions, specs and the links between them form one graph that factlattice-engine can follow, so an agent can gather what bears on a choice
- design-principles: https://github.com/740Dave/gnomon/blob/main/docs/design-principles.md
- design-principles-covers: pillars of outstanding teams (among them compelling purpose, psychological safety, complementary strengths between the human and the agents) and the principles of the pilot's experience
- source: README.md between the gnomon-platform-opening markers, "Why Gnomon Exists"

### [GP-GNOMON-ENGINE] Gnomon engine

- part-of: [GP-PLATFORM]
- repository: https://github.com/740Dave/gnomon
- role: the heart of the platform
- required: for the full experience of the platform
- provides: the harness that runs the team, and the web dashboard the pilot uses to lead it
- status: released
- source: README.md between the gnomon-platform-opening markers, "The projects that make up the Gnomon Platform", Gnomon engine row
- source-status: README.md of https://github.com/740Dave/gnomon, written for its first public release

### [GP-FACTLATTICE-ENGINE] factlattice-engine

- part-of: [GP-PLATFORM]
- repository: https://github.com/740Dave/factlattice
- service-name: `lts-engine`
- role: the team's memory and shared knowledge
- provides: a memory graph agents can query, traverse and update over MCP
- storage: plain-text FactLattice (`.lts`) files that people can read, diff and version
- use-in-definitions: agent definitions embed factlattice-engine queries for essential knowledge
- use-by-agents: agents query anything else when they need it, and can update their own or the team's shared memory graph
- write-visibility: the next query sees the change
- model-independence: no model inference in the engine; any agent, of any model or vendor, whose MCP client can launch a local stdio server can use the same graph (measured: Claude Code and OpenAI Codex CLI); a client limited to remote MCP servers over HTTP needs a bridge; the files themselves need no engine at all to read
- measured-other-client: on 2026-10-28 the maintainers ran OpenAI Codex CLI 0.164.0 (a GPT-6 model) against its own factlattice-engine MCP server process, with the same code and registry, and so the same graph, as a Claude Code session; Codex fetched a node with all its properties, traversed its edges, and wrote a new node through the typed writer, and the Claude Code session then read back exactly what Codex wrote (Codex needs the server's tools approved in its configuration)
- os: POSIX; the MCP server, `call` command line and typed writers import `fcntl`, so not Windows; the optional always-on embedder uses launchd (macOS only); the repository records testing on macOS only
- status: draft release
- readme-status: FactLattice 1.0 — DRAFT; notation and four engine layers implemented and tested
- source: README.md between the gnomon-platform-opening markers, "The projects that make up the Gnomon Platform", factlattice-engine row
- source-status: README.md of https://github.com/740Dave/factlattice, "Status"
- source-service-name: README.md of https://github.com/740Dave/factlattice, engine description

### [GP-DECISION-ENGINE] Decision engine

- part-of: [GP-PLATFORM]
- repository: https://github.com/740Dave/decision-engine
- provides: decision-support documents (DSDs) and the decisions-made graph
- role: a single, consistent way for multiple agents to ask the pilot for decisions
- storage: every decision stored persistently in FactLattice files that factlattice-engine can query
- status: placeholder
- source: README.md between the gnomon-platform-opening markers, "The projects that make up the Gnomon Platform", Decision engine row
- source-status: README.md of https://github.com/740Dave/decision-engine, "This repository" ("Coming soon.")

### [GP-GNOMON-PLUGINS] Gnomon plugins

- part-of: [GP-PLATFORM]
- repository: https://github.com/740Dave/gnomon-plugins
- kinds: platform-wide plugins and workspace-specific plugins
- role: a library of optional, platform-wide capability enhancements
- workspace-plugins: typically developed by users to meet a particular project's needs
- status: placeholder
- source: README.md between the gnomon-platform-opening markers, "The projects that make up the Gnomon Platform", Gnomon plugins row
- source-status: README.md of https://github.com/740Dave/gnomon-plugins, "This repository" ("Coming soon.")

### Which parts of the Gnomon Platform to use: a decision matrix [GP-ADOPTION-MATRIX]

- part-of: [GP-PLATFORM]
- kind: decision-matrix
- question: which projects of the Gnomon Platform does a given need call for
- rule: read the rows in order; use the first row whose need matches; the status column says whether the project can be used today
- row-1-need: only a structured way for agents to ask a human for decisions, and a record of the answers
- row-1-use: [GP-DECISION-ENGINE]; it writes plain FactLattice files, and [GP-FACTLATTICE-ENGINE] is optional, for querying them
- row-1-status: not available yet: the repository is a placeholder
- row-2-need: only a memory graph agents can query, traverse and write, kept as plain-text files
- row-2-use: [GP-FACTLATTICE-ENGINE] alone, as a Python library, a command line, or an MCP server registered in an MCP client; no other platform project is needed
- row-2-status: draft release
- row-3-need: to lead a team of Claude Code agents on one Mac, with shared memory, decision documents and a web dashboard
- row-3-use: [GP-GNOMON-ENGINE] with [GP-FACTLATTICE-ENGINE]; [GP-DECISION-ENGINE] for decisions once it is published
- row-3-status: Gnomon engine released; factlattice-engine draft release; Decision engine not available yet
- row-4-need: optional extras such as printing, PDF handling or attention lights
- row-4-use: [GP-GNOMON-PLUGINS], which needs [GP-GNOMON-ENGINE]
- row-4-status: not available yet: the repository is a placeholder
- row-5-need: an agent or model other than Claude Code, for example OpenAI Codex
- row-5-use: for memory, [GP-FACTLATTICE-ENGINE] today: any MCP client that can launch a local stdio server can query, traverse and write the same graph, with no dependency on Claude Code (see its measured-other-client line); to run the team in a harness, [GP-GNOMON-ENGINE] supports Claude Code only today
- row-5-status: factlattice-engine: usable from MCP clients that launch local stdio servers, two measured (draft release); Gnomon engine: Claude Code only, Codex support stated as in progress in its README
- row-6-need: an operating system other than macOS
- row-6-use: [GP-FACTLATTICE-ENGINE] is POSIX: its MCP server, `call` command line and typed writers import the POSIX-only `fcntl` module, so they cannot run on Windows; its optional always-on embedder uses launchd, which is macOS only; the repository records no testing outside macOS; [GP-GNOMON-ENGINE] requires macOS
- row-6-status: Gnomon engine: macOS only, Windows and Linux support stated as planned in its README; factlattice-engine: not Windows, other POSIX systems untested
- source: the status and role lines of the project nodes above; README.md of https://github.com/740Dave/gnomon, Requirements; README.md of https://github.com/740Dave/decision-engine, This repository; factlattice/authoring/edit.py of https://github.com/740Dave/factlattice (the fcntl import)
<!-- gnomon-platform-lts:end -->

## [GPL-REPO] Gnomon plugins repository

- part-of: [GP-PLATFORM]
- status: placeholder
- readme-state: Coming soon.
- purpose: optional plugins for the Gnomon Platform; each adds a capability without changing the Gnomon engine
- planned-print-verbs: printing, with a provider for each printer
- planned-pdf-verbs-create: creating PDFs from Markdown
- planned-pdf-verbs-extract: extracting text from PDFs
- planned-pdf-verbs-default: a bundled permissively licensed default, and a documented connector for another PDF library
- planned-led-attention-lights: drives a small LED array that shows which agent needs the pilot
- not-here: core file handling (open, archive, copy) is part of the Gnomon engine, because it shares the engine's safety rules
- source: README.md of https://github.com/740Dave/gnomon-plugins, "This repository"

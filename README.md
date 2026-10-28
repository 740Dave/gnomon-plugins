# The Gnomon Platform: Gnomon-Plugins Repo

<!-- gnomon-platform-opening:start -->
**The Gnomon Platform makes it easy to lead an outstanding AI team that remembers, collaborates with you and produces extraordinary results.**

## Why Gnomon Exists

The Gnomon Platform is built to address four fundamental problems that come up when one person leads a team of AI agents. By so doing, the Gnomon Platform enables more effective collaboration between humans and AI team members. This extensible platform provides value-added wrappers around native AI services, enables a range of MCP services, and provides a web interface for managing agent interactions and multiple projects (workspaces), each with their own agent profiles and capabilities.

| Problem | What the Gnomon Platform does about it |
|---|---|
| **Memory.** An agent starts each session without what the team learned before, and even when a memory store exists it may answer without consulting it. | Specs, decisions and each agent's memory live as plain-text FactLattice files that factlattice-engine can query. Each agent's definition is rendered at launch with its memory inlined, and a failed expansion is shown loudly. |
| **Ambiguity.** Given an unclear spec, or too little context, an agent may guess silently. | The agent puts the choice to you as a decision document, with options, tradeoffs and a recommendation. Your answer is recorded and delivered back to the agent. |
| **Agent behaviour.** A confident report can rest on a check that never ran. | The harness records every action it takes with its source, status is reported from evidence about the live object, and every change is reviewed by someone who did not write it. |
| **Synthesis.** What a decision needs is scattered across many documents. | Decisions, specs and the links between them form one graph that factlattice-engine can follow, so an agent can gather what bears on a choice. |

The results are expected, not yet measured.

The Gnomon design principles ([design-principles](https://github.com/740Dave/gnomon/blob/main/docs/design-principles.md)) also describe the pillars of outstanding teams that the platform builds on (among them compelling purpose, psychological safety, and complementary strengths between the human and the agents) and the principles of the pilot's experience. If you find Gnomon useful and are curious about its approach to human-AI collaboration, that document is worth a read.

## The projects that make up the Gnomon Platform

| Project | What it does for the team | Repository |
|---|---|---|
| **Gnomon engine:** The heart of the platform, and required for the full experience | The harness that runs the team, and the web dashboard you, the pilot, use to lead it. | https://github.com/740Dave/gnomon |
| **factlattice-engine:** A service that reads static FactLattice (*.lts) files to form a queryable and traversable graph that is accessible via MCP interfaces. | The team's memory and shared knowledge. Agent definitions embed factlattice-engine queries for essential knowledge; agents query anything else when they need it, and can update their own or the team's shared memory graph in real time. | https://github.com/740Dave/factlattice |
| **Decision engine:** decision-support documents (DSDs) and the decisions-made graph | A single, consistent way for multiple agents to ask you for decisions, with every decision you make stored persistently in FactLattice files that factlattice-engine can query. | https://github.com/740Dave/decision-engine |
| **Gnomon plugins:** Gnomon supports platform-wide plugins and workspace-specific plugins. | A library of optional, platform-wide capability enhancements. Workspace-specific plugins are typically developed by users to meet a particular project's needs. | https://github.com/740Dave/gnomon-plugins |

<!-- gnomon-platform-opening:end -->

## This repository

Optional plugins for the Gnomon Platform will live here. Each one adds a capability without changing the Gnomon engine itself.

Planned first plugins:

- **print-verbs:** printing, with a provider for each printer.
- **pdf-verbs:** creating PDFs from Markdown and extracting text from PDFs, with a bundled permissively licensed default and a documented connector for anyone who prefers another PDF library.
- **LED attention lights:** drives a small LED array that shows which agent needs you.

Core file handling (open, archive, copy) is part of the Gnomon engine, not this repository, because it shares the engine's safety rules.

Coming soon.

#WebnovelWriter

[![License](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Compatible-purple.svg)](https://claude.ai/claude-code)

<a href="https://trendshift.io/repositories/22487" target="_blank"><img src="https://trendshift.io/api/badge/repositories/22487" alt="lingfengQAQ%2Fwebnovel-writer | Trendshift style="width: 250px; height: 55px;" width="250" height="55"/></a>

## Project Introduction

`Webnovel Writer` is a long-form online novel creation system based on Claude Code. Its goal is to reduce "forgetting" and "illusion" in AI writing and support long-term serialized creation.

Detailed documentation has been split into `docs/`:

- Architecture and Modules: `docs/architecture.md`

- Command Details: `docs/commands.md`

- RAG and Configuration: `docs/rag-and-config.md`

- Theme Templates: `docs/genres.md`

- Operations and Recovery: `docs/operations.md`

- Documentation Navigation: `docs/README.md`

## Quick Start

### 1) Install Plugin (Official Marketplace)

```bash
claude plugin marketplace add lingfengQAQ/webnovel-writer --scope user
claude plugin install webnovel-writer@webnovel-writer-marketplace --scope user

```
> To only apply to the current project, change `--scope user` to `--scope project`.

### 2) Install Python Dependencies

```bash
python -m pip install -r https://raw.githubusercontent.com/lingfengQAQ/webnovel-writer/HEAD/requirements.txt

```
Note: This entry point will install both the core writing pipeline and Dashboard dependencies.

### 3) Initialize the Novel Project

Execute in Claude Code:

```bash
/webnovel-init

```
Note: `/webnovel-init` will create a `PROJECT_ROOT` (subdirectory) under the current Workspace based on the book title, and write the current project pointer to `workspace/.claude/.webnovel-current-project`.

### 4) Configure the RAG Environment (Required)

Go to the root directory of the initialized book project and create a `.env` file:

```bash

cp .env.example .env

```

Minimum Configuration Example:

```bash

EMBED_BASE_URL=https://api-inference.modelscope.cn/v1

EMBED_MODEL=Qwen/Qwen3-Embedding-8B

EMBED_API_KEY=your_embed_api_key

RERANK_BASE_URL=https://api.jina.ai/v1

RERANK_MODEL=jina-reranker-v3

RERANK_API_KEY=your_rerank_api_key

```

### 5) Get Started

```bash

/webnovel-plan 1

/webnovel-write 1

/webnovel-review 1-5

```

To troubleshoot local CLI/plugin directory/project root resolution issues, you can directly run the unified preflight check:

```bash
python -X utf8 "<CLAUDE_PLUGIN_ROOT>/scripts/webnovel.py" --project-root "<WORKSPACE_ROOT>" preflight

```

### 6) Launch the Visualization Panel (Optional)

```bash
/webnovel-dashboard

```

Note:

- The Dashboard is a read-only panel (project status, entity graph, chapter/outline browsing, and follow-up view).

- The front-end build artifacts have been released with the plugin; users do not need to run `npm build` locally.

### 7) Agent Model Settings (Optional)

The default configuration for all built-in Agents in this project is:

```yaml
model: inherit

```
This indicates that the child Agent inherits the model used by the current Claude session.

` ... To assign a model to a specific Agent, edit the frontmatter of the corresponding file (`webnovel-writer/agents/*.md`), for example:

```yaml

---
name: context-agent

description: ...

tools: Read, Grep, Bash

model: sonnet

---
```

Common possible values: `inherit` / `sonnet` / `opus` / `haiku` (based on current Claude Code support).

## Update Summary

| Version | Description |

|------|------|

| **v5.5.4 (Current)** | Added strong constraints to the writing chain prompts (hard constraints on processes, constraints on Chinese thinking and writing, step responsibility boundaries); unified the Chinese-language review/polishing/Agent report text; cleaned up the internal version number and version history of the document to reduce confusion with plugin release versions. | | **v5.5.3** | Added a unified `preflight` preflight command; unified the writing chain CLI examples to UTF-8, eliminated long shell preflight snippets in the documentation, and reduced the risk of garbled characters in the Windows terminal. |

| **v5.5.2** | Supports synchronizing chapter names from detailed outlines to the main file names; fixed compatibility issues with workflow_manager under the parameterless find_project_root monkeypatch. |

| **v5.5.1** | Fixed the issue of extracting chapters from volume-level single-file outlines in context snapshots; added `/webnovel-dashboard` and `/webnovel-learn` to the command documentation. | | **v5.5.0** | Added read-only visual Dashboard Skill (`/webnovel-dashboard`) and real-time refresh capability; supports plugin directory startup and pre-built frontend distribution. |

| **v5.4.4** | Introduced the official Plugin Marketplace installation mechanism; unified fixes for CLI calls to Skills/Agents/References (single path `CLAUDE_PLUGIN_ROOT`, unified pass-through command `--`). |

| **v5.4.3** | Enhanced intelligent RAG context assistance (`auto/graph_hybrid` rollback to BM25). |

| **v5.3** | Introduced a tracking system (Hook / Cool-point / Micro-cashout / Debt tracking). |

## Plugin Release

Recommended to use the `Plugin Release` workflow on GitHub Actions for unified release:

1. First, synchronize version information locally:

``bash
python -X utf8 `webnovel-writer/scripts/sync_plugin_version.py --version 5.5.4 --release-notes "Release Notes"`

``
2. Commit and push version changes (`README.md`, `plugin.json`, `marketplace.json`).

3. Open the repository's Actions page and select `Plugin Release`.

4. Enter the `version` (e.g., `5.5.4`) that matches the current repository's metadata and the `release_notes` for the GitHub Release.

5. The workflow will perform the following actions:

- Verify that `plugin.json` and `marketplace.json` match the current version in the README.

- Verify that the current version matches the entered `version`.

- Create and push the `vX.Y.Z` tag.

- Create a GitHub Release with the same name.

In daily development, `Plugin Version Check` will automatically check the version information for consistency when pushing/PRs.

``` ## Open Source License

This project is licensed under the `GPL v3` ​​license. See `LICENSE` for details.

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=lingfengQAQ/webnovel-writer&type=Date)](https://star-history.com/#lingfengQAQ/webnovel-writer&Date)

## Acknowledgements

This project was developed using **Claude Code + Gemini CLI + Codex** in conjunction with Vibe Coding.

Inspiration: [Linux.do post](https://linux.do/t/topic/1397944/49)

## Contributions

Issues and PRs are welcome:

```bash
git checkout -b feature/your-feature
git commit -m "feat: add your feature"
git push origin feature/your-feature
```

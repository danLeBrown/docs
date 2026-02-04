# Agent Guide: docs.prvue.dev

This document is for AI agents and contributors starting a new session. It summarizes what docs.prvue.dev is, what was done to set it up, and how to work in this repo.

---

## 1. Purpose of this repo

- **docs.prvue.dev** is the **documentation repository** for **Preview Deployer**.
- **Preview Deployer** is the main project (lives in a separate repo: `preview-deployer`). It creates isolated preview environments for backend apps when GitHub PRs are opened (Terraform, Ansible, orchestrator, CLI).
- This repo **only** holds the docs. The docs are built with **Mintlify** and published at **docs.prvue.dev** (or run locally with `mintlify dev`).
- **Do not** put application code here. All content is MDX/Markdown and config (`docs.json`, etc.).

---

## 2. What was discussed and the plan we executed

We executed the plan from **Mintlify Documentation for Preview Deployer** (e.g. `mintlify_docs_for_preview_deployer_*.plan.md`). Summary:

- **Goal**: Set up a Mintlify doc site for Preview Deployer, migrate existing markdown docs into it, and add an Examples section for the five example repos (NestJS, Laravel, Go, Python, Rust).
- **Location**: All doc **file changes** were made in **docs.prvue.dev** (this repo). The **preview-deployer** repo only had its README updated to link to this docs site.
- **Conventions**: We followed **docs.prvue.dev/.cursor/rules.md** (Mintlify components, frontmatter, tone) and the plan’s nav/structure.

---

## 3. Steps we took (what exists now)

| Step | What was done |
|------|----------------|
| **1. Mintlify config** | **docs.json** updated for Preview Deployer: name "Preview Deployer", single "Guides" tab with groups: Getting Started, Guides, Examples, Operations, Reference. Colors, favicon, logo, navbar (GitHub button). |
| **2. Intro page** | **index.mdx** rewritten as Preview Deployer intro: value prop, cards to Quickstart/Configuration/Architecture/Examples, next steps. |
| **3. Root docs (migrated)** | Five docs migrated from **preview-deployer/docs/** to MDX in this repo with internal links fixed to Mintlify paths: **quickstart.mdx**, **configuration.mdx**, **architecture.mdx**, **testing.mdx**, **troubleshooting.mdx**. |
| **4. Examples section** | **examples/index.mdx** (overview, supported vs custom compose) + **examples/nestjs.mdx**, **laravel.mdx**, **go.mdx**, **python.mdx**, **rust.mdx** (one page per example repo; key files, config snippets, links to READMEs). |
| **5. Reference section** | **reference/orchestrator-how-it-works.mdx**, **reference/implementation-plan.mdx**, **reference/agent-handoff-prompt.mdx**, **reference/documentation-guide.mdx** (rules and standards for writing docs). |
| **6. llm.txt** | **llm.txt** at repo root: plain-language map of Preview Deployer, doc site sections, main repo and example repos, note for AI tools to keep it updated. |
| **7. preview-deployer README** | In the **preview-deployer** repo: Documentation section now points to **docs.prvue.dev** and lists Quickstart, Architecture, Configuration, Examples, Testing, Troubleshooting with links to this site. Quick Start and Testing links updated to use docs.prvue.dev. |
| **8. docs.prvue.dev README** | **README.md** in this repo rewritten for the docs repo: purpose, contents, development (`mintlify dev`), publishing, contributing (link to Documentation guide and `.cursor/rules.md`), resources. |

---

## 4. Repo structure (what lives where)

```
docs.prvue.dev/
├── .cursor/
│   ├── rules.md          # Mintlify + technical writing rules (required reading for edits)
│   └── agent-guide.md    # This file — context and handoff for agents
├── docs.json             # Mintlify config: name, nav, colors, logo, navbar
├── index.mdx             # Homepage (Preview Deployer intro)
├── quickstart.mdx        # Getting started
├── configuration.mdx     # Config reference
├── architecture.mdx      # System design
├── testing.mdx           # Testing guide
├── troubleshooting.mdx   # Troubleshooting
├── examples/
│   ├── index.mdx         # Examples overview
│   ├── nestjs.mdx
│   ├── laravel.mdx
│   ├── go.mdx
│   ├── python.mdx
│   └── rust.mdx
├── reference/
│   ├── orchestrator-how-it-works.mdx
│   ├── implementation-plan.mdx
│   ├── agent-handoff-prompt.mdx
│   └── documentation-guide.mdx
├── llm.txt               # AI-facing map of project and doc site (keep in sync)
├── README.md             # Repo readme (development, contributing)
├── favicon.svg
├── logo/
├── images/
└── (legacy Mintlify starter files: ai-tools/, api-reference/, essentials/, development.mdx, snippets/ — not in nav; can be removed or repurposed)
```

- **Navigation** is defined only in **docs.json** under `navigation.tabs[].groups`. A page must be listed there to appear in the sidebar.
- **Internal links** in MDX must use Mintlify paths (e.g. `/configuration`, `/examples/nestjs`, `/reference/implementation-plan`), not `.md`/`.mdx` or relative file paths.

---

## 5. Key files for agents

| File | Purpose |
|------|--------|
| **.cursor/agent-guide.md** | This file. Read first in a new session for context and handoff. |
| **.cursor/rules.md** | Mintlify components, frontmatter, tone, structure. Follow when editing or adding pages. |
| **docs.json** | Nav and site config. Add new pages here when you create new content. |
| **llm.txt** | High-level map for AI. Update when you add sections, example repos, or restructure. |
| **reference/documentation-guide.mdx** | User- and contributor-facing rules (structure, examples, reference, internal links, MDX, llm.txt). Point contributors here. |

---

## 6. Two repos: preview-deployer vs docs.prvue.dev

| Repo | Role |
|------|------|
| **preview-deployer** | Application: Terraform, Ansible, orchestrator, CLI, templates. **Source of truth for product behavior.** Docs *content* was originally in `preview-deployer/docs/` (markdown); we **migrated** that content into docs.prvue.dev and fixed links. preview-deployer README now **links to** docs.prvue.dev. |
| **docs.prvue.dev** | Documentation only. Mintlify site; all published doc content lives here. No app code. |

- When documenting **product behavior, config, or architecture**, the **source of truth** is the preview-deployer repo (code, `preview-deployer/docs/` if anything remains). This repo is the **published doc site**.
- When adding or changing **doc pages, nav, or doc conventions**, work in **docs.prvue.dev** and follow **.cursor/rules.md** and **reference/documentation-guide.mdx**.

---

## 7. How to add or change content

1. **New page**: Create the `.mdx` file (with `title` and `description` frontmatter), add it to the appropriate group in **docs.json** under `navigation.tabs[].groups`. Use Mintlify paths for internal links. If the new page changes the “map” of the site, update **llm.txt**.
2. **New example repo**: Add `examples/{name}.mdx` (e.g. `examples/nestjs.mdx`), add the page to the Examples group in **docs.json**, update **examples/index.mdx** and **llm.txt**.
3. **New reference page**: Add `reference/{name}.mdx`, add to Reference group in **docs.json**, update **llm.txt** if needed.
4. **Edits to existing pages**: Edit the `.mdx` file; keep internal links as Mintlify paths and frontmatter valid. No need to change **docs.json** unless you rename or remove a page.

---

## 8. Quick start for the next agent session

1. **Read this file** (`.cursor/agent-guide.md`) for context and what was done.
2. **Read** `reference/documentation-guide.mdx` (in the doc site or in this repo) for structure and writing rules.
3. **Read** `.cursor/rules.md` before editing or adding MDX (frontmatter, components, tone).
4. **Use** `llm.txt` as the high-level map; update it when you add sections, example repos, or restructure.
5. **Run** `mintlify dev` at repo root to preview changes locally.

This gives the next agent session enough context to continue doc work in docs.prvue.dev without re-deriving the setup or conventions.

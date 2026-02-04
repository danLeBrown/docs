# Preview Deployer Documentation

This repository contains the official documentation for [Preview Deployer](https://github.com/danLeBrown/preview-deployer)—automated preview deployment for backend applications on GitHub PRs. The site is built with [Mintlify](https://mintlify.com) and published at **docs.prvue.dev**.

## Contents

- **Getting Started**: Introduction, Quickstart
- **Guides**: Configuration, Architecture
- **Examples**: NestJS, Laravel, Go, Python, Rust example repos
- **Operations**: Testing, Troubleshooting
- **Reference**: Orchestrator internals, Implementation plan, Agent handoff, Documentation guide

## Development

Install the [Mintlify CLI](https://www.npmjs.com/package/mintlify) and run the dev server from this repo root:

```bash
npm i -g mintlify
mintlify dev
```

Open **http://localhost:3000** to preview the docs. Edits to MDX files and `docs.json` hot-reload.

**Note:** If the dev server fails, run `mintlify update` to ensure you have the latest CLI. If a page 404s, confirm you're in the repo root where `docs.json` lives.

## Publishing

Deployments are typically triggered by your host (e.g. Mintlify dashboard, or CI). Push changes to the default branch; the published site at docs.prvue.dev updates according to your deployment setup.

## Contributing to the docs

- Follow the [Documentation guide](https://docs.prvue.dev/reference/documentation-guide) for structure, Examples/Reference standards, internal links, and when to update `llm.txt`.
- Use the Mintlify and technical writing rules in [.cursor/rules.md](.cursor/rules.md) (frontmatter, components, tone).

## Resources

- [Preview Deployer repo](https://github.com/danLeBrown/preview-deployer)
- [Mintlify docs](https://mintlify.com/docs)

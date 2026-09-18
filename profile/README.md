# OpenPencil

Open-source design editor built on one premise: **a design is a node tree,
not a picture.**

Design tools treat the canvas as the product and the file as an
implementation detail — a proprietary binary only the vendor's software can
fully read, behind APIs that fight automation. OpenPencil inverts that. The
document is a node tree you can open, query, transform, lint, and diff; the
editor is one client of it. A designer moves things on the canvas; a script
renames every color token; an AI agent builds a screen — all through the
same small set of operations, and each change is data you can review like a
code change.

It opens Figma's `.fig` files natively, runs as a ~15 MB desktop app or a
browser tab, and never sends your files to any server — only to peers you
share with or an AI provider you connect. The editor, the engine, the file
codec, the CLI, the MCP server, and the Vue SDK are all MIT.

```sh
brew install --cask openpencil
```

Or [use the web app](https://app.openpencil.dev) — no install, no account.

**[Try it online](https://app.openpencil.dev/demo)** ·
[Download](https://github.com/open-pencil/open-pencil/releases/latest) ·
[Documentation](https://openpencil.dev) ·
[Roadmap](https://openpencil.dev/development/roadmap)

## Start here

| Project | What it is |
| --- | --- |
| [open-pencil](https://github.com/open-pencil/open-pencil) | The editor — desktop and web app — with the engine, CLI, MCP server, Vue SDK, and the [agent skill](https://github.com/open-pencil/open-pencil/tree/master/skills/open-pencil) (`npx skills add open-pencil/open-pencil`) |

The same repository publishes the programmable surface to npm:

| Package | What it does |
| --- | --- |
| [@open-pencil/core](https://www.npmjs.com/package/@open-pencil/core) | Editor engine — renderer, layout, document I/O, Figma API, tools, and RPC |
| [@open-pencil/scene-graph](https://www.npmjs.com/package/@open-pencil/scene-graph) | Scene graph nodes, primitives, hit testing, copy/snap/undo, variants, and vector-network types |
| [@open-pencil/kiwi](https://www.npmjs.com/package/@open-pencil/kiwi) | Kiwi binary runtime, Figma schema helpers, and low-level `.fig` container parsing |
| [@open-pencil/fig](https://www.npmjs.com/package/@open-pencil/fig) | `.fig` archives — SceneGraph conversion, instances, and metadata |
| [@open-pencil/pen](https://www.npmjs.com/package/@open-pencil/pen) | `.pen` document parser and SceneGraph adapter |
| [@open-pencil/dom-css](https://www.npmjs.com/package/@open-pencil/dom-css) | HTML/CSS/Tailwind conversion into editable design documents |
| [@open-pencil/vue](https://www.npmjs.com/package/@open-pencil/vue) | Headless Vue SDK for embedding OpenPencil or building custom editors |
| [@open-pencil/cli](https://www.npmjs.com/package/@open-pencil/cli) | Headless CLI — inspect, query (XPath), lint, analyze, export, convert, and import `.fig`/`.pen` files; run Figma plugin API scripts; control the running editor over RPC |
| [@open-pencil/mcp](https://www.npmjs.com/package/@open-pencil/mcp) | MCP server (stdio + HTTP) — 100+ design tools for Claude Code, Cursor, Windsurf, and any MCP client |
| [@open-pencil/harness](https://www.npmjs.com/package/@open-pencil/harness) | Optional companion CLI for coding-agent Harness sessions |

## Around the editor

| Project | What it does |
| --- | --- |
| [twirlwind](https://github.com/open-pencil/twirlwind) | Tailwind v4-first CSS-to-utility-class serializer, used by JSX/Tailwind export |
| [git-lfs-s3-proxy](https://github.com/open-pencil/git-lfs-s3-proxy) | Provider-neutral Git LFS gateway for S3-compatible storage; serves the repository's fixtures |

## Elixir

The same document model from the BEAM, for services and pipelines that read design files without the editor:

| Project | What it does |
| --- | --- |
| [figler](https://github.com/open-pencil/figler) | Analyze, transform, and render Figma files from Elixir |
| [kiwi_codec](https://github.com/open-pencil/kiwi_codec) | Pure Elixir codec for Kiwi schema binary messages |

## Engine infrastructure

The rendering and layout stack OpenPencil runs on, maintained here:

| Project | What it does |
| --- | --- |
| [canvaskit-webgpu](https://github.com/open-pencil/canvaskit-webgpu) | CanvasKit WASM build with Skia Graphite + Dawn (WebGPU) backend |
| [skia](https://github.com/open-pencil/skia) | Skia fork carrying the Graphite/Dawn CanvasKit patches |
| [yoga](https://github.com/open-pencil/yoga) | Yoga fork with CSS Grid support, powering auto layout |

## How it fits together

```text
.fig / .pen document (node tree)
├── editor                  — desktop (Tauri) and web app, real-time P2P collaboration
├── @open-pencil/core       — editor engine, renderer, layout, tools, RPC, document I/O
├── @open-pencil/scene-graph — nodes, primitives, hit testing, copy/snap/undo
├── @open-pencil/kiwi       — Kiwi runtime and low-level .fig container parsing
├── @open-pencil/fig        — focused .fig package entrypoint
├── @open-pencil/pen        — Pencil document format helpers
├── @open-pencil/dom-css    — HTML/CSS/Tailwind to editable design documents
├── @open-pencil/cli        — tree / query / lint / analyze / export / eval from the terminal
├── @open-pencil/mcp        — the same operations as MCP tools for AI agents
└── @open-pencil/vue        — headless components for building your own editor
```

Every surface — canvas, CLI, MCP, SDK — drives the same operations on the
same tree. That is the whole design: nothing the editor can do is closed to
a script, and nothing a script does bypasses what the editor checks.

OpenPencil is also the design layer of a larger open stack — a web stack
built so that software written by AI (and by people) can be checked, not
just generated. The argument and the map live in
**[Building Blocks for the Future Web](https://github.com/elixir-vibe/building-blocks)**.

## License

MIT across the organization, except `skia` (BSD-3-Clause, as upstream) and
`git-lfs-s3-proxy` (CC0).

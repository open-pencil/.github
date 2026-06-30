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

It opens Figma's `.fig` files natively, runs as a ~7 MB desktop app or a
browser tab, and never sends your files anywhere. The editor, the engine,
the file codec, the CLI, the MCP server, and the Vue SDK are all MIT.

```sh
brew install open-pencil/tap/open-pencil
```

Or [use the web app](https://app.openpencil.dev) — no install, no account.

**[Try it online](https://app.openpencil.dev/demo)** ·
[Download](https://github.com/open-pencil/open-pencil/releases/latest) ·
[Documentation](https://openpencil.dev) ·
[Roadmap](https://openpencil.dev/development/roadmap)

## Start here

| Project | What it is |
| --- | --- |
| [open-pencil](https://github.com/open-pencil/open-pencil) | The editor — desktop and web app, plus the engine, CLI, MCP server, and Vue SDK as workspace packages |

The same repository publishes the programmable surface to npm:

| Package | What it does |
| --- | --- |
| [@open-pencil/core](https://www.npmjs.com/package/@open-pencil/core) | Editor engine — renderer, layout, document I/O, Figma API, tools, and RPC |
| [@open-pencil/scene-graph](https://www.npmjs.com/package/@open-pencil/scene-graph) | Scene graph nodes, primitives, hit testing, copy/snap/undo, variants, and vector-network types |
| [@open-pencil/kiwi](https://www.npmjs.com/package/@open-pencil/kiwi) | Kiwi binary runtime, Figma schema helpers, and low-level `.fig` container parsing |
| [@open-pencil/fig](https://www.npmjs.com/package/@open-pencil/fig) | Focused `.fig` package entrypoint |
| [@open-pencil/pen](https://www.npmjs.com/package/@open-pencil/pen) | Pencil document format helpers |
| [@open-pencil/dom-css](https://www.npmjs.com/package/@open-pencil/dom-css) | HTML/CSS/Tailwind conversion into editable design documents |
| [@open-pencil/vue](https://www.npmjs.com/package/@open-pencil/vue) | Headless Vue SDK for embedding OpenPencil or building custom editors |
| [@open-pencil/cli](https://www.npmjs.com/package/@open-pencil/cli) | Headless CLI — inspect, query (XPath), lint, analyze, export, and convert `.fig`/`.pen` files; control the running editor over RPC |
| [@open-pencil/mcp](https://www.npmjs.com/package/@open-pencil/mcp) | MCP server (stdio + HTTP) — 100+ design tools for Claude Code, Cursor, Windsurf, and any MCP client |

## Around the editor

| Project | What it does |
| --- | --- |
| [skills](https://github.com/open-pencil/skills) | Agent skills — teach AI coding agents to inspect, modify, and export design files |
| [homebrew-tap](https://github.com/open-pencil/homebrew-tap) | Homebrew tap for the desktop app |
| [twirlwind](https://github.com/open-pencil/twirlwind) | Tailwind v4-first CSS-to-utility-class serializer, used by JSX/Tailwind export |

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

MIT across the organization. Forks (`skia`, `yoga`) keep their upstream
licenses.

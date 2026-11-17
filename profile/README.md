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

It opens Figma's `.fig` files natively, turns HTML/CSS into editable layers,
and runs as a ~15 MB desktop app or a browser tab. Your files stay on your
machine unless you send them somewhere: to peers you share with, an AI
provider you connect, or an OpenPencil Cloud server — your team's own, or the
hosted one once it opens. The editor, the engine, the file codecs, the CLI, the MCP server,
and the Vue SDK are MIT; the Cloud server is Apache 2.0.

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
| [@open-pencil/vue](https://www.npmjs.com/package/@open-pencil/vue) | Headless Vue SDK for embedding OpenPencil or building custom editors |
| [@open-pencil/cli](https://www.npmjs.com/package/@open-pencil/cli) | Headless CLI — inspect, query (XPath), lint, analyze, export, convert, and import `.fig`/`.pen` files and HTML; run Figma plugin API scripts; control the running editor over RPC |
| [@open-pencil/mcp](https://www.npmjs.com/package/@open-pencil/mcp) | MCP server (stdio + HTTP) — 100+ design tools for Claude Code, Cursor, Windsurf, and any MCP client |
| [@open-pencil/cloud](https://www.npmjs.com/package/@open-pencil/cloud) | Self-hostable OpenPencil Cloud — accounts, workspaces, revisions, sharing, and collaboration, for Node and Cloudflare Workers |
| [@open-pencil/harness](https://www.npmjs.com/package/@open-pencil/harness) | Optional companion CLI for coding-agent Harness sessions |

File formats and conversions:

| Package | What it does |
| --- | --- |
| [@open-pencil/kiwi](https://www.npmjs.com/package/@open-pencil/kiwi) | Kiwi binary runtime, Figma schema helpers, and low-level `.fig` container parsing |
| [@open-pencil/fig](https://www.npmjs.com/package/@open-pencil/fig) | `.fig` archives — SceneGraph conversion, instances, and metadata |
| [@open-pencil/pen](https://www.npmjs.com/package/@open-pencil/pen) | `.pen` document parser and SceneGraph adapter |
| [@open-pencil/drawio](https://www.npmjs.com/package/@open-pencil/drawio) | draw.io (diagrams.net) documents, including diagrams embedded in its PNG and SVG exports |
| [@open-pencil/mermaid](https://www.npmjs.com/package/@open-pencil/mermaid) | Mermaid flowcharts read into a typed model |
| [@open-pencil/dom-css](https://www.npmjs.com/package/@open-pencil/dom-css) | HTML/CSS/Tailwind into editable design documents, and designs back to HTML, JSX, and Tailwind |
| [@open-pencil/design-jsx](https://www.npmjs.com/package/@open-pencil/design-jsx) | Design JSX — build editable scene trees with `<Frame>`, `<Text>`, paints, effects, and variables, and export layers back to JSX |
| [@open-pencil/emit](https://www.npmjs.com/package/@open-pencil/emit) | Source emission for exporters — JavaScript, TypeScript, and JSX built as ESTree and printed with esrap |

WebAssembly engines, built in the same repository from the forks below:

| Package | What it does |
| --- | --- |
| [@open-pencil/canvaskit](https://www.npmjs.com/package/@open-pencil/canvaskit) | CanvasKit (Skia in WebAssembly) with Skia's PDF backend — the renderer and PDF export |
| [@open-pencil/taffy](https://www.npmjs.com/package/@open-pencil/taffy) | Taffy flexbox and grid layout in WebAssembly, a whole tree laid out in one call — auto layout |
| [@open-pencil/html-engine](https://www.npmjs.com/package/@open-pencil/html-engine) | HTML laid out as a browser lays it out, without a browser — Blitz (Stylo, Taffy, Parley) in WebAssembly, for HTML import |

## Around the editor

| Project | What it does |
| --- | --- |
| [twirlwind](https://github.com/open-pencil/twirlwind) | Tailwind v4-first CSS-to-utility-class serializer, used by JSX/Tailwind export |
| [whaticon](https://github.com/open-pencil/whaticon) | Find the Iconify icon an SVG draws, by perceptual hash; names the icons HTML import brings in |
| [git-lfs-s3-proxy](https://github.com/open-pencil/git-lfs-s3-proxy) | Provider-neutral Git LFS gateway for S3-compatible storage; serves the repository's fixtures |

## Elixir

The same document model from the BEAM, for services and pipelines that read design files without the editor:

| Project | What it does |
| --- | --- |
| [figler](https://github.com/open-pencil/figler) | Analyze, transform, and render Figma files from Elixir |
| [kiwi_codec](https://github.com/open-pencil/kiwi_codec) | Pure Elixir codec for Kiwi schema binary messages |

## Engine infrastructure

Forks that carry OpenPencil's patches until they land upstream:

| Project | What it does |
| --- | --- |
| [skia](https://github.com/open-pencil/skia) | Skia, built as CanvasKit with the PDF backend (`@open-pencil/canvaskit`) |
| [taffy](https://github.com/open-pencil/taffy) | Taffy with table layout and OpenPencil's layout fixes (`@open-pencil/taffy`) |
| [blitz](https://github.com/open-pencil/blitz) | Blitz with table layout, text baselines, and the table `border` attribute (`@open-pencil/html-engine`) |

## How it fits together

```text
.fig / .pen / HTML / draw.io / Mermaid → node tree
├── editor                   — desktop (Tauri) and web app, real-time collaboration
├── @open-pencil/core        — editor engine: renderer, layout, tools, RPC, document I/O
├── @open-pencil/scene-graph — nodes, primitives, hit testing, copy/snap/undo
├── format packages          — kiwi, fig, pen, drawio, mermaid, dom-css, design-jsx
├── @open-pencil/cli         — tree / query / lint / analyze / export / eval from the terminal
├── @open-pencil/mcp         — the same operations as MCP tools for AI agents
├── @open-pencil/vue         — headless components for building your own editor
└── @open-pencil/cloud       — optional server for documents, sharing, and collaboration
```

Every surface — canvas, CLI, MCP, SDK — drives the same operations on the
same tree. That is the whole design: nothing the editor can do is closed to
a script, and nothing a script does bypasses what the editor checks.

OpenPencil is also the design layer of a larger open stack — a web stack
built so that software written by AI (and by people) can be checked, not
just generated. The argument and the map live in
**[Building Blocks for the Future Web](https://github.com/elixir-vibe/building-blocks)**.

## License

MIT across the organization, except OpenPencil Cloud (Apache 2.0), the forks
that keep their upstream licenses (`skia` BSD-3-Clause, `blitz` MIT or
Apache 2.0), and `git-lfs-s3-proxy` (CC0).

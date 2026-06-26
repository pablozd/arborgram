# Arborgram

**Arborgram** is a web-based syntax tree visualizer. It takes bracket notation as input and renders syntactic trees as SVG in real time.

Designed for teaching and research in generative syntax, morphology, and phonology. Available in Spanish and English.

→ **[arborgram.pablozd.ar](https://arborgram.pablozd.ar)**

## Features

- Single HTML file — no installation or backend required.
- Live SVG rendering as you type.
- Export as SVG or PNG.
- Copy SVG directly to clipboard.
- Spanish / English toggle (persisted across sessions).
- Serif and sans-serif typeface options.
- Configurable font size (8–24 pt), row height, and horizontal spacing.
- Uniform sibling gap option.
- Three branch modes: fixed row height, constant angle, constant length.

## Quick example

Input:

```txt
[SC [SN [Det El][N perro]] [SV [V persigue] [SN al gato negro]]]
```

Output: a labeled syntax tree with branching lines, bold non-terminal labels, and roman terminal nodes.

## Notation

### Basic structure

```txt
[XP node1 node2 ...]
```

Each `[Label ...]` creates a node dominating what follows. Multi-word leaves automatically render as triangles (roofs).

### Label styles

| Notation | Effect |
|---|---|
| `[Cº]` / `[T⁰]` | Bold, no italic (empty heads) — any label ending in `º` `°` `⁰` |
| `["n"P]` / `\i{n}P` | Partial italic within a label (nP, aP, vP) |
| `[__John__]` | Forced italic on the whole node |
| `\i{t}` `\b{t}` `\u{t}` `\s{t}` | Inline italic, bold, underline, strikethrough |
| `t_{i}` | Subscript |

### Movement arrows

```txt
qué%1  ...  t%1
```

`%N` at the end of a label connects two nodes with a curved arrow. Modifiers (combinable in any order):

| Modifier | Effect |
|---|---|
| `.dotted` `.solid` `.dashed` | Line style |
| `.end` `.start` `.both` `.none` | Arrowhead |
| `.blue` `.red` `.#3a7bd5` | Color (palette or hex) |
| `.out30.in-20` | Exit/entry angle in degrees |
| `.dip0.5` | Curve depth (factor of default) |
| `.lbl:Agree` | Label on the arrow (italic); `.left` to move it left |

### Constituent box and strikethrough

```txt
[NP! the black cat]   → dotted box around the constituent
the black cat+        → strikethrough on the leaf (lower copy)
```

### Multidominance

```txt
[TP [DP Juan=1] [T' [T] [vP [DP Juan=1] [v' [v⁰] [VP [V|come]]]]]]
```

`=ID` marks a shared node. The first occurrence is the primary node; the second is the secondary mother. The node is drawn once.

### Multiline labels and AVM

```txt
[V buy|second line]
[V|@CASE:nom;NUM:sg;PERS:3]
```

`|` separates lines within a label. `@` opens a feature matrix (AVM) below the label; `;` = rows, `:` = attribute:value.

### Multiple trees

```txt
[A one] [B two] [C three]
```

Multiple trees separated by space are rendered side by side without a common root.

## Local use

1. Download `arboles.html`.
2. Open it in any modern browser.
3. Type or paste a bracketed structure.
4. Export as SVG or PNG.

No compilation needed.

## Publishing as a static site

The project is a single HTML file and can be served from any static host (GitHub Pages, Nginx, Netlify, Vercel, etc.).

Example with Nginx:

```nginx
server {
    listen 80;
    server_name arborgram.example.com;
    root /var/www/arborgram;
    index arboles.html;
    location / { try_files $uri $uri/ =404; }
}
```

## Project structure

```txt
.
├── arboles.html   ← interface, parser, layout engine, SVG renderer
├── index.html     ← alias for arboles.html
├── CNAME          ← custom domain for GitHub Pages
└── README.md
```

The file `arboles.html` contains everything: UI, CSS, parser, layout, SVG renderer, export and clipboard functions, and i18n strings.

## Customization

Key constants at the top of the script:

```js
const MAX_BRANCH_ANGLE_DEG = 38;  // maximum branch angle (degrees)
const PAD = 20;                    // SVG padding
```

Font, spacing, and branch mode are configurable from the Settings drawer without editing the source.

## License

Code: [MIT](https://opensource.org/license/mit) · LaTeX package: [LPPL 1.3c](https://www.latex-project.org/lppl/lppl-1-3c/) · Diagrams/documentation: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

© 2026 Pablo Zdrojewski — [support@pablozd.ar](mailto:support@pablozd.ar)

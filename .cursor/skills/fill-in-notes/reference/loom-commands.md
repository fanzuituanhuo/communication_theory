# Loom command reference (this project)

`\documentclass[cjk]{loom}` — options: `cjk` (中文), `letter` (US-letter; default A4).
XeLaTeX only. Local class: `source_coding/src/loom.cls` (answer mode extended).

## Dual PDF entries
- `main.tex` — student (blanks)
- `main-answers.tex` — `\showanswerstrue` then `\input{main-body}`
- Shared body: `main-body.tex`

Project macros (defined in both entries):
- `\pmf` → `p`
- `\Xcal` → `\mathcal{X}`
- `\info` → `I`
- `\seq{X}` → `X_1,X_2,\cdots,X_L`

## Cover & structure
- `\loomcover{title}{subtitle}{author}{date}` — title page + selvage rail
- `\weave` — start the rail if you skip the cover
- `\runningthread{text}` — quiet footer label
- `\section` / `\subsection` / `\subsubsection` — Optima headings; section number on the rail

## Knots (theorem-likes)
- `theorem`, `lemma`, `proposition`, `corollary` → indigo
- `definition` → madder
- `example` → weld
- `remark`, `remark*` → unboxed
- `proof` → woven end tile; keep readable by default in this project
- Optional `[note]` after the head, e.g. `\begin{theorem}[… Thm. 2.16]`
- `\weaveid{L03}` — inline knot-ID stamp

## Intuition voice
- `strand` — informal “what’s going on” (read-only)
- `\whisper{…}` — short aside
- `\keyword{…}` — madder bold for a new term

## Pedagogy — prefer answer-aware commands

| Prefer | Avoid in new content | Role |
|---|---|---|
| `\answerin[width]{answer}` | `\fillin[width]` | ruled blank / red answer |
| `\answertodo{hint}{answer}` | `\TODO{hint}` | proof/derivation gap with answer mode |

Also available:
- `\block{…}` — quiet sub-heading
- `\trigger{…}` — “when you’d reach for this”
- `yourturn` — active-input box
- `\workspace[n]` — `n` faint ruled lines
- `\recall{question}` — margin active-recall prompt
- `\warmth{0..5}` — grok gauge

Upstream `\fillin` / `\TODO` still exist in the class (and `\answerin`/`\answertodo`
delegate to them when answers are off), but new notes should always pass the answer
text through `\answerin` / `\answertodo`.

## Selvage edge
- `\loose{…}` — dangling-thread margin exercise
- `\warp{key}` / `\pick{key}` — declare / reuse a recurring object

## Tables
- `\newcolumntype{L}` — wrapping `X` column for `tabularx`
- Pattern: `\begin{tabularx}{\linewidth}{@{}l l L@{}} … \end{tabularx}`
- Header over `L`: `\multicolumn{1}{l}{\color{indigo}…}`

## Palette
`inkiron`, `indigo`, `madder`, `weld`, `linen`, `thread`, `selvage` — retune in `loom.cls`.

# Pitfalls — XeLaTeX / unicode-math / this repo

## Engine & dual build
- **Must use XeLaTeX** (`latexmk -xelatex`), never pdflatex — class loads `fontspec`.
- Always build **both** student and answer entries, then move PDFs:

```bash
cd source_coding/src
latexmk -xelatex main
latexmk -xelatex main-answers
mv main.pdf main-answers.pdf ../pdf/
```

- Intermediate `.aux`/`.log`/`.xdv` stay in `src/`; final PDFs only in `pdf/`.
- Run twice (or latexmk): selvage rail uses `remember picture`; TOC/`\ref` need pass 2.
- Document class: `\documentclass[cjk]{loom}` — missing `[cjk]` breaks Chinese.
- Non-macOS: swap `\newfontfamily` lines in `source_coding/src/loom.cls` if needed.

## Answer-mode commands
- New blanks: `\answerin` / `\answertodo` only. Bare `\fillin` / `\TODO` have no
  answer-mode fill and break the dual-PDF workflow.
- Math-mode answers: `\answerin` handles math vs text; prefer `\answerin[…]{\text{…}}`
  when the blank sits in a display and the answer is Chinese/words.
- Several blanks on one display line overflow — stack in `aligned` instead of one row.

## unicode-math
- `\mathbb` in a subscript needs braces: `\PP^1_{\R}`, not `\PP^1_\R`.
- `\widehat` over a `\mathbb` macro needs braces: `\widehat{\E}`.
- Do **not** load `amssymb` — conflicts with unicode-math (`\eth already defined`).

## Layout
- Wide table columns: use `L` (wrapping `X`); header over `L` as
  `\multicolumn{1}{l}{\color{indigo}…}`.
- Long `\warp{key}` tags clip — keep keys short.
- Margin notes don’t auto-avoid: don’t put `\loose` right after a `yourturn` that
  ends with `\recall` — they overprint. Close with an inline `strand` or separate them.
- Optima lacks some glyphs (e.g. `→`): in `\block`/headings use `$\to$`.

## Project hygiene
- Edit only under `source_coding/src/`. Do not modify `loom-notes-main/` unless
  syncing upstream Loom.
- New images → `source_coding/src/assets/`.
- New sections: add `\input{…}` only in `main-body.tex`, not in both entry files.
- When bulk-replacing Chinese, use UTF-8-aware tools (plain `perl -CSD` can mojibake).

## Verify before declaring done
```bash
gs -dQUIET -dBATCH -dNOPAUSE -sDEVICE=png16m -r130 -dFirstPage=2 -dLastPage=2 -o p2.png ../pdf/main.pdf
grep -cE 'Overfull \\hbox \([0-9]{2,}\.' main.log
grep -c undefined main.log
grep -c 'Font shape .*undefined' main.log
```
Aim for 0 on the greps; actually look at the rasterized page.

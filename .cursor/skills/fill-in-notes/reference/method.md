# The method — passive read + active recall

Notes should **read** like exposition and **do** like a worksheet. Wrong ratio →
either a transcript (no thinking) or a blank worksheet (no scaffold).

## The 70/30 rule

Roughly **70% readable, 30% to fill.** Gaps go at high-value thinking points.

**Leave readable (passive):**
- Motivation and intuition (`strand`)
- Theorem / proposition / lemma / corollary statements — in full
- Proofs by default — keep the derivation continuous and readable
- Cheat-sheet / dictionary scaffolding (structure stays; blank only key cells)

**Blank out (active) — use project commands:**
- A *defining clause* of a definition → `\answerin[…]{…}`
- The *computation* or punchline in an example → `\answerin` or restage as `yourturn`
- A dictionary row the section is about → blank cell with `\answerin`
- A short “key idea recall” after a proof → `yourturn` or `\recall`
- Only a specially trainable one-step proof move → `\answertodo{hint}{answer}`

## Proof policy (this project — overrides upstream)

Upstream Loom examples often skeletonize proofs with `\TODO`. **Do not** do that
mechanically here.

- Default: write the full proof; do not dig blanks into every step.
- After the proof, add a short `yourturn` that asks for the key move, key equality,
  or one-sentence intuition.
- Rare exception: a short one-step proof where blanking the core action is useful —
  then one `\answertodo`, not a full skeleton.

## Find the spine first

Before writing sections, name the ONE organizing idea and put it on the front page
in `main-body.tex`. Examples: a dictionary, an engine list, a single theorem the
rest orbits, a mirrored pair. Keep the source order only if it *is* the best shape.

## Per-section rhythm

`\section` → `\warmth{0}\quad\whisper{…}` → `strand` → `\trigger`/`\block` →
cheat-table → knots (definition · theorem · example) with `\answerin` gaps →
optional `yourturn` → `\recall` / `\loose`.

## Tone

Warm, concrete, lean. Prefer the source’s best concrete example. Cite source
numbering in knot titles when the learner needs an answer key. Go light on
em-dashes. State honestly; don’t inflate.

# Design Brief — Reverie Traveler Sheet

**For:** a design-focused agent building the character sheet for *Reverie — The Notebook Game*.
**Deliverable:** a single self-contained HTML file (no build step, no external JS libraries; Google Fonts allowed). A reference scaffold exists (`reverie-traveler-sheet.html`) — treat it as a wireframe with working interactions, not a finished design. You may redesign freely within the constraints below.

---

## 1. What this object is

Reverie is an analog, collaborative travel RPG played with a notebook, a pencil, and two d6. The character sheet is **one traveler's notebook page**. It is not a dashboard and not a form — it is a paper object that happens to be on a screen. It must work three ways:

1. **On a phone during play** — glanceable, tappable, one-handed.
2. **Printed** — drops cleanly onto A4/A5, black-on-white, all interactive chrome hidden.
3. **As a template to copy by hand** — someone should be able to reproduce its structure into a real notebook in two minutes. Structure must therefore be drawable: dots, boxes, slots, ruled lines. No element may depend on color alone to be understood.

## 2. Identity: the daylight inverse

The game's manual lives in lantern-dark (ink night `#131a22`, amber `#e0a458`, seaglass `#7fa99b`, bone `#e8e2d4`). The sheet is the **same identity turned inside out**: it lives in daylight, as the paper the manual glows against.

Tokens (adjust values only if you keep the relationships):

| Token | Value | Role |
|---|---|---|
| paper | `#ece6d8` | page ground (bone, warmed slightly) |
| ink | `#1c2733` | primary text and strokes |
| graphite | `#5a646e` | hints, secondary strokes — pencil, not print |
| lantern | `#a1712f` | the single warm accent: Burden, weathering marks, oracle numbers (darkened amber for light-ground contrast) |
| seaglass | `#4f7a6c` | echo/motif accent only — used sparingly |

Do **not** drift toward a generic cream-and-terracotta template. Every accent must map to a game concept (lantern = cost/attention, seaglass = memory), never to decoration.

## 3. Typography

Three roles, already established in the game's identity:

- **Display** — Cormorant Garamond (600, and italic): road-name, facet names, prompts.
- **Written/body** — Crimson Pro: player-entered text renders in *italic light* — it should read as penned into the page. Avoid handwriting fonts; they tip into costume.
- **Utility** — IBM Plex Mono, small caps-style tracking: section labels, slot numbers, the oracle strip. Mono = the rules' voice; serif = the traveler's voice. Keep that separation strict.

## 4. Content model (fixed — do not add or remove fields)

- **Road-name** — one line, the largest text on the page.
- **Five answers**: reason for wandering; keepsake (cross-references satchel slot 1); burden (cross-references satchel slot 7); dream-place (cross-references the echo-mark margin). Each is one written line with an italic prompt above it.
- **Three facets** — Bone / Breath / Dream. Each has: name, three-word gloss, **3 dot sockets** (shared budget of 6 dots across all facets, max 3, min 1 per facet), and **3 weathering boxes** beneath.
- **Satchel** — exactly 7 slots. Slot 7 is visually distinct and permanently labeled *burden* (dashed border, lantern tint in the scaffold).
- **Waymarks** — ruled lines, one per session, growable.
- **Echo-mark margin** — a true notebook margin: a narrow rail with ~5 empty circles where the player draws/types invented symbols for recurring motifs. This is the sheet's most Reverie-specific element; give it care.
- **Oracle strip** — footer micro-reference: `1 no,and · 2 no · 3 no,but · 4 yes,but · 5 yes · 6 yes,and`. Nothing more; the sheet is not the rulebook.

## 5. Layout concept

```
┌──┬──────────────────────────────────┐
│e │ REVERIE · TRAVELER               │
│c │ Road-name ______________________ │
│h │                                  │
│o │ FIVE ANSWERS (2-col, prompts+    │
│  │ ruled lines; wide rows for       │
│m │ reason & dream-place)            │
│a │                                  │
│r │ FACETS  [Bone] [Breath] [Dream]  │
│k │  ●●○ dots / ☐☐☐ weathering each  │
│s │                                  │
│  │ SATCHEL [1][2][3][4][5][6][B]    │
│  │ WAYMARKS ◆ ______________        │
│  │ ORACLE STRIP 1..6                │
└──┴──────────────────────────────────┘
```

Single page, max-width ≈ 50rem, margin rail on the left (collapses to a top strip under ~560px). Vertical rhythm should feel like a well-ruled page, not a card grid.

## 6. Interaction spec

All state is in-memory only. **Never use localStorage/sessionStorage** (unsupported in the target environment).

- **Dots:** clicking dot *n* sets that facet to *n*; clicking the current top dot lowers by one. A live "dots left: N" counter enforces the shared budget of 6 (clamp, don't error). Filled dots render as graphite fill, not flat color.
- **Weathering:** boxes toggle to a hand-struck **X** in lantern. When all three are marked, the facet visibly *closes* (label suffix "· closed", tinted border). This is the sheet's one state-change moment — make it legible but quiet.
- **Text fields:** `contenteditable` with italic graphite placeholder hints (via `data-hint`/`:empty::before`). Hints are in the game's voice: "phrase it like a mystery…", "it rides in slot 7".
- **Waymarks:** an "+ add a waymark" action appends a line and focuses it. Hidden in print.
- **Echo-marks:** each circle is a one-or-two-character editable glyph. Seaglass ink.

## 7. States & accessibility

- Empty state = an inviting blank page; hints do the onboarding, no instructions block.
- All toggles are real `<button>`s with `aria-pressed`; all editable regions have `aria-label`s; visible `:focus-visible` outline (lantern).
- Color contrast ≥ 4.5:1 for text on paper; state never conveyed by color alone (dots fill, boxes strike, closed facets gain a text suffix).
- Respect `prefers-reduced-motion`; motion budget is near-zero anyway — at most a soft transition on fills. No ambient animation: the manual glows, the sheet is still.

## 8. Print

`@media print`: white background, no shadow, hide the add button, force-print the fills/strikes (`print-color-adjust: exact`), fit one sheet to one A4 portrait page. Bonus: a second `.half` layout that fits two A5 sheets per A4 for cutting.

## 9. Copy rules

- Sentence case, plain verbs. Prompts are questions in the traveler's register ("What do you fear becoming?"), labels are the rules' register in mono ("weathering", "satchel — seven slots").
- No instructional paragraphs on the sheet; if a rule needs explaining on the page, the design has failed.

## 10. Signature element (where to spend boldness)

One place: the **echo-mark margin**. It is what makes this a Reverie sheet rather than any indie-RPG sheet. Ideas worth exploring: circles that subtly age (deepen) once filled; a faint dotted thread linking the dream-place answer to the margin; the margin printing with extra empty circles. Keep everything else disciplined — the page should feel like it is waiting for a pencil.

## 11. Out of scope

Dice rollers, rules text beyond the oracle strip, persistence/accounts, party/shared views, dark mode (the manual is the dark mode).

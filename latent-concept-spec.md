# LATENT
## Concept Specification — the Reverie Capture Companion

*A phone app that is only interesting when you stop walking.*

**Status:** concept locked, ready for prototyping.
**Lineage:** implements the "Field notes" rule from *The Shared Lantern* — capture while moving, develop when seated. Quietly, it is v0.05 of the parked Road platform: the future corpus for the Lens and the Archivist.

---

## 1. The name

**Latent**, from photography's own vocabulary: a *latent image* is what exists on exposed film before developing — present, complete, invisible. The word already lives in the rules (a Vessel's Charge "is latent"). The app holds latent images; Develop makes them actual.

## 2. The vow

Latent is a capture tool with a ten-second ceiling and a vow of emptiness. Everything it holds is meant to leave it and become ink in the real notebook. It is structurally incapable of being interesting while walking. The notebook is the truth; Latent is the pocket between the world and the page.

## 3. The one law: total darkness

**The live screen shows three buttons and nothing else.** No capture count. No thumbnails. No timeline. No settings icon. No ember of feedback of any kind while a passage is live. A capture confirms with a single haptic pulse — felt, not seen — and the screen returns to the three buttons.

This is the design's spine. Every future feature request is tested against it and almost all will fail. The phone must have nothing to offer a wandering eye; the world must always be the more interesting screen.

## 4. Live mode — night

Lantern-dark UI (the game's night palette: ink `#131a22`, amber `#e0a458`). Three large glare-readable one-thumb targets:

- **GLYPH** — opens the traveler's own echo-mark symbols, drawn once by finger, shown as a grid. Tap one = a timestamped recurrence of that motif. Long-press empty cell = draw a new glyph. Motif tracking with zero typing. Closes itself.
- **PHOTO** — full-screen viewfinder, one shutter, no review, no retake, no filters. The door where the lantern passed, the found thing, the sign. Closes itself.
- **VOICE** — hold to speak, release to keep. Spoken as a notebook line ("residue: the lit window above the closed shop"). No playback available live. Closes itself.

Bracketing ghost controls, visible only at rest on the three-button screen:

- **Begin passage** — timestamps, and silently records weather + rough location if the journey has opted in. Nothing else changes on screen.
- **End passage** — asks for one spoken residue line. Skippable; a skipped residue marks the passage *unclosed*.

## 5. Develop mode — day

Available only when a passage has ended. The UI inverts to the daylight paper palette (paper `#ece6d8`, ink, graphite) — the same night/day inversion the whole Reverie design system uses, now meaning something: **capture is night, ink is day.**

- The passage unrolls as a **strip in capture order**, one item at a time, advanced by swipe. No grid overview until developed.
- The header writes itself from the silent annotations: *Passage 4 · harbor · light rain · 41 min.*
- **Playback, not transcription.** Photos display; voice memos play aloud; glyph taps show symbol + time. There is no speech-to-text and never will be — the hand inks every line into the real notebook. The app shows and speaks; the pencil does the rest.
- Finishing marks the strip **developed**: it fades to a sepia contact sheet in a quiet archive, ordered by journey. Browsable, never editable, exportable as a plain file bundle.
- **Unclosed passages** sit at the top of Develop, slightly accusatory, until inked.

## 6. Modes — one law, three idioms

The total-darkness law is constant; what varies is who develops, and when.

### Solo — the time-split self
Solo Reverie's structural weakness is one mind playing both traveler and keeper. Latent solves it with time. On the walk you play aloud — murmured narration, questions to world-oracles, glyph taps as motifs surface — captured, unreviewable. At Develop, your own voice plays back, and twenty-minutes-ago-you is a different person: a traveler who didn't know what the next street held. **Past-you walks; present-you keeps and inks.** The darkness plus the delay manufactures the second player solo play never had.

Two solo idioms:
- **The motif hunt.** Begin a passage with no destination and let glyph taps be the navigation — turn toward whatever rusts. Walking meditation with attention anchored to symbols; the contemplative core of the game with zero apparatus.
- **The walking Threshold Moment.** Already looking at the world, the tie's rule inverts: *press the shutter on the first thing you notice.* The photo enters the fiction at Develop — you won't know what you caught until you sit down.

### Duo — the braid
Each traveler carries their own Latent and captures independently. At the café, either phone's Develop **interleaves both strips by timestamp** (local share — QR or proximity, no server). The walk is inked as one braided sequence, and each traveler discovers what the other dog-eared that they never saw. The Duet's energy — *which detail was invented?* — recurs as: *when did you press the shutter, and at what?*

### Table — the keeper's week and the empty chair
During a seated session, Latent stays in pockets, correctly. Its table uses live between sessions:
- **The keeper's week.** The incoming keeper carries Latent in the days before their passage; their three-things prep develops from real captures, so the opening image is a photograph they took — transformed from the inherited residue, per the chain rule.
- **The errand feed.** An absent player's undeveloped strip is a postcard's raw material, ready-made: one image, one voice line, one glyph.

## 7. Optional cruelty: volatile film

A per-journey setting, **off by default**: undeveloped captures blur — literally, a little more each day — and are gone in seven. Ink at the next roof or lose the walk. For travelers who trust themselves too much.

## 8. What Latent refuses, permanently

No dice (dice are physical). No rules text (the cards exist). No feed, no accounts, no cloud, no social, no sharing. No gallery access mid-walk, no editing, no filters. No AI — *yet*: door photos, voice residues, and glyph timestamps are precisely the corpus the future Lens and Archivist metabolize, and Latent's export format should quietly anticipate that without ever mentioning it.

## 9. Technical shape

- Offline-first installable PWA; no server, no account, functional forever in airplane mode.
- Camera via getUserMedia; voice via MediaRecorder; storage on-device (IndexedDB), size-capped with oldest-developed-first eviction.
- Opt-in per journey: coarse geolocation + cached weather for self-annotating headers.
- Export: a per-journey bundle (photos, audio, a plain-text manifest of timestamps/glyphs) — human-readable, future-Lens-ready.
- Accessibility: haptic capture confirmation; all three live buttons operable by touch position alone; Develop fully screen-reader navigable.

## 10. Acceptance tests

- [ ] A live passage offers **zero** visual information beyond three buttons
- [ ] Any capture completes in under ten seconds, one-handed, walking
- [ ] Nothing captured can be reviewed until the passage ends
- [ ] Develop plays voice aloud and never prints its words
- [ ] Two phones can braid one walk with no network
- [ ] The app is fully usable with the phone never leaving airplane mode
- [ ] Deleting the app after developing loses nothing that matters — it's all in the notebook

---

*The world is the screen. The notebook is the save file. Latent is only the dark between them.*

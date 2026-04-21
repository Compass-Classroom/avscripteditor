---
reviewer: Ryan Stufflebeam
date: 2026-04-21 10:16
session: BriefOnly dry run — Astronomy Ch 1, Faulkner
scope: Image briefs only (text on-screen callouts deliberately excluded — see architectural notes)
---

# Ryan's Feedback — 2026-04-21 10:16

Review of the `BriefOnly` dry run on the Astronomy / Faulkner Ch 1 Google Sheet. **Images only.** All `type: text` rows intentionally skipped in this pass — see architectural items below for why.

Severity tags: `[blocker]` must fix, `[refine]` adjust the brief, `[idea]` worth considering, `[nit]` minor.

---

## Architecture / Structural

- [ ] **[blocker] Split on-screen text out of this skill entirely.** On-screen text callouts should be produced by a *different* agent — one that has the textbook in front of it. AVScriptEditor should only be doing image review. All `type: text` entries in this dry run were skipped for that reason.
  - *Why:* text selection needs textbook context that the image-review agent doesn't have, and mixing the two muddies both passes.

- [ ] **[blocker] Briefs need their own dedicated column — get them out of NOTES.**
  - *Why:* NOTES is reserved for XML generation downstream. Anything left in NOTES becomes a marker on the Final Cut timeline for the human editor to act on. Briefs sitting in NOTES will pollute the timeline with marker noise.
  - *Suggested fix:* add a new column (e.g. `BRIEF` or `IMAGE BRIEF`) and update the column map in `SKILL.md` + all four workflows. NOTES stays empty unless the editor deliberately flags something for the FCP human.

---

## Row-by-row (column F — image briefs)

Rows not listed were either `type: text` (skipped this pass) or not reviewed.

### Approved as-is

- [ ] **F10** — good.
- [ ] **F12** — good.
- [ ] **F14** — good.
- [ ] **F20** — good (same strong pick from the previous iteration).
- [ ] **F27** — good.
- [ ] **F31** — good; "gives time" works here.
- [ ] **F40** — good.
- [ ] **F48** — good.
- [ ] **F62** — good.
- [ ] **F70** — good.
- [ ] **F77** — great.
- [ ] **F82** — good; **this** is the right spot for the zodiac (see F67 below).
- [ ] **F117** — good.

### Refinements

- [ ] **[refine] F13** — pivot from the current pick to a **historical** image (altarpiece painting or illuminated manuscript depicting the creation account).
  - *Why:* the previous iteration worked because there were no historical images leading into this beat. Now that historical images precede it, staying in that visual lane preserves continuity.

- [ ] **[refine] F44** — correct star, but the brief needs to specify **the star seen just over the Egyptian horizon**.
  - *Why:* the whole point of the beat is the context — star + Egyptian horizon together on screen so the viewer connects them.
  - *Sourcing hint:* could be a science photo, an art-astronomy photo, or a painting. Any medium works as long as the horizon context is unmistakable.

- [ ] **[refine] F67** — medieval calendar direction is right, but reconsider leading with the zodiac here.
  - *Why:* the calendar has to read as *a calendar* to a high-school student with no archaeology or antiquities background. Zodiac imagery may distract from that.
  - *Move the zodiac to F82* (already the right place for it).

- [ ] **[refine] F103** — great pick **if such an image exists**. Flag back if sourcing can't find it.

- [ ] **[refine] F112** — probably good; decision deferred until we see what sourcing pulls.

- [ ] **[refine] F123** — good **if we can find a public-domain Farmer's Almanac image**. Needs license check at source time.

---

## General observations

- [ ] **[idea] Image density feels slightly high.** There are stretches where we cover Danny's face a little too often.
  - *But:* having more options up front is genuinely useful — it beats hunting for images later. The sweet spot is "cover what needs covering, not every beat."
  - *Suggested next step:* revisit `Density Target` in `ProfileAstronomyFaulkner.md` after a second pass, once we know where the real over-coverage is happening.

- [ ] **[idea] Cross-reference the textbook chapter's images as a disambiguation aid.** Not to copy them — to use as a hint when Danny is non-specific about which star, planet, or object he's referencing.
  - *Why:* when the narration is vague ("this star", "that planet"), the textbook often shows exactly what he means. A side-channel lookup against the chapter's figure list would let the image agent resolve ambiguous references.
  - *Implementation note:* this probably belongs as an optional input to `BriefOnly` / `PopulateSheet` — a textbook-chapter reference alongside the sheet URL.

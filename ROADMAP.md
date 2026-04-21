# AVScriptEditor — Roadmap

Ideas parked for later. Nothing here is committed work; each item carries the signal that prompted it so we can decide when to pick it up.

## Parked — revisit after more real-world passes

### Density Target review

**Status:** Do NOT change `Density Target` in `ProfileAstronomyFaulkner.md` yet.

Ryan flagged on the BriefOnly dry run (`Feedback/Ryans-Feedback-2026-04-21-1016.md`) that image density felt *slightly* high in stretches. He also noted — on follow-up — that the abundance of image options is useful in practice: having more candidates up front beats hunting for images later. The sweet spot will reveal itself after a second pass in production.

**Revisit when:**
- A second BriefOnly/PopulateSheet pass has been produced AND reviewed
- Ryan has a concrete read on where actual over-coverage shows up (specific beat types, section transitions, etc.)

**Owner:** Ryan (editorial judgment) + Verbum (profile edit via `UpdateProfile` workflow once Ryan gives a direction).

---

## Design — scoped, not yet implemented

### Textbook chapter cross-reference

**Goal:** Let BriefOnly / PopulateSheet consult the course's textbook chapter when the narration is vague about which star, planet, or object is being referenced ("this star", "that planet", "the moon phases here"). The textbook usually shows exactly what the instructor means — figures, captions, and page layout disambiguate.

**Why now (as a parked design, not an implementation):** Ryan raised it as an idea in the first review. The architectural shape is worth having ready so we can wire it in quickly when the first textbook source is handed over.

**Shape — Miessler/PAI-aligned:**

1. **Textbook source lives in the profile, not the invocation.**
   Each course has its own textbook, and the file path/URL is stable per course. Add a `## Textbook Source` section to each profile answering:
   - Title + edition
   - Access method (Google Drive file ID, S3 URL, local path, etc.)
   - File format (PDF, DOCX, EPUB)
   - Chapter-to-AV-script mapping (usually 1:1, but a mapping table goes here if it's not)

2. **Chapter selection is a run-time argument.**
   Invocation pattern:
   > "Draft briefs for astronomy-faulkner on \<sheet-url\>, textbook-chapter 1"

   The workflow parses `textbook-chapter N`, picks up the source from the profile, and loads chapter N's figures before the pacing pass begins.

3. **Dispatch to existing skills rather than rebuild.**
   - Textbook in Google Drive → `GoogleWorkspace` pulls it
   - PDF → `PDF` / `Documents` skill parses figures (page, caption, bounding boxes)
   - Figures (as images) can inform the brief's sourcing hint OR pass directly through to a reviewer for disambiguation

4. **Backward compatible — optional everywhere.**
   BriefOnly without a textbook argument works exactly as today. With the argument, briefs for vague-narration rows get an extra line: `TEXTBOOK:<chapter> <figure> | <caption>`. The sourcer (FindScienceMedia / FindArt) can then search for *either* an image matching the caption OR an image of the same subject with correct context.

**Acceptance criteria for the implementation phase:**
- Profile has a `## Textbook Source` section with access details
- `BriefOnly` accepts an optional `textbook-chapter: N` arg
- When provided, figures from that chapter are parsed before briefing starts
- Ambiguous-subject beats get a `TEXTBOOK:` line when a relevant figure exists
- Skill still runs without a textbook argument (no regression)

**Not in scope for the first implementation:**
- Automatic chapter detection from sheet name (nice-to-have; skip)
- Figure-to-brief confidence scoring (premature optimization)
- Caching parsed chapters across runs (optimize later if slow)

**Prerequisites to start:**
- Astronomy textbook (Faulkner edition) accessible — Google Drive file ID or PDF path
- Confirmed chapter-to-AV-script mapping (1:1 assumed until proven otherwise)

**Why it's parked now:** no blocker yet; Ryan is evaluating current briefs. Ready to start when the first textbook source is wired in.

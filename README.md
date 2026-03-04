# Planning Statement Skill

A Claude skill for developing professional UK planning statements through an iterative, conversational process.

## What it does

Guides you through every section of a planning statement one stage at a time, researching relevant Local Plan and NPPF policies as you go, and compiling the result into a formatted .docx document.

## How it works

### Iterative loop at every stage

Each stage follows the same cycle:

1. **You provide the facts** for that topic
2. **Claude researches** the relevant Local Plan and NPPF policies for that specific topic
3. **Claude feeds back** what the policies require and how your facts align
4. **You correct or add detail**
5. **Claude re-checks** the corrections against the original policy AND any associated policies the change triggers
6. **Loop back** if new issues surface, otherwise confirm and move on

### Accumulating outline file

Every confirmed stage appends bullet points to `/home/claude/outline.md` — facts, policies identified, compliance narrative, and outstanding issues. This file persists across `/compact` and serves as the source material for document generation.

### Dynamic compact trigger

When the outline exceeds 50 bullet points, Claude triggers `/compact` at the next stage boundary. The outline file holds all state, so nothing is lost.

## Stage order

| Stage | Topic | Policy research |
|-------|-------|-----------------|
| 0 | Project Setup | Adopted Local Plan identified |
| 1 | Introduction | -- |
| 2 | Site Description & Context | Designation-specific policies |
| 3 | Planning History | Parish Council comment research |
| 4 | The Proposal | Proposal-triggered policies (volume, CIL, use class) |
| 5 | Design & Visual Impact | Design policies, SPD/guidance |
| 6 | Residential Amenity | Amenity policies, separation distances, daylight |
| 7 | Access, Highways & Parking | Parking standards, transport policies |
| 8 | Environmental Considerations | Flood, ecology, trees, sustainability policies |
| 9 | Heritage (if applicable) | Heritage policies, conservation area appraisals |
| 10 | Policy Framework Review | Bird's-eye gap-check of entire outline against all policies |
| 11 | Consultation & Engagement | Cross-check policies cited in pre-app advice |
| -- | Final Check | Unique aspects, fallback positions |
| -- | Document Generation | Compile outline into .docx |

### Key design decisions

**Policy research is embedded, not front-loaded.** The old Stage 5 "Policy Framework" has been moved to Stage 10 as a holistic review. Each topic stage does its own policy research as you go, so by Stage 10 most policies are already identified and the review is a gap-check and strategic policy sweep (NPPF Ch.2/4, spatial strategy, neighbourhood plans).

**Parish Council intelligence.** The parish/town council is identified at Stage 0. At Stage 3, Claude researches their comments on comparable applications — returning reference numbers, descriptions, and positions. This is awareness intelligence, not a checklist to rebut. The statement addresses policy tests on their merits, not community politics.

**Backward references.** If later stages reveal something that affects earlier sections (e.g. a conservation area appraisal identifying roofscape significance), Claude adds a note under the relevant earlier stage heading in the outline file.

**Document structure is flexible.** Section 10 (Policy Framework) can sit as Section 10 in the final document (after topic sections, before conclusion) or as Section 5 (traditional position). Claude asks which you prefer before generating.

## Output

Professional .docx planning statement with numbered sections, page numbers, table of contents (for longer statements), and inline policy citations throughout.

## Triggers

- "planning statement", "write a planning statement", "help with planning statement"
- "policy justification", "planning application support"
- "I need to justify this scheme to the planners"
- "help me with the policy argument"
- Any Design and Access Statement discussion involving policy justification

## Rules

- One stage at a time — never skip or combine
- Never request applicant details or site address
- Policy citations must be specific — always cite policy numbers
- Active professional voice, positive framing
- No bullet points in the final document body — flowing paragraphs

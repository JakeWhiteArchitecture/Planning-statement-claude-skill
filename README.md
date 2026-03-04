---
name: planning-statement
description: Develop planning statements for UK planning applications through an iterative, stage-by-stage conversational process. Guides the user through each section of the statement — gathering site-specific information, researching relevant Local Plan policies online, and confirming completeness before moving on. Produces a professional .docx planning statement as the final deliverable. Triggers on planning statement, write a planning statement, help with planning statement, policy justification, planning application support, or when the user is preparing a planning submission and needs policy compliance narrative. Also use when a Design and Access Statement is discussed in the context of planning policy justification. Always use this skill when the user mentions writing or developing a planning statement, even if they don't use those exact words — for example "I need to justify this scheme to the planners" or "help me with the policy argument".
---

# Planning Statement Skill

---

## WORKFLOW OVERVIEW

```
START
  |
  v
+-----------------------------+      +---------------------------+
|  STAGE 0: PROJECT SETUP     |      |  OUTLINE FILE             |
|  District, app type         |      |  /home/claude/outline.md  |
|  -> Local Plan research     |----->|  Accumulates confirmed    |
+-----------------------------+      |  bullet points at each    |
  |                                  |  stage. Persists state    |
  v                                  |  across /compact.         |
+-----------------------------+      |                           |
|  STAGE 1: INTRODUCTION      |----->|  Each stage appends:      |
|  Agent, address, purpose    |      |  - Facts                  |
+-----------------------------+      |  - Policies identified    |
  |                                  |  - Compliance narrative   |
  v                                  |  - Outstanding issues     |
+-----------------------------+      |                           |
|  STAGE 2: SITE & CONTEXT    |----->|                           |
|  Physical, designations     |      |                           |
+-----------------------------+      |                           |
  |                                  |                           |
  v                                  |                           |
+-----------------------------+      |                           |
|  STAGE 3: PLANNING HISTORY  |----->|                           |
+-----------------------------+      |                           |
  |                                  |                           |
  v                                  |                           |
+-----------------------------+      |                           |
|  STAGE 4: THE PROPOSAL      |----->|                           |
+-----------------------------+      |                           |
  |                                  |                           |
  v                                  |                           |
+-----------------------------+      |                           |
|  STAGE 5: DESIGN & VISUAL   |----->|                           |
+-----------------------------+      |                           |
  |                                  |                           |
  v                                  |                           |
+-----------------------------+      |                           |
|  STAGE 6: AMENITY           |----->|                           |
+-----------------------------+      +---------------------------+
  |
  v
+--------------------------------------+
|  >>> /compact TRIGGER <<<            |
|  Fires when outline.md exceeds 50   |
|  bullet points. Always at a stage   |
|  boundary. Re-read outline.md       |
|  after compact to resume.           |
+--------------------------------------+
  |
  v
+-----------------------------+      +---------------------------+
|  STAGE 7: ACCESS & HIGHWAYS |----->|  OUTLINE FILE continues   |
+-----------------------------+      |                           |
  |                                  |                           |
  v                                  |                           |
+-----------------------------+      |                           |
|  STAGE 8: ENVIRONMENT       |----->|                           |
+-----------------------------+      |                           |
  |                                  |                           |
  v                                  |                           |
+-----------------------------+      |                           |
|  STAGE 9: HERITAGE          |----->|                           |
|  (skip if not applicable)   |      |                           |
+-----------------------------+      +---------------------------+
  |
  v
+--------------------------------------+
|  STAGE 10: POLICY FRAMEWORK REVIEW   |
|  Bird's-eye review of outline.md     |
|  against ALL policies. Gap-check.    |
|  Strategic policies (NPPF Ch.2/4).   |
|  Cross-references between sections.  |
+--------------------------------------+
  |
  v
+-----------------------------+
|  STAGE 11: CONSULTATION     |
|  Pre-app, DRP, engagement   |
+-----------------------------+
  |
  v
+-----------------------------+
|  FINAL CHECK                |
|  Unique aspects? Fallback?  |
+-----------------------------+
  |
  v
+-----------------------------+
|  DOCUMENT GENERATION        |
|  Read outline.md            |
|  Read docx SKILL.md         |
|  Compile .docx              |
+-----------------------------+
```

---

## CRITICAL RULES

- **One stage at a time.** Never skip ahead or combine stages.
- **Iterative loop at every stage.** Each stage follows the loop defined below -- not a single pass.
- **Outline file is the memory.** Every confirmed stage appends to `/home/claude/outline.md`. This file persists across `/compact` and is the source of truth for document generation.
- **District Council must be established first.** Stage 0 must identify which LPA the application is being submitted to -- this determines all subsequent policy research.
- **Active, professional voice.** Write as though from the applicant's architect/agent. Positive framing -- "the proposal will..." not "the proposal should..."
- **Policy citations must be specific.** Always cite policy numbers and quote or closely paraphrase the relevant policy test. Generic references like "the proposal complies with local plan policy" are not acceptable.
- **Compact trigger at 50 bullet points.** After each stage is confirmed and appended to the outline, count the total bullet points in `/home/claude/outline.md`. If the count exceeds 50, trigger `/compact` at the next stage boundary. The outline file holds all state -- nothing is lost.

---

## THE ITERATIVE LOOP

**Every stage from Stage 2 onwards follows this loop:**

```
+---> USER PROVIDES FACTS
|         |
|         v
|    CLAUDE RESEARCHES relevant policies for THIS topic
|    (web_search for [district] policies on [topic])
|         |
|         v
|    CLAUDE FEEDS BACK:
|    - Which policies apply and what they require
|    - How the user's facts align with those policy tests
|    - Any gaps or concerns
|         |
|         v
|    USER CORRECTS OR ADDS DETAIL
|         |
|         v
|    CLAUDE RE-CHECKS corrected/additional detail against:
|    - The original policy identified
|    - ANY ASSOCIATED POLICIES the correction triggers
|    (e.g. increased depth triggers amenity policy;
|     mature tree triggers ecology + TPO policy;
|     roof height change triggers landscape policy)
|         |
|         v
|    Loop back if new issues found
|    Otherwise:
|         |
|         v
|    CLAUDE CONFIRMS the policy compliance narrative
|    for this section and APPENDS to outline.md
|         |
|         v
|    "Have we fully explored this topic, or is there
|     anything else to add before we move on?"
```

**Key principle:** Corrections cascade. A changed dimension is not just a number update -- it may cross a policy threshold, trigger an adjacent policy, or affect a test in a different topic area. Always check associated policies when facts change.

---

## THE OUTLINE FILE

At the start of Stage 0, create `/home/claude/outline.md` with this structure:

```markdown
# Planning Statement Outline
## Project: [brief description]
## LPA: [district]
## Application Type: [type]
## Local Plan: [document name and plan period]
---

### Stage 0: Project Setup
**Facts:**
- [bullet points]
**Designations:**
- [bullet points]
**Local Plan identified:**
- [document name, key policy numbers noted]

### Stage 1: Introduction
**Facts:**
- [bullet points]

### Stage 2: Site Description & Context
**Facts:**
- [bullet points]
**Policies identified:**
- [policy number]: [name] -- [how it applies]
**Compliance narrative:**
- [bullet point summary of the argument for this section]
**Outstanding issues:**
- [anything flagged for later stages]

[...repeat structure for each subsequent stage...]
```

**Rules for the outline file:**
- Append after each stage is confirmed -- never overwrite previous stages
- Bullet points must be substantive, not shorthand. Include dimensions, distances, policy numbers, the agreed compliance argument. This file must survive a `/compact` and still make sense.
- If a later stage triggers a backward reference (e.g. heritage research reveals something that affects site context), add a note under the relevant earlier stage heading: `**[Added at Stage 9]:** Conservation area appraisal identifies roofscape significance -- add to materials discussion.`
- The outline file is for Claude's use, not a deliverable. It does not need to be pretty. It needs to be comprehensive.


---

## STAGE 0: PROJECT SETUP

**Purpose:** Establish the basic parameters that determine the entire document structure and policy framework.

**Action:** Create `/home/claude/outline.md` with the header structure.

**Ask these questions:**

1. **Which District/Borough Council** is this application being submitted to?
2. **Which Parish/Town Council** is the site within? (Note: some urban areas are unparished)
3. **Never ask for applicant or site address.**
4. **What type of planning application** is this? (Householder / Full / Outline / S73 / Listed Building Consent / Prior Approval / LDC)
5. **Brief description of the proposal** -- one or two sentences is fine at this point.

**After receiving answers:**

- Confirm the LPA and note any known policy context -- identify the adopted Local Plan document name and plan period.
- Ask: "Do you know what site designations apply? For example: Green Belt, AONB, Conservation Area, Article 5, Listed buildings, Flood Zone, SSSI, Tree Preservation Orders?" -- note the answers for later stages.
- Ask: "Shall I search online for the current adopted Local Plan policies for [district] so I can reference them accurately throughout?"

**Policy research trigger:** If user says yes, use web_search to find the adopted Local Plan and identify the key policy document(s). Fetch and note the policy numbers and document name for reference throughout.

**Append to outline.md:** Project header, LPA, Parish/Town Council, application type, known designations, Local Plan document details.

**Confirm:** "I've got the basic setup and created the outline file. Ready to move to Stage 1 -- Introduction?"

---

## STAGE 1: INTRODUCTION

**Purpose:** Establish the formal opening of the statement -- who, what, where, why.

**Information to gather:**

- Agent details (if applicable -- this will typically be Jake White Architecture)
- Application type (confirm from Stage 0)
- Brief development description (refine from Stage 0)
- Purpose of the statement -- e.g. "to demonstrate compliance with national and local planning policy"
- **Never request applicant details or site address.**

**What this section will contain in the final document:**

A short introductory paragraph identifying the nature of the application and the purpose of the statement. Typically 2-3 paragraphs.

**Append to outline.md:** Agent, refined description, statement purpose.

**Confirm:** "Have we fully explored the introduction, or is there anything else to add before we move on to Site Description & Context?"

---

## STAGE 2: SITE DESCRIPTION & CONTEXT

**Purpose:** Paint a clear picture of the site for the case officer who may not have visited.

**Follow the iterative loop.**

**Information to gather:**

- Physical description of the site (size, topography, existing buildings, access points)
- Surrounding context (what's to the north, south, east, west -- neighbouring uses, character)
- Street scene / area character
- Vegetation, trees, landscape features
- Any uploaded photos, plans, or aerial views to reference
- **Designations** (confirm and expand from Stage 0):
  - Green Belt
  - AONB / National Landscape
  - AGLV / locally valued landscape
  - Conservation Area
  - Listed Building (grade) or setting of
  - Flood Zone (1/2/3a/3b)
  - SSSI / SPA / SAC / Ramsar
  - Tree Preservation Orders
  - Archaeological Notification Area
  - Article 4 Direction
  - Article 5 Direction
  - Neighbourhood Plan area
  - Any local designations specific to the LPA

**Policy research within the loop:** Search for [district] policies relating to each confirmed designation. Feed back what those policies require and how the site's characteristics interact with them.

**Append to outline.md:** Facts, designations confirmed, designation-specific policies identified, any outstanding issues for later stages.

**Confirm:** "Have we fully explored the site and its context? Anything to add before we move on to Planning History?"

---

## STAGE 3: PLANNING HISTORY

**Purpose:** Establish what has been applied for and decided on this site previously.

**Information to gather:**

- Previous planning applications on the site (reference numbers, descriptions, decisions, dates)
- Any refused applications and reasons for refusal (critical -- the statement must address these)
- Any appeal decisions
- Pre-application advice received (reference, date, officer, key advice given)
- Any enforcement history (if relevant and known)
- Current lawful use

**If user doesn't have this information:**

- Offer to search the LPA's planning register online if the address is known

**Parish Council comment research:**

If a Parish/Town Council was identified in Stage 0, offer to search for their comments on similar applications in the area. Search the LPA planning register or parish council minutes for recent comments on comparable proposals (e.g. similar scale extensions, new dwellings, similar use class changes).

For each relevant comment found, note:
- Application reference and description
- Parish Council's position (support/object/no comment)
- Key concerns raised

**Important:** Parish Council comments are intelligence, not a checklist to respond to. Many parish councils are generally anti-development and their objections often go beyond material planning considerations. The statement should be **aware** of likely concerns so it can pre-emptively address any that overlap with genuine policy tests, but should NOT directly respond to or rebut parish council positions. The focus is the adopted local and neighbourhood plans, regional and national policy.

**Append to outline.md:** Application history, refusal reasons (flagged for policy response), pre-app advice summary, Parish Council comment patterns (for awareness, not direct response).

**Confirm:** "Have we fully explored the planning history? Anything to add before we move on to The Proposal?"

---

## STAGE 4: THE PROPOSAL

**Purpose:** Describe what is actually being proposed in sufficient detail for the case officer.

**Follow the iterative loop.**

**Information to gather:**

- Detailed description of the proposed development
- Dimensions -- footprint, height, depth of extension, ridge/eaves heights
- Materials -- external finishes, roof covering
- Number of storeys
- Use -- existing and proposed (Use Class if relevant)
- Floorspace figures (existing GIA, proposed GIA, net change)
- Number of bedrooms/units (if residential)
- Parking provision (existing and proposed)
- Access arrangements
- Landscaping intentions
- Any demolition
- Phasing (if applicable)

**For extensions/alterations specifically:**

- Relationship to existing building -- where does it connect, how does it read architecturally
- Area, Height and Volume calculations (existing vs proposed, % increase)

**Policy research within the loop:** The proposal description will trigger specific policy checks -- e.g. volume increase triggers Green Belt policy if applicable, floorspace triggers CIL/affordable housing thresholds, parking numbers trigger transport policy. Research and feed back.

**Append to outline.md:** Full proposal description, dimensions, materials, calculations, policies triggered by the proposal specifics.

**Confirm:** "Have we fully described the proposal? Anything to add before we move on to Design & Visual Impact?"

---

## STAGE 5: DESIGN & VISUAL IMPACT

**Purpose:** Demonstrate that the proposal is well-designed and respects local character.

**Follow the iterative loop.**

**Information to gather / discuss:**

- How the proposal responds to the existing building's character (form, materials, proportions, roof pitch)
- How it sits within the street scene / wider landscape
- Scale and massing -- is it subordinate, matching, or dominant?
- Materials palette and rationale
- Key design moves / architectural approach
- If in Green Belt: impact on openness (visual AND spatial)
- If in AONB/AGLV: landscape impact, views from public vantage points
- Reference to NPPF Chapter 12 and relevant local design policy
- Any Design Review Panel feedback (refer to Stage 11 later)

**Policy research within the loop:** Search for [district] design policies and any design SPD/guidance. Feed back what the policy tests require, check the user's design rationale against them.

**Append to outline.md:** Design approach, policy compliance narrative for design, any DRP feedback noted.

**Confirm:** "Have we fully explored the design and visual impact? Anything to add before we move on to Amenity?"

---

## STAGE 6: RESIDENTIAL AMENITY

**Purpose:** Demonstrate the proposal does not unacceptably harm neighbours' living conditions.

**Follow the iterative loop.**

**Information to gather / discuss:**

- **Privacy/overlooking** -- distance to neighbouring windows, orientation, any new windows facing neighbours, mitigation (obscure glazing, high-level, angled)
- **Daylight/sunlight** -- does the proposal project beyond the 45-degree line from neighbours' windows? Any BRE assessment? North-facing elements less impactful
- **Overbearing/sense of enclosure** -- height, proximity, bulk visible from neighbouring gardens/rooms
- **Noise/disturbance** -- any change in activity levels, plant/equipment, hours of use
- **Outlook** -- impact on neighbours' outlook from principal rooms
- **Construction impact** -- hours, access, duration (brief mention)

**Policy research within the loop:** Search for [district] amenity policies and any specific guidance on separation distances or daylight standards. Feed back what the tests require, check the user's dimensions and arrangements against them.

**Append to outline.md:** Amenity facts, policies identified, compliance narrative for amenity.

**Confirm:** "Have we fully explored the amenity impacts? Anything to add before we move on?"

---

## >>> COMPACT TRIGGER <<<

**This is not a fixed stage -- it triggers dynamically.**

After each stage is confirmed and appended to the outline, count the total bullet points in `/home/claude/outline.md`. If the count exceeds 50, trigger compact at the next stage boundary.

**Say to the user:**

> "The outline has passed 50 bullet points -- the conversation is getting heavy. I'm going to trigger /compact now to free up context space. Nothing will be lost -- the outline file has everything we've confirmed."

**After compact, immediately:**

1. Read `/home/claude/outline.md` in full using the `view` tool
2. Confirm to the user: "I've re-read the outline. We're resuming at Stage [N] -- [stage name]. Ready?"


---

## STAGE 7: ACCESS, HIGHWAYS & PARKING

**Purpose:** Demonstrate safe and adequate access, parking, and transport arrangements.

**Follow the iterative loop.**

**Information to gather / discuss:**

- Existing access arrangements (vehicular and pedestrian)
- Any changes to access
- Parking provision -- existing spaces, proposed spaces, relevant standard (LPA or county)
- Cycle storage
- EV charging provision
- Refuse/recycling collection arrangements
- Highway safety -- visibility splays, turning areas
- Trip generation (for larger schemes)
- Accessibility -- Part M compliance, level access
- Proximity to public transport, shops, services (sustainability argument)

**Policy research within the loop:** Search for [district] or [county] parking standards and transport policies. Feed back what the standards require, check the user's parking/access arrangements against them.

**Append to outline.md:** Access and parking facts, policies identified, compliance narrative.

**Confirm:** "Have we fully explored access and highways? Anything to add before we move on to Environmental Considerations?"

---

## STAGE 8: ENVIRONMENTAL CONSIDERATIONS

**Purpose:** Address all environmental matters relevant to the site and proposal.

**Follow the iterative loop for each applicable sub-topic.**

**Sub-topics (discuss each, skip any that are clearly not applicable):**

### 8A: Flood Risk & Drainage
- Flood zone (from Stage 2 designations)
- Sequential test / exception test (if Zone 2/3)
- Surface water drainage strategy (SuDS)
- Foul drainage
- Any FRA submitted or required

### 8B: Ecology & Biodiversity
- Protected species surveys
- Biodiversity Net Gain (BNG) -- search for current mandatory requirements and thresholds
- Ecological enhancement measures
- Impact on designated sites (SSSI, SPA, SAC)

### 8C: Trees & Landscaping
- Trees on or adjacent to site
- TPOs
- Arboricultural impact assessment
- Proposed landscaping / planting

### 8D: Sustainability & Energy
- Part L compliance approach
- Renewable energy provision
- Fabric-first approach
- Any local sustainability policy requirements

### 8E: Contamination
- Previous uses suggesting contamination
- Any Phase 1 desk study

### 8F: Other
- Air quality
- Noise (from external sources onto the development)
- Lighting
- Waste minimisation

**Policy research within the loop:** Search for [district] environmental policies -- flood risk, ecology, sustainability, trees. Each sub-topic may trigger its own policy research and feedback cycle.

**Append to outline.md:** Environmental facts per sub-topic, policies identified, compliance narratives.

**Confirm:** "Have we fully explored the environmental considerations? Anything to add before we move on?"

---

## STAGE 9: HERITAGE (if applicable)

**Skip this stage if no heritage designations were identified in Stage 2.**

**Purpose:** Demonstrate that the proposal preserves or enhances heritage significance.

**Follow the iterative loop.**

**Information to gather / discuss:**

- What heritage assets are affected (listed building, conservation area, scheduled monument, registered park/garden, non-designated heritage asset)
- Significance of the asset(s) -- architectural, historic, archaeological, artistic
- Setting considerations
- How the proposal affects significance -- preserves, enhances, or causes harm
- If harm: level of harm (substantial or less than substantial)
- If less than substantial harm: public benefits that outweigh the harm (NPPF paragraph 208)
- If substantial harm: exceptional circumstances / substantial public benefits (NPPF paragraph 207)
- Reference to any Heritage Statement submitted with the application

**Policy research within the loop:** Search for [district] heritage policies and any relevant conservation area appraisal. If the appraisal reveals significance factors that affect earlier stages (e.g. roofscape, materials, boundary treatments), add backward references to the outline file under those earlier stage headings.

**Append to outline.md:** Heritage facts, significance analysis, harm assessment, policies identified, compliance narrative. Plus any backward references to earlier stages.

**Confirm:** "Have we fully explored the heritage considerations? Anything to add?"

---

## STAGE 10: POLICY FRAMEWORK REVIEW

**Purpose:** Bird's-eye review of the entire outline against all policies. This is NOT a data-gathering stage -- it is a review and gap-check stage.

**Action:**

1. Read `/home/claude/outline.md` in full using the `view` tool.
2. Review every stage's policy compliance narrative against the full policy framework.
3. Check for:

**Strategic-level policies not yet captured:**
- NPPF Chapter 2: Achieving sustainable development (presumption in favour)
- NPPF Chapter 4: Decision making
- Spatial strategy / settlement hierarchy policies
- Any overarching Local Plan policies that frame the entire development plan
- Neighbourhood Plan policies (if applicable)
- Relevant SPDs

**Cross-references and consistency:**
- Does the design narrative align with what was said about site context?
- Do the amenity dimensions match the proposal dimensions?
- Are all designation-specific policies identified in Stage 2 addressed in later stages?
- Do refusal reasons from Stage 3 have explicit policy responses in later stages?
- Are there any policy tests identified in one stage that should also be referenced in another?

**Gaps:**
- Any policy categories not covered? Common misses: CIL/S106, housing mix, affordable housing thresholds, accessibility, waste
- Any NPPF chapters relevant to this scheme not yet cited?
- Any Local Plan policies identified during research that haven't been addressed?

**NPPF paragraph verification:**
- Search for the current NPPF to confirm paragraph numbers cited throughout the outline. Paragraph numbers shift between NPPF versions -- verify before document generation.

**After the review:**

- Present findings to the user: "I've reviewed the full outline against all policies. Here's what I found: [gaps/issues/additions needed]."
- Discuss and resolve each finding through the iterative loop.
- Update the outline file with any additions, corrections, or cross-references.

**Append to outline.md:** Strategic policies section (NPPF sustainable development, decision-making framework, spatial strategy), any gap-fill policies, cross-reference notes, NPPF paragraph numbers confirmed.

**Confirm:** "The policy framework review is complete. Ready to move on to Consultation & Engagement?"

---

## STAGE 11: CONSULTATION & ENGAGEMENT

**Purpose:** Demonstrate that the applicant has engaged constructively with stakeholders.

**Information to gather / discuss:**

- Pre-application advice -- date, reference, officer, key points of advice and how the scheme responds
- Design Review Panel -- date, panel comments, how the scheme responds
- Neighbour engagement -- any informal discussions, letters, meetings
- Parish Council engagement
- Any public consultation events
- Statutory consultee engagement (highways, environment agency, etc.)

**Note:** Pre-app advice often directly references policies. Cross-check any policy references in the advice against the policies identified in the outline. If the officer cited a policy we haven't addressed, flag it and add it.

**Append to outline.md:** Consultation facts, any additional policies flagged from pre-app advice.

**Confirm:** "Have we fully explored consultation and engagement? Anything to add?"

---

## FINAL CHECK

After completing all applicable stages, ask:

> "We've now covered all the standard planning statement topics. The outline file is complete. Before I draft the document, are there any **unique aspects of this scheme** that aren't covered by the stages above? For example:
> - Specific material considerations the officer should weigh
> - Fallback positions (e.g. permitted development comparison)
> - Viability arguments
> - Community benefits
> - Enabling development arguments
> - Any other site-specific or scheme-specific matters
>
> Or shall I proceed to formulate the document?"

If additional topics are identified, discuss each one iteratively with the same loop, append to outline.md, and confirm before proceeding.

---

## DOCUMENT GENERATION

**When the user confirms ready to draft:**

1. Read the docx skill at `/mnt/skills/public/docx/SKILL.md`
2. Read `/home/claude/outline.md` in full -- this is the source material
3. Compile into a professional planning statement using the outline as the content skeleton
4. Structure with the following sections:

```
1.0  Introduction
2.0  Site Description and Context
3.0  Planning History
4.0  The Proposal
5.0  Design and Visual Impact
6.0  Residential Amenity
7.0  Access, Highways and Parking
8.0  Environmental Considerations
9.0  Heritage Considerations (if applicable)
10.0 Planning Policy Framework
     10.1 National Planning Policy Framework
     10.2 [District] Local Plan
     10.3 Neighbourhood Plan / SPDs (if applicable)
11.0 Consultation and Engagement
12.0 Conclusion
```

**Note on Section 10 placement in the document:** Although the Policy Framework Review was the last analytical stage (Stage 10 in the workflow), in the final document it can sit either:
- **As Section 10** (as shown above) -- after the topic-specific sections, pulling together the strategic policy argument before the conclusion. This works well because each earlier section has already cited its relevant policies inline, and Section 10 provides the overarching framework.
- **As Section 5** (traditional position) -- if the user prefers a conventional structure where policy is laid out before the topic analysis. Ask the user which they prefer before generating.

5. The Conclusion should:
   - Summarise key policy compliance points
   - State the planning balance clearly
   - End with a recommendation: "For the reasons set out in this statement, the proposal is considered to accord with the development plan and national policy. Planning permission should be granted."

6. Format as a professional .docx with:
   - Numbered sections and subsections
   - Page numbers
   - Table of contents (for longer statements)
   - Professional fonts and spacing

7. Output to `/mnt/user-data/outputs/` and present to user

---

## WRITING STYLE

- **Professional but accessible** -- a planning officer and a client should both be able to read it
- **Positive framing** -- "the proposal will enhance..." not "the proposal should not harm..."
- **Specific** -- cite policy numbers, dimensions, distances, percentages
- **Proportionate** -- a householder extension statement might be 8-12 pages; a major application could be 30+
- **No bullet points in the body** -- write in flowing paragraphs. Lists only for policy references or where genuinely clearer
- **Active voice** -- "the proposal provides..." not "it is considered that provision is made for..."
- **Avoid hedging** -- "the proposal complies with Policy [X]" not "it is considered that the proposal is broadly in accordance with the aims of Policy [X]"
- **Policy citations inline** -- each topic section should cite its relevant policies within the narrative, not just in Section 10. Section 10 provides the strategic framework; topic sections provide the detailed compliance arguments.

---

## QUICK REFERENCE: POLICY RESEARCH TRIGGERS

Policy research is now embedded in the iterative loop at every stage, not concentrated in one place. However, these are the typical policy topics searched at each stage:

| Stage | Research Topic |
|-------|---------------|
| 0 | Adopted Local Plan -- identify document name and key policies |
| 2 | Designation-specific policies (Green Belt, AONB, CA, Flood Zone) |
| 4 | Proposal-triggered policies (volume thresholds, CIL, use class) |
| 5 | Design policies, design SPD/guidance, character assessments |
| 6 | Amenity policies, separation distance guidance, daylight standards |
| 7 | Parking standards (LPA or county), transport policies |
| 8 | Environmental policies -- flood, ecology, trees, sustainability |
| 9 | Heritage policies, conservation area appraisals |
| 10 | Strategic policies, NPPF verification, gap-check across all topics |
| 11 | Cross-check any policies cited in pre-app advice |

Always ask before searching. The user may already have the policy information or may prefer to provide it themselves.

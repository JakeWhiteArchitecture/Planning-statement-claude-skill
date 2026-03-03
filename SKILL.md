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
+-------------------------------+
|  STAGE 0: PROJECT SETUP       |
|  District, site, app type     |
|  Benefit Threads identified   |
|  -> Policy research trigger   |
+-------------------------------+
  |
  v
+-------------------------------+
|  STAGE 1: INTRODUCTION        |
|  Applicant, description       |
|  -> Confirm before moving on  |
+-------------------------------+
  |
  v
+-------------------------------+
|  STAGE 2: SITE & CONTEXT      |
|  Physical, designations       |
|  -> Policy research trigger   |
|  -> Confirm before moving on  |
+-------------------------------+
  |
  v
+-------------------------------+
|  STAGE 3: PLANNING HISTORY    |
|  Previous apps, pre-app       |
|  -> Confirm before moving on  |
+-------------------------------+
  |
  v
+-------------------------------+
|  STAGE 4: THE PROPOSAL        |
|  Detailed description         |
|  -> Confirm before moving on  |
+-------------------------------+
  |
  v
+-------------------------------+
|  STAGE 5: STATUTORY FRAMEWORK |
|  s38(6), s70(2), NPPF p11    |
|  -> Confirm before moving on  |
+-------------------------------+
  |
  v
+-------------------------------+
|  STAGE 6: PRINCIPLE OF DEV    |
|  Settlement, allocation,      |
|  5YHLS, fallback              |
|  -> Policy research trigger   |
|  -> Confirm before moving on  |
+-------------------------------+
  |
  v
+-------------------------------+
|  STAGE 7: NEED &              |
|  JUSTIFICATION                |
|  Benefit Threads -> policy    |
|  Housing/economic/community   |
|  -> Policy research trigger   |
|  -> Confirm before moving on  |
+-------------------------------+
  |
  v
+-------------------------------+
|  STAGE 8: POLICY FRAMEWORK    |
|  NPPF + Local Plan + NP       |
|  -> Policy research trigger   |
|  -> Confirm before moving on  |
+-------------------------------+
  |
  v
+-------------------------------+
|  STAGE 9: DESIGN & VISUAL     |
|  Character, appearance        |
|  -> Policy research trigger   |
|  -> Confirm before moving on  |
+-------------------------------+
  |
  v
+-------------------------------+
|  STAGE 10: AMENITY            |
|  Privacy, light, noise        |
|  -> Policy research trigger   |
|  -> Confirm before moving on  |
+-------------------------------+
  |
  v
+-------------------------------+
|  STAGE 11: ACCESS & HIGHWAYS  |
|  Transport, parking           |
|  -> Policy research trigger   |
|  -> Confirm before moving on  |
+-------------------------------+
  |
  v
+-------------------------------+
|  STAGE 12: ENVIRONMENT        |
|  Flood, ecology, trees,       |
|  drainage, sustainability     |
|  -> Policy research trigger   |
|  -> Confirm before moving on  |
+-------------------------------+
  |
  v
+-------------------------------+
|  STAGE 13: HERITAGE           |
|  Listed, CA, archaeology      |
|  (skip if not applicable)     |
|  -> Policy research trigger   |
|  -> Confirm before moving on  |
+-------------------------------+
  |
  v
+-------------------------------+
|  STAGE 14: CONSULTATION       |
|  Pre-app, engagement, DRP     |
|  -> Confirm before moving on  |
+-------------------------------+
  |
  v
+-------------------------------+
|  FINAL CHECK                  |
|  Any unique topics to add?    |
|  -> Confirm ready to draft    |
+-------------------------------+
  |
  v
+-------------------------------+
|  DOCUMENT GENERATION          |
|  Compile .docx                |
|  Present to user              |
+-------------------------------+
```

---

## CRITICAL RULES

- **One stage at a time.** Never skip ahead or combine stages.
- **Confirm before moving on.** At the end of every stage, ask: "Have we fully explored this topic, or is there anything else to add before we move on?"
- **Policy research is embedded.** At relevant stages, ask: "Shall I search online for [district] Local Plan policies relevant to [this topic] before we move on?"
- **District Council must be established first.** Stage 0 must identify which LPA the application is being submitted to -- this determines all subsequent policy research.
- **Never include workmanship liability** in any text. Workmanship is the contractor's responsibility.
- **Active, professional voice.** Write as though from the applicant's architect/agent. Positive framing -- "the proposal will..." not "the proposal should..."
- **Policy citations must be specific.** Always cite policy numbers and quote or closely paraphrase the relevant policy test. Generic references like "the proposal complies with local plan policy" are not acceptable.

---

## STAGE 0: PROJECT SETUP

**Purpose:** Establish the basic parameters that determine the entire document structure and policy framework.

**Ask these questions:**

1. **Which District/Borough Council** is this application being submitted to?
2. **Never ask for applicant or site address.**
3. **What type of planning application** is this? (Householder / Full / Outline / S73 / Listed Building Consent / Prior Approval / LDC)
4. **Brief description of the proposal** -- one or two sentences is fine at this point.
5. **What are the positive attributes and benefits of this proposal?** Ask: "What do you see as the key benefits of this scheme -- for the occupants, the site, the street scene, the wider community, or sustainability? Think broadly: improved living conditions, better use of land, energy performance, biodiversity gains, economic benefits, resolving existing problems, design quality, heritage enhancement -- anything that makes this a good scheme." Record all responses as **Benefit Threads** to be woven through the statement and used to steer policy research at later stages.

**Why this matters:** Planning statements that only demonstrate policy compliance read defensively. Front-loading the scheme's positive attributes ensures that every subsequent policy research stage actively seeks out policies that *support* the proposal's benefits -- not just policies the proposal must defend against. The final document should read as a positive case for approval, not a compliance checklist.

**After receiving answers:**

- Confirm the LPA and note any known policy context -- identify the adopted Local Plan document name and plan period.
- Review the Benefit Threads and note which policy areas they are likely to engage (e.g. a sustainability benefit will need sustainability policies; a streetscape improvement will need design/character policies). Flag these for targeted research at later stages.
- Ask: "Do you know what site designations apply? For example: Green Belt, AONB, Conservation Area, Article 5, Listed buildings, Flood Zone, SSSI, Tree Preservation Orders?" -- note the answers for later stages.
- Ask: "Shall I search online for the current adopted Local Plan policies for [district] so I can reference them accurately throughout? I'll also look for policies that specifically support the benefits you've identified."

**Policy research trigger:** If user says yes, use web_search to find the adopted Local Plan and identify the key policy document(s). Fetch and note the policy numbers and document name for reference throughout. Additionally, use the Benefit Threads to search for policies that positively support the scheme's merits -- these should be noted alongside the defensive/compliance policies and referenced throughout the statement.

**Confirm:** "I've got the basic setup. Ready to move to Stage 1 -- Introduction?"

---

## STAGE 1: INTRODUCTION

**Purpose:** Establish the formal opening of the statement -- who, what, where, why.

**Information to gather:**

- Agent details (if applicable -- this will typically be Jake White Architecture)
- Application type (confirm from Stage 0)
- Full site address
- Brief development description (refine from Stage 0)
- Purpose of the statement -- e.g. "to demonstrate compliance with national and local planning policy"
- **Never request applicant details.**

**What this section will contain in the final document:**

A short introductory paragraph identifying the site, the applicant, the nature of the application, and the purpose of the statement. Typically 2-3 paragraphs.

**Confirm:** "Have we fully explored the introduction, or is there anything else to add before we move on to Site Description & Context?"

---

## STAGE 2: SITE DESCRIPTION & CONTEXT

**Purpose:** Paint a clear picture of the site for the case officer who may not have visited.

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

**Policy research trigger:** "Some of these designations have specific policy implications. Shall I search online for [district] policies relating to [relevant designations] before we move on?"

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

**Confirm:** "Have we fully explored the planning history? Anything to add before we move on to The Proposal?"

---

## STAGE 4: THE PROPOSAL

**Purpose:** Describe what is actually being proposed in sufficient detail for the case officer.

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

**Confirm:** "Have we fully described the proposal? Anything to add before we move on to Statutory Framework?"

---

## STAGE 5: STATUTORY FRAMEWORK

**Purpose:** Establish the legal basis for how planning decisions are made. This sets the rules of the game before the detailed policy assessment begins.

**Proportionality:** For householder applications, this can be a single short paragraph. For full or outline applications, it warrants a dedicated section.

**Information to cover (not gathered from user -- this is standard legal context):**

- **Section 38(6) of the Planning and Compulsory Purchase Act 2004** -- applications must be determined in accordance with the development plan unless material considerations indicate otherwise.
- **Section 70(2) of the Town and Country Planning Act 1990** -- the LPA shall have regard to the provisions of the development plan, so far as material, and to any other material considerations.
- **NPPF presumption in favour of sustainable development** (paragraph 11) -- the "tilted balance" and when it is engaged (e.g. absence of five-year housing land supply, out-of-date policies).
- **Identify the statutory development plan** for the area -- list the documents that constitute it (e.g. "The statutory development plan for this site comprises the [District] Local Plan [year], the [Neighbourhood Plan if applicable], and the [Minerals/Waste Plan if relevant]").

**Writing guidance:** This section should read as confident, factual legal context -- not defensive or over-explained. It frames the decision-making test so the reader understands what the statement is being assessed against.

**Confirm:** "Have we established the statutory framework? Anything to add before we move on to Principle of Development?"

---

## STAGE 6: PRINCIPLE OF DEVELOPMENT

**Purpose:** Establish whether the proposed development is acceptable in principle before diving into the detailed topic-by-topic assessment. This is the threshold question a case officer must answer first.

**Proportionality:** For householder applications within established residential areas, this may be a brief paragraph confirming the principle is not in dispute. For full or outline applications, especially on edge-of-settlement, Green Belt, or unallocated sites, this is a critical section that can make or break the case.

**Information to gather / discuss:**

- Is the site within the defined settlement boundary / development limit?
- Is the site allocated for development in the Local Plan?
- Is it previously developed land (PDL/brownfield)?
- What is the current use and the proposed use -- is the change of use acceptable in principle under the spatial strategy?
- If outside a settlement boundary: what policy support exists for development in this location? (e.g. NPPF paragraph 83 for rural economy, infill, rural exception sites)
- If Green Belt: which NPPF exceptions apply? (paragraphs 154-156 for new buildings, 157 for extensions/alterations, 158-159 for replacement buildings, etc.)
- **Five-year housing land supply** -- can the LPA demonstrate a five-year supply? If not, the tilted balance under NPPF paragraph 11(d) is engaged. Search for the LPA's latest housing land supply position.
- **Housing Delivery Test** -- has the LPA met the HDT threshold? If delivery is below 75%, the tilted balance is engaged.
- Any relevant precedent from planning history (Stage 3) that supports the principle.
- Any fallback position (e.g. permitted development rights that could deliver a comparable or worse outcome without planning permission).

**Policy research trigger:** "Shall I search for [district]'s latest five-year housing land supply position and any spatial strategy policies relevant to the principle of development at this location?"

**Confirm:** "Have we established the principle of development? Anything to add before we move on to Need & Justification?"

---

## STAGE 7: NEED & JUSTIFICATION FOR DEVELOPMENT

**Purpose:** Articulate *why* this development is needed -- not just that it complies with policy, but that it serves a genuine purpose and delivers tangible benefits. This section draws directly on the Benefit Threads identified in Stage 0 and translates them into planning arguments.

**Proportionality:** For householder applications, this may be a brief paragraph on personal/family need and improved living conditions. For full or outline applications, this should be a substantive section covering housing need, economic benefits, and community value.

**Information to gather / discuss:**

- **Housing need** (if residential) -- local housing need figures, affordability, tenure mix, housing type/size needed in the area
- **Personal/family need** (for householder apps) -- growing family, accessibility requirements, working from home, caring for elderly relatives
- **Economic benefits** -- construction jobs, local spending, New Homes Bonus, Council Tax revenue, business rates (if commercial)
- **Community benefits** -- public open space, affordable housing contribution, infrastructure improvements, community facilities
- **Addressing existing problems** -- resolving a poor layout, replacing a substandard building, improving energy performance of existing housing stock, removing an eyesore
- **Sustainability benefits** -- reducing carbon emissions, improving building performance, supporting sustainable transport patterns, BNG delivery
- **Any site-specific justification** -- e.g. enabling development to fund heritage restoration, agricultural diversification, rural enterprise

**Link to Benefit Threads:** Review the Benefit Threads from Stage 0 and ensure each one has been translated into a planning argument with policy support. If any threads haven't yet been connected to specific policies, flag them for the Policy Framework stage.

**Policy research trigger:** "Shall I search for [district]'s policies on [housing need / economic development / sustainability] to support the justification for this scheme?"

**Confirm:** "Have we fully articulated the need and justification? Anything to add before we move on to the Policy Framework?"

---

## STAGE 8: PLANNING POLICY FRAMEWORK

**Purpose:** Identify and analyse every relevant planning policy. This is the core of the statement.

**This stage has THREE sub-stages:**

### 5A: National Policy (NPPF)

Identify relevant NPPF chapters and paragraphs. Common ones include:

- Chapter 2: Achieving sustainable development
- Chapter 4: Decision making
- Chapter 9: Promoting sustainable transport
- Chapter 12: Achieving well-designed and beautiful places
- Chapter 13: Protecting Green Belt land (if applicable)
- Chapter 14: Meeting the challenge of climate change and flooding
- Chapter 15: Conserving and enhancing the natural environment
- Chapter 16: Conserving and enhancing the historic environment (if applicable)

For each relevant chapter, identify the specific paragraph and policy test, then explain how the proposal addresses it. **Search for the current NPPF to confirm paragraph numbers** -- these can shift between NPPF versions.

**Policy research trigger:** "Shall I search for the current NPPF paragraph numbers relevant to [topic]? Paragraph numbers change between NPPF versions."

### 5B: Local Plan Policies

**Policy research trigger:** "Shall I now search online for [district] Local Plan policies relevant to this application? I'll look for policies covering [list topics based on what we've gathered]."

For each identified Local Plan policy:
- State the policy number and name
- Quote or closely paraphrase the relevant test
- Explain in 2-3 sentences minimum how the proposal complies

**Common policy categories to search for:**
- Spatial strategy / settlement hierarchy
- Design quality / character
- Residential amenity
- Green Belt (if applicable)
- Heritage (if applicable)
- Transport and parking
- Flood risk and drainage
- Biodiversity / ecology
- Trees and landscaping
- Sustainability / energy
- Housing mix / density (if new dwellings)
- Affordable housing (if triggered)
- Infrastructure / CIL / S106

### 5C: Neighbourhood Plan / SPDs

- Check if a Neighbourhood Plan applies to the site
- Check for relevant Supplementary Planning Documents
- Identify any relevant policies and explain compliance

**Confirm:** "Have we fully covered the policy framework? Any policies I've missed, or any you'd like me to research further before we move on?"

---

## STAGE 9: DESIGN & VISUAL IMPACT

**Purpose:** Demonstrate that the proposal is well-designed and respects local character.

**Information to gather / discuss:**

- How the proposal responds to the existing building's character (form, materials, proportions, roof pitch)
- How it sits within the street scene / wider landscape
- Scale and massing -- is it subordinate, matching, or dominant?
- Materials palette and rationale
- Key design moves / architectural approach
- If in Green Belt: impact on openness (visual AND spatial)
- If in AONB/AGLV: landscape impact, views from public vantage points
- Reference to NPPF Chapter 12 and relevant local design policy
- Any Design Review Panel feedback (refer to Stage 11)

**Policy research trigger:** "Shall I search for [district]'s design policies or any relevant design SPD/guidance before we move on?"

**Confirm:** "Have we fully explored the design and visual impact? Anything to add before we move on to Amenity?"

---

## STAGE 10: RESIDENTIAL AMENITY

**Purpose:** Demonstrate the proposal does not unacceptably harm neighbours' living conditions.

**Information to gather / discuss:**

- **Privacy/overlooking** -- distance to neighbouring windows, orientation, any new windows facing neighbours, mitigation (obscure glazing, high-level, angled)
- **Daylight/sunlight** -- does the proposal project beyond the 45-degree line from neighbours' windows? Any BRE assessment? North-facing elements less impactful
- **Overbearing/sense of enclosure** -- height, proximity, bulk visible from neighbouring gardens/rooms
- **Noise/disturbance** -- any change in activity levels, plant/equipment, hours of use
- **Outlook** -- impact on neighbours' outlook from principal rooms
- **Construction impact** -- hours, access, duration (brief mention)

**Policy research trigger:** "Shall I search for [district]'s amenity policies and any specific guidance on separation distances or daylight standards?"

**Confirm:** "Have we fully explored the amenity impacts? Anything to add before we move on to Access & Highways?"

---

## STAGE 11: ACCESS, HIGHWAYS & PARKING

**Purpose:** Demonstrate safe and adequate access, parking, and transport arrangements.

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

**Policy research trigger:** "Shall I search for [district] or [county] parking standards and transport policies?"

**Confirm:** "Have we fully explored access and highways? Anything to add before we move on to Environmental Considerations?"

---

## STAGE 12: ENVIRONMENTAL CONSIDERATIONS

**Purpose:** Address all environmental matters relevant to the site and proposal.

**Sub-topics (discuss each, skip any that are clearly not applicable):**

### 9A: Flood Risk & Drainage
- Flood zone (from Stage 2 designations)
- Sequential test / exception test (if Zone 2/3)
- Surface water drainage strategy (SuDS)
- Foul drainage
- Any FRA submitted or required

### 9B: Ecology & Biodiversity
- Protected species surveys
- Biodiversity Net Gain (BNG) -- search for current mandatory requirements and thresholds
- Ecological enhancement measures
- Impact on designated sites (SSSI, SPA, SAC)

### 9C: Trees & Landscaping
- Trees on or adjacent to site
- TPOs
- Arboricultural impact assessment
- Proposed landscaping / planting

### 9D: Sustainability & Energy
- Part L compliance approach
- Renewable energy provision
- Fabric-first approach
- Any local sustainability policy requirements

### 9E: Contamination
- Previous uses suggesting contamination
- Any Phase 1 desk study

### 9F: Other
- Air quality
- Noise (from external sources onto the development)
- Lighting
- Waste minimisation

**Policy research trigger:** "Shall I search for [district]'s environmental policies -- flood risk, ecology, sustainability, trees?"

**Confirm:** "Have we fully explored the environmental considerations? Anything to add before we move on?"

---

## STAGE 13: HERITAGE (if applicable)

**Skip this stage if no heritage designations were identified in Stage 2.**

**Purpose:** Demonstrate that the proposal preserves or enhances heritage significance.

**Information to gather / discuss:**

- What heritage assets are affected (listed building, conservation area, scheduled monument, registered park/garden, non-designated heritage asset)
- Significance of the asset(s) -- architectural, historic, archaeological, artistic
- Setting considerations
- How the proposal affects significance -- preserves, enhances, or causes harm
- If harm: level of harm (substantial or less than substantial)
- If less than substantial harm: public benefits that outweigh the harm (NPPF paragraph 208)
- If substantial harm: exceptional circumstances / substantial public benefits (NPPF paragraph 207)
- Reference to any Heritage Statement submitted with the application

**Policy research trigger:** "Shall I search for [district]'s heritage policies and any relevant conservation area appraisal?"

**Confirm:** "Have we fully explored the heritage considerations? Anything to add?"

---

## STAGE 14: CONSULTATION & ENGAGEMENT

**Purpose:** Demonstrate that the applicant has engaged constructively with stakeholders.

**Information to gather / discuss:**

- Pre-application advice -- date, reference, officer, key points of advice and how the scheme responds
- Design Review Panel -- date, panel comments, how the scheme responds
- Neighbour engagement -- any informal discussions, letters, meetings
- Parish Council engagement
- Any public consultation events
- Statutory consultee engagement (highways, environment agency, etc.)

**Confirm:** "Have we fully explored consultation and engagement? Anything to add?"

---

## FINAL CHECK

After completing all applicable stages, ask:

> "We've now covered all the standard planning statement topics. Before I draft the document, are there any **unique aspects of this scheme** that aren't covered by the stages above? For example:
> - Specific material considerations the officer should weigh
> - Fallback positions (e.g. permitted development comparison)
> - Viability arguments
> - Community benefits
> - Enabling development arguments
> - Any other site-specific or scheme-specific matters
>
> Or shall I proceed to formulate the document?"

If additional topics are identified, discuss each one iteratively with the same confirm-before-moving-on approach.

---

## DOCUMENT GENERATION

**When the user confirms ready to draft:**

1. Read the docx skill at `/mnt/skills/public/docx/SKILL.md`
2. Compile all gathered information into a professional planning statement
3. Structure with the following sections:

```
1.0  Introduction
2.0  Site Description and Context
3.0  Planning History
4.0  The Proposal
5.0  Statutory Framework
6.0  Principle of Development
7.0  Need and Justification for Development
8.0  Planning Policy Framework
     8.1  National Planning Policy Framework
     8.2  [District] Local Plan
     8.3  Neighbourhood Plan / SPDs (if applicable)
9.0  Design and Visual Impact
10.0 Residential Amenity
11.0 Access, Highways and Parking
12.0 Environmental Considerations
13.0 Heritage Considerations (if applicable)
14.0 Consultation and Engagement
15.0 Conclusion
```

4. The Conclusion should:
   - Summarise key policy compliance points
   - State the planning balance clearly
   - End with a recommendation: "For the reasons set out in this statement, the proposal is considered to accord with the development plan and national policy. Planning permission should be granted."

5. Format as a professional .docx with:
   - Numbered sections and subsections
   - Page numbers
   - Table of contents (for longer statements)
   - Professional fonts and spacing

6. Output to `/mnt/user-data/outputs/` and present to user

---

## WRITING STYLE

- **Professional but accessible** -- a planning officer and a client should both be able to read it
- **Positive framing** -- "the proposal will enhance..." not "the proposal should not harm..."
- **Specific** -- cite policy numbers, dimensions, distances, percentages
- **Proportionate** -- a householder extension statement might be 8-12 pages; a major application could be 30+
- **No bullet points in the body** -- write in flowing paragraphs. Lists only for policy references or where genuinely clearer
- **Active voice** -- "the proposal provides..." not "it is considered that provision is made for..."
- **Avoid hedging** -- "the proposal complies with Policy [X]" not "it is considered that the proposal is broadly in accordance with the aims of Policy [X]"

---

## QUICK REFERENCE: POLICY RESEARCH TRIGGERS

At the following stages, offer to search online for relevant policies:

| Stage | Research Topic |
|-------|---------------|
| 0 | Adopted Local Plan -- identify document name and key policies |
| 2 | Designation-specific policies (Green Belt, AONB, CA, Flood Zone) |
| 6 | Five-year housing land supply, spatial strategy, principle of development |
| 7 | Housing need, economic development, sustainability policies to support justification |
| 8 | Full Local Plan policy audit -- design, amenity, transport, environment, heritage |
| 9 | Design policies, design SPD/guidance, character assessments |
| 10 | Amenity policies, separation distance guidance |
| 11 | Parking standards (LPA or county), transport policies |
| 12 | Environmental policies -- flood, ecology, trees, sustainability |
| 13 | Heritage policies, conservation area appraisals |

Always ask before searching. The user may already have the policy information or may prefer to provide it themselves.

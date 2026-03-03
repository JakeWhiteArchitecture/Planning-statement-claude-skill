# Planning Statement Skill

A Claude skill that produces professional planning statements for UK planning applications through a guided, stage-by-stage conversational workflow. Rather than requiring the user to write a complete brief upfront, the skill walks through each section iteratively — gathering project-specific information, researching Local Plan policies via web search, and confirming completeness at every stage before moving on. The final output is a formatted `.docx` document ready for review and further development.

## What It Does

The skill acts as a structured co-author. You provide the project details conversationally, and it builds a planning statement that:

- Cites specific Local Plan policy numbers and NPPF paragraphs (not vague references)
- Writes in an active, professional voice from the agent/architect's perspective
- Covers all material planning considerations relevant to the scheme
- Scales proportionately — a householder extension gets 8-12 pages, a major application gets 30+
- Outputs as a properly formatted Word document with numbered sections, page numbers, and table of contents

## Workflow

The skill progresses through 12 stages, one at a time, with a confirmation checkpoint at each:

| Stage | Topic | Policy Research |
|-------|-------|-----------------|
| 0 | Project Setup - LPA, application type, brief description, **Benefit Threads** | Adopted Local Plan + benefit-supporting policies |
| 1 | Introduction - agent, site address, purpose | - |
| 2 | Site Description & Context - physical description, designations | Designation-specific policies |
| 3 | Planning History - previous applications, pre-app advice | - |
| 4 | The Proposal - detailed scheme description | - |
| 5 | **Statutory Framework** - s38(6), s70(2), NPPF presumption, dev plan identification | - |
| 6 | **Principle of Development** - settlement boundary, allocation, PDL, 5YHLS, fallback | Spatial strategy, housing land supply |
| 7 | **Need & Justification** - Benefit Threads translated to planning arguments | Housing need, economic, sustainability policies |
| 8 | Policy Framework - NPPF, Local Plan, Neighbourhood Plan | Full policy audit |
| 9 | Design & Visual Impact - character, materials, scale | Design policies & SPDs |
| 10 | Residential Amenity - privacy, daylight, noise | Amenity & separation guidance |
| 11 | Access, Highways & Parking - transport, EV, cycle storage | Parking standards |
| 12 | Environmental - flood, ecology, trees, sustainability, contamination | Environmental policies |
| 13 | Heritage (if applicable) - listed buildings, conservation areas | Heritage policies & CA appraisals |
| 14 | Consultation & Engagement - pre-app, DRP, neighbour engagement | - |
| Final | Unique considerations, fallback positions, then document generation | - |

## Key Design Decisions

**One stage at a time.** The skill never skips ahead or combines stages. This prevents information gaps and keeps the conversation focused.

**Embedded policy research.** At relevant stages, the skill offers to search online for the district's adopted Local Plan policies. This means the final document cites real, current policy numbers rather than generic compliance claims.

**District-first approach.** Stage 0 must establish which Local Planning Authority the application targets - everything downstream (policy references, designation checks, parking standards) depends on this.

**Benefit Threads.** Stage 0 also captures the scheme's positive attributes and benefits early - improved living conditions, better use of land, energy performance, biodiversity gains, design quality, community benefits, or anything else that makes it a good scheme. These "Benefit Threads" steer all subsequent policy research so the skill actively hunts for policies that *support* the proposal, not just policies it must defend against. The result is a statement that reads as a positive case for approval rather than a compliance checklist.

**Statutory Framework first.** Stage 5 establishes the legal basis for decision-making (Section 38(6), Section 70(2), NPPF presumption) before any policy assessment begins. This frames the rules the case officer must apply and gives the statement authority.

**Principle before detail.** Stage 6 addresses whether the development is acceptable in principle -- settlement boundaries, site allocation, five-year housing land supply, fallback positions -- before the topic-by-topic assessment. For full and outline applications this is often the make-or-break argument.

**Need and justification.** Stage 7 translates the Benefit Threads from Stage 0 into formal planning arguments, articulating why the development is needed and what tangible benefits it delivers. This ensures the statement reads as a positive case for approval, not just a policy compliance exercise.

**Confirm before moving on.** Every stage ends with an explicit checkpoint. Nothing gets missed because the user always has the chance to add more before progressing.

**No applicant details requested.** The skill never asks for the applicant's name or personal information - only the agent, site, and scheme details.

**No workmanship liability.** The skill never includes workmanship liability in any generated text. Workmanship is the contractor's responsibility, not the designer's.

## Output Structure

The generated `.docx` follows this structure:

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

## Trigger Phrases

The skill activates on any of the following (or similar intent):

- "planning statement"
- "write a planning statement"
- "help with planning statement"
- "policy justification"
- "planning application support"
- "I need to justify this scheme to the planners"
- "help me with the policy argument"
- Design and Access Statement discussed in the context of planning policy

## Writing Style

The generated statement uses a professional but accessible tone. It favours positive framing ("the proposal will enhance..." not "the proposal should not harm..."), active voice, specific policy citations, and flowing paragraphs over bullet points. No hedging - "the proposal complies with Policy X", not "it is considered that the proposal is broadly in accordance with the aims of Policy X".

## Dependencies

- **docx skill** - used at the document generation stage to produce the formatted Word document
- **web_search** - used at policy research trigger points to find adopted Local Plan documents and specific policy wording

## Author

Jake White MCIAT - Jake White Architecture

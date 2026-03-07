---
name: pmf-research-synthesis
description: Synthesize market research and expert advice to identify the riskiest PMF dimension and update the narrative. This skill should be used after completing market research and optional expert calls to determine what to validate next.
---

# PMF Research Synthesis

This skill analyzes evidence from market research and expert advice to identify the riskiest dimension, recommend narrative updates (refinement/pivot/reset), and determine the next validation step.

## Purpose

Generate a risk prioritization analysis that:
1. Synthesizes findings from market research + expert advice across 6 dimensions
2. Calculates risk scores using evidence quality × failure impact
3. Identifies THE riskiest dimension requiring targeted validation
4. Recommends narrative updates (refinement, pivot, or reset)
5. Updates pmf-narrative.md from V1 → V2 with evidence-based changes

## When to Use This Skill

Use this skill when:
- Completed `/pmf-market-research` and have market-research-synthesis.md
- (Optional) Conducted expert calls and documented in expert-notes.md
- Ready to determine which dimension to validate next
- Following deliberate PMF framework: broad validation → identify risk → targeted validation

Do NOT use this skill when:
- Haven't run market research yet (use `/pmf-market-research` first)
- Ready to jump straight to customer interviews without prioritization
- Already know which dimension is riskiest (use `/pmf-validation-planner` directly)

## Key Concepts

**Three update types**:
1. **Refinement**: Minor clarity improvements (confidence increases from 4-6 → 7-8)
2. **Pivot**: Significant changes to 1+ dimensions (analogs support different approach)
3. **Reset**: Scrapping entire narrative (only antilogs found, not viable)

**Risk = (10 - Evidence Score) × Failure Impact**
- Evidence: 1-10 (how strong is validation from analogs + experts?)
- Impact: 1-4 (what happens if hypothesis is wrong? Low/Med/High/Critical)

## Workflow

### Phase 1: Setup and Evidence Gathering

1. **Locate required files**:
   - `pmf-narrative.md` (V1)
   - `validation/market-research-synthesis.md` (required)
   - `validation/expert-notes.md` (optional but recommended)

2. **Read all evidence into context**:
   - Load pmf-narrative V1 to understand current hypotheses
   - Load market research synthesis for analog/antilog findings
   - Load expert notes (if exists) for additional insights

3. **Verify prerequisites**:
   - Market research has findings for all 6 dimensions
   - Each dimension has confidence assessment
   - Analogs/antilogs are documented with clear patterns

### Phase 2: Evidence Analysis by Dimension

For EACH of the 6 dimensions:

1. **Extract V1 hypothesis** from pmf-narrative.md

2. **Compile evidence**:
   - Analog count and key patterns (what worked?)
   - Antilog count and failure modes (what failed?)
   - Expert advice summary (consensus or disagreement?)

3. **Assess confidence change**:
   - V1 confidence (from narrative)
   - V2 confidence (based on evidence strength)
   - Rationale for change

4. **Determine update type**:
   - ✅ Validated: 3+ analogs, no major antilogs, confidence 7-8+
   - 🔄 Refinement: 2+ analogs support general approach with nuances to incorporate
   - ⚠️ Pivot: Antilogs show current approach risky, but alternative exists
   - ❌ Reset: Only antilogs, no viable path forward

5. **Draft V2 hypothesis** (if refinement or pivot needed):
   - Incorporate analog insights
   - Avoid antilog pitfalls
   - Apply expert advice specificity

### Phase 3: Risk Scoring and Prioritization

1. **Calculate risk score for each dimension**:

| Dimension | Evidence Score (V2 confidence) | Failure Impact | Risk Score |
|-----------|-------------------------------|----------------|------------|
| Problem | {1-10} | {1-4} | {(10-score) × impact} |
| Target Audience | {1-10} | {1-4} | {(10-score) × impact} |
| Value Prop | {1-10} | {1-4} | {(10-score) × impact} |
| Competitive Advantage | {1-10} | {1-4} | {(10-score) × impact} |
| Growth Strategy | {1-10} | {1-4} | {(10-score) × impact} |
| Business Model | {1-10} | {1-4} | {(10-score) × impact} |

**Failure impact assessment**:
- Problem: Critical (if not acute, product doesn't work)
- Target Audience: High (wrong audience = can't find PMF)
- Value Prop: Medium (can iterate messaging)
- Competitive Advantage: Medium (can build different moat)
- Growth Strategy: High (can't scale without channels)
- Business Model: Critical (unprofitable = unsustainable)

2. **Identify riskiest dimension**: Highest risk score

3. **Explain why it's riskiest**:
   - Evidence gaps (what don't we know?)
   - Failure consequences (what happens if wrong?)
   - Urgency (can we afford to be wrong?)

### Phase 4: Update PMF Narrative to V2

1. **Load current pmf-narrative.md**

2. **Add version history entry**:
```markdown
### V2: Post-Market Research & Expert Advice (YYYY-MM-DD)
**Changes**:
- Refined {dimension}: {specific change based on analog pattern}
- Pivoted {dimension}: from {old} to {new} based on {antilog + expert consensus}
- Identified {dimension} as riskiest (confidence: {score}/10)
```

3. **Update each dimension's narrative text** with:
   - Refinements (new insights from analogs)
   - Pivots (significant approach changes)
   - Evidence citations ("Analogs X, Y, Z showed...")

4. **Update validation status table**:
   - New confidence scores (V1 → V2)
   - Mark riskiest dimension with "Yes"
   - Update overall confidence average
   - Change recommended next step

5. **Save updated narrative** as V2

### Phase 5: Generate Risk Prioritization Report

1. **Load template**: `assets/risk-prioritization-template.md`

2. **Populate with analysis**:
   - Executive summary (confidence change, riskiest dimension)
   - Per-dimension evidence analysis
   - Risk scoring table with rankings
   - Riskiest dimension deep dive (why it matters, what could go wrong)
   - Recommended next steps

3. **Save report**: `validation/risk-prioritization.md`

### Phase 6: Recommend Next Steps

Based on overall confidence and riskiest dimension:

**Decision tree**:
```
Overall confidence >7/10?
├─ YES → Run `/pmf-interview-prep` (validate with customers)
└─ NO → Check riskiest dimension confidence
    ├─ 7+ → Proceed to interviews (low risk)
    ├─ 4-6 → Run `/pmf-validation-planner` (targeted validation needed)
    └─ <4 → Consider more research or pivot before expensive validation
```

**Specific recommendations**:
- "Your riskiest dimension is {X}. Run `/pmf-validation-planner` to design targeted validation."
- "Growth Strategy needs a smoke test to validate channel hypothesis before building product."
- "3+ dimensions still risky. Recommend additional expert calls before validation."

Display to user:
```
✅ Synthesis Complete

**Overall confidence**: {V1}/10 → {V2}/10 ({change})
**Riskiest dimension**: {Dimension} (Confidence: {score}/10, Risk score: {score})

**Recommended action**: {Specific next step}

**Files updated**:
- pmf-narrative.md (V1 → V2)
- validation/risk-prioritization.md (new)
```

## Quality Gates

Before completing:
1. All 6 dimensions analyzed with evidence summary
2. V2 confidence scores assigned with rationale
3. Risk scores calculated using formula
4. Riskiest dimension clearly identified and explained
5. PMF narrative updated to V2 with version history
6. Specific next step recommended (not vague "do more research")
7. Risk prioritization report saved

## Tips

1. **Weight recent evidence higher**: 2024-2026 analogs > 2015 examples
2. **Multiple experts > single expert**: Look for consensus
3. **Expert advice vs analogs conflict**: Investigate why (context differences?)
4. **Don't ignore antilogs**: They reveal hidden risks
5. **Dimension interdependencies**: Some dimensions affect others (document this)

## Reference Files

- **Synthesis framework**: `references/synthesis-framework.md`
- **Risk prioritization template**: `assets/risk-prioritization-template.md`

## Post-Skill Actions

After completing:
1. Review updated pmf-narrative.md V2
2. Review risk-prioritization.md for detailed analysis
3. Run next recommended skill (typically `/pmf-validation-planner` or `/pmf-interview-prep`)

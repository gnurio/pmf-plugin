# PMF Risk Prioritization

**Product**: {Product Name}
**Analysis Date**: {YYYY-MM-DD}
**Input**: pmf-narrative.md V1 + market-research-synthesis.md + expert-notes.md
**Output**: pmf-narrative.md V2 + this risk prioritization analysis

---

## Executive Summary

**Overall confidence change**: {V1 average}/10 → {V2 average}/10 ({+/- change})

**Update type**: {Refinement / Pivot / Reset}

**Riskiest dimension**: {Dimension Name} (Confidence: {score}/10, Impact: {High/Critical})

**Recommended next step**: {Specific action - e.g., "Run targeted validation on Growth Strategy using smoke test"}

---

## Evidence Analysis by Dimension

### Dimension 1: Problem to Solve

**V1 Hypothesis**:
{Copy from V1 narrative}

**Evidence Gathered**:
- **Analogs**: {count} - {brief summary of what they validated}
- **Antilogs**: {count} - {brief summary of failure patterns}
- **Expert advice**: {summary of expert consensus or disagreement}

**V1 Confidence**: {score}/10
**V2 Confidence**: {score}/10
**Change rationale**: {Why confidence increased/decreased/stayed same}

**Update type**: ✅ Validated / 🔄 Refinement needed / ⚠️ Pivot needed / ❌ Reset needed

**V2 Hypothesis** (if changed):
{Updated problem statement with refinements or pivots}

---

### Dimension 2: Target Audience

**V1 Hypothesis**:
{Copy from V1 narrative}

**Evidence Gathered**:
- **Analogs**: {count} - {summary}
- **Antilogs**: {count} - {summary}
- **Expert advice**: {summary}

**V1 Confidence**: {score}/10
**V2 Confidence**: {score}/10
**Change rationale**: {Why}

**Update type**: ✅ Validated / 🔄 Refinement needed / ⚠️ Pivot needed / ❌ Reset needed

**V2 Hypothesis** (if changed):
{Updated target audience}

---

### Dimension 3: Value Proposition

**V1 Hypothesis**:
{Copy from V1 narrative}

**Evidence Gathered**:
- **Analogs**: {count} - {summary}
- **Antilogs**: {count} - {summary}
- **Expert advice**: {summary}

**V1 Confidence**: {score}/10
**V2 Confidence**: {score}/10
**Change rationale**: {Why}

**Update type**: ✅ Validated / 🔄 Refinement needed / ⚠️ Pivot needed / ❌ Reset needed

**V2 Hypothesis** (if changed):
{Updated value prop}

---

### Dimension 4: Competitive Advantage

**V1 Hypothesis**:
{Copy from V1 narrative}

**Evidence Gathered**:
- **Analogs**: {count} - {summary}
- **Antilogs**: {count} - {summary}
- **Expert advice**: {summary}

**V1 Confidence**: {score}/10
**V2 Confidence**: {score}/10
**Change rationale**: {Why}

**Update type**: ✅ Validated / 🔄 Refinement needed / ⚠️ Pivot needed / ❌ Reset needed

**V2 Hypothesis** (if changed):
{Updated competitive advantage}

---

### Dimension 5: Growth Strategy

**V1 Hypothesis**:
{Copy from V1 narrative}

**Evidence Gathered**:
- **Analogs**: {count} - {summary}
- **Antilogs**: {count} - {summary}
- **Expert advice**: {summary}

**V1 Confidence**: {score}/10
**V2 Confidence**: {score}/10
**Change rationale**: {Why}

**Update type**: ✅ Validated / 🔄 Refinement needed / ⚠️ Pivot needed / ❌ Reset needed

**V2 Hypothesis** (if changed):
{Updated growth strategy}

---

### Dimension 6: Business Model

**V1 Hypothesis**:
{Copy from V1 narrative}

**Evidence Gathered**:
- **Analogs**: {count} - {summary}
- **Antilogs**: {count} - {summary}
- **Expert advice**: {summary}

**V1 Confidence**: {score}/10
**V2 Confidence**: {score}/10
**Change rationale**: {Why}

**Update type**: ✅ Validated / 🔄 Refinement needed / ⚠️ Pivot needed / ❌ Reset needed

**V2 Hypothesis** (if changed):
{Updated business model}

---

## Risk Scoring Analysis

| Dimension | Evidence Score (1-10) | Failure Impact (Low=1, Med=2, High=3, Critical=4) | Risk Score | Rank |
|-----------|----------------------|--------------------------------------------------|------------|------|
| Problem | {score} | {impact} | {(10-score) × impact} | {rank} |
| Target Audience | {score} | {impact} | {(10-score) × impact} | {rank} |
| Value Prop | {score} | {impact} | {(10-score) × impact} | {rank} |
| Competitive Advantage | {score} | {impact} | {(10-score) × impact} | {rank} |
| Growth Strategy | {score} | {impact} | {(10-score) × impact} | {rank} |
| Business Model | {score} | {impact} | {(10-score) × impact} | {rank} |

**Riskiest dimension**: {Dimension with highest risk score}

---

## Riskiest Dimension Deep Dive

### {Riskiest Dimension Name}

**Why this is the riskiest**:
- Evidence score: {score}/10 ({Low/Moderate/High risk})
- If wrong, the impact is: {Critical/High/Medium/Low}
- Combined risk score: {score} (highest among all dimensions)

**Specific risks identified**:
1. {Risk 1 from antilogs or lack of analogs}
2. {Risk 2 from expert warnings}
3. {Risk 3 from market research patterns}

**Why this dimension matters more than others right now**:
{Explain failure impact - e.g., "If we can't find scalable growth channels, we'll run out of runway before achieving PMF, regardless of how good the product is"}

**Evidence gaps**:
{What do we still not know about this dimension?}

---

## Recommended Next Steps

### Immediate Action

**Update PMF Narrative to V2**:
- Apply all refinements and pivots identified above
- Update confidence scores in validation status table
- Add version history entry explaining changes

**Path Forward**:

**If overall confidence >7/10**:
→ Proceed to customer validation with `/pmf-interview-prep`
- Riskiest dimension can be validated through interviews alongside other dimensions

**If riskiest dimension confidence 4-6/10**:
→ Run targeted validation on riskiest dimension using `/pmf-validation-planner`
- Design specific experiment (survey, smoke test, growth test) to de-risk this dimension
- Then proceed to customer interviews after validation

**If riskiest dimension confidence <4/10**:
→ Consider additional research or pivot before expensive validation
- Option 1: More expert calls focused on this dimension
- Option 2: Deeper analog research on specific tactics for this dimension
- Option 3: Pivot approach based on antilog lessons before validating

**If 3+ dimensions confidence <5/10**:
→ Too many risks to validate efficiently
- Prioritize: Focus only on top 2 riskiest dimensions
- Sequence: Validate highest-risk dimension first, then reassess

---

## Dimension Interdependencies

{Analyze how dimensions affect each other}

**Example**:
- Growth Strategy depends on Value Prop (can't grow if messaging doesn't resonate)
- Business Model depends on Target Audience (pricing tied to willingness to pay)
- Competitive Advantage depends on Problem acuteness (switching costs only work if problem is acute)

**Implication for validation sequencing**:
{Should you validate dependencies first? Or can dimensions be validated independently?}

---

## Confidence in This Analysis

**Strength of evidence**:
- Market research: {Strong/Moderate/Weak} - {number} analogs/antilogs across dimensions
- Expert advice: {Strong/Moderate/Weak} - {number} experts consulted, {level of consensus}

**Analysis limitations**:
{What could we be wrong about? What assumptions are we making?}

**Recommendation confidence**: {High/Medium/Low}
- High: Clear evidence patterns, expert consensus, obvious riskiest dimension
- Medium: Mixed signals, but preponderance of evidence supports recommendation
- Low: Limited evidence, conflicting expert advice, multiple dimensions equally risky

---

## Notes

{Any additional context, caveats, or observations that don't fit above}

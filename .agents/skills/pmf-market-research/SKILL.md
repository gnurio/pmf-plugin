---
name: pmf-market-research
description: Conduct comprehensive market research across 6 PMF dimensions by identifying analogs (successes) and antilogs (failures) in parallel. This skill should be used after creating an initial PMF narrative (V1) to validate hypotheses with external market evidence before investing in customer interviews.
---

# PMF Market Research

This skill automates comprehensive market research to validate the 6 PMF dimensions using analogs (successful examples) and antilogs (failure cases). It reduces weeks of manual research into 10-15 minutes through parallel research agents.

## Purpose

Generate a market research synthesis document that:
1. Identify 10+ analogs and antilogs per PMF dimension through parallel web research
2. Analyze patterns across successful and failed products to validate or invalidate hypotheses
3. Assess confidence changes for each dimension based on market evidence
4. Identify the riskiest dimension(s) requiring targeted validation
5. Provide specific refinement recommendations for the PMF narrative

## When to Use This Skill

Use this skill when:
- Have completed initial PMF narrative (V1) using `/pmf-hypothesis-builder`
- Need to validate hypotheses with market evidence before customer interviews
- Want to identify the riskiest dimension to focus validation efforts
- Following a deliberate risk validation approach (broad validation first)

Do NOT use this skill when:
- Don't have a pmf-narrative.md file yet (use `/pmf-hypothesis-builder` first)
- Already completed market research (check for existing `validation/market-research-synthesis.md`)
- Ready for customer validation (use `/pmf-interview-prep` after market research)
- Measuring PMF for existing product (use `/pmf-metrics-setup` instead)

## Key Concepts

**Analogs**: Products/companies that succeeded with similar approaches. Study them to understand what works.
- Threshold: $10M+ revenue (demonstrates PMF, not just early traction)
- Look for: Sustained growth, clear success patterns, relevant dimension alignment

**Antilogs**: Products/companies that failed despite similar approaches. Study them to avoid mistakes.
- Threshold: Raised funding or had traction (not idea-stage failures)
- Look for: Clear failure modes, relevant dimension misalignment, documented postmortems

**Why both matter**: Analogs show what's possible; antilogs reveal hidden risks. Spotify example: Pandora (analog for streaming viability) + Napster (antilog for licensing issues) = identified business model as riskiest dimension.

## Workflow

### Phase 1: Setup and Validation

1. **Locate PMF narrative**: Use Glob to find `**/pmf-*/pmf-narrative.md`

2. **Verify prerequisites**:
   - Confirm pmf-narrative.md exists and contains V1 with all 6 dimensions defined
   - Check if market-research-synthesis.md already exists (avoid duplicate work)
   - Read pmf-narrative.md into context

3. **Confirm with user**:
   Use AskUserQuestion to confirm proceeding with full research across all 6 dimensions

### Phase 2: Parallel Research Execution

**Critical**: Launch 6 parallel research agents (one per dimension) using Task tool with subagent_type="general-purpose".

For EACH dimension, the research agent should:
1. Use WebSearch to identify 3-5 analogs (successful companies with $10M+ revenue)
2. Use WebSearch to identify 2-3 antilogs (failed companies with documented postmortems)
3. Analyze patterns and synthesize insights
4. Assess confidence level (1-10) based on evidence strength

**Research focus by dimension**:

**Dimension 1 - Problem to Solve**:
- Analogs: Customer testimonials showing problem acuteness, must-have product adoption
- Antilogs: "Solution looking for a problem" failures, nice-to-have products that failed
- Search terms: "acute customer problem {industry}", "must-have vs nice-to-have"

**Dimension 2 - Target Audience**:
- Analogs: Clear ICP definitions, successful "now" segment focus before expansion
- Antilogs: "Tried to serve everyone" failures, wrong target audience mistakes
- Search terms: "ICP definition {industry}", "early adopter characteristics"

**Dimension 3 - Value Proposition**:
- Analogs: Strong NPS, clear positioning, benefits customers cite as valuable
- Antilogs: Poor resonance, "nobody understood what we did", high churn
- Search terms: "value proposition messaging {industry}", "benefits vs features"

**Dimension 4 - Competitive Advantage**:
- Analogs: Built one of 7 Powers, sustained market leadership, pricing power
- Antilogs: Commoditization, undercut on price, copied by incumbents
- Search terms: "7 Powers {industry}", "moat building", "competitive advantage case study"

**Dimension 5 - Growth Strategy**:
- Analogs: Found scalable channels, efficient CAC, organic growth loops
- Antilogs: Unsustainable CAC, reliance on non-scalable channels, growth stalled
- Search terms: "growth channels {product type}", "scalable acquisition", "CAC efficiency"

**Dimension 6 - Business Model**:
- Analogs: Positive unit economics, clear path to profitability, sustainable LTV:CAC
- Antilogs: Negative unit economics at scale, pricing too low, broken business equation
- Search terms: "unit economics {product type}", "pricing strategy", "path to profitability"

Launch all 6 research tasks in parallel for maximum efficiency.

### Phase 3: Research Synthesis

After all 6 research agents complete:

1. **Load synthesis template**: Read `assets/market-research-synthesis-template.md`

2. **Compile findings**: For each dimension:
   - Extract analog examples from research agent output
   - Extract antilog examples from research agent output
   - Summarize patterns identified by agent
   - Document confidence change (before → after research)
   - Mark validation status (✅ Validated / ⚠️ Needs more research / ❌ At risk)

3. **Cross-dimension analysis**:
   - Identify themes across multiple dimensions
   - List dimensions with strong validation (3+ analogs, no antilogs)
   - List dimensions at risk (multiple antilogs, or no analogs found)
   - Document unexpected insights

4. **Risk prioritization**:
   - Rank dimensions by risk level (consider both confidence and impact)
   - Identify THE riskiest dimension (lowest confidence + highest impact if wrong)
   - Explain rationale for risk ranking

5. **Generate recommendations**:
   - **Refinement**: Minor adjustments to increase clarity based on analog patterns
   - **Pivot**: Significant changes needed based on antilog warnings
   - **Reset**: Only antilogs found, current approach not viable
   - **Expert advice**: Recommend 2-3 domain experts to consult for ambiguous dimensions

6. **Populate template**: Fill all sections of market-research-synthesis-template.md with compiled findings

7. **Save synthesis**: Write to `{pmf-project-folder}/validation/market-research-synthesis.md`

### Phase 4: Completion and Next Steps

1. **Display summary to user**:
   ```
   ✅ Market Research Complete

   **Analogs identified**: {total count} across {count} dimensions
   **Antilogs identified**: {total count} across {count} dimensions

   **Dimensions validated** (✅): {list}
   **Dimensions at risk** (❌): {list}

   **Riskiest dimension**: {dimension name}
   **Confidence**: {score}/10

   **Recommended action**: {Refinement / Pivot / Reset}

   Full synthesis saved to: {file-path}
   ```

2. **Recommend next step**:
   - If refinement needed: "Review synthesis, then run `/pmf-research-synthesis` after expert calls"
   - If pivot needed: "Review findings carefully - significant changes recommended before proceeding"
   - If reset needed: "Current approach not viable based on market evidence. Consider new hypothesis"

## Quality Gates

Before completing the skill, verify:

1. **All 6 dimensions researched**: Each has at least 2-3 analogs OR antilogs
2. **Evidence quality**: Analogs meet $10M+ threshold, antilogs have documented failure modes
3. **Source diversity**: Not all findings from same source (diversify across case studies, reports, interviews)
4. **Pattern identification**: Clear synthesis of what worked/failed, not just list of companies
5. **Confidence assessment**: Each dimension has updated confidence score with rationale
6. **Risk prioritization**: Riskiest dimension clearly identified with supporting evidence
7. **Actionable recommendations**: Specific refinements suggested, not vague "do more research"

If any quality gate fails, run additional research or prompt user for manual supplementation.

## Tips for Effective Research

1. **Search strategy diversity**: Combine different search approaches:
   - Company-specific: "{company name} case study {dimension}"
   - Problem-specific: "{specific problem} success stories"
   - Failure-focused: "{dimension} startup postmortem"
   - Academic: "research on {dimension} in {product type}"

2. **Source prioritization**:
   - **High value**: First Round Review, a16z blog, Y Combinator, company teardowns, founder case studies
   - **Medium value**: TechCrunch profiles, Forbes articles, industry reports
   - **Lower value**: Generic blog posts, uncited claims

3. **Analog quality over quantity**: Better to have 3 strong analogs with clear patterns than 10 weak ones

4. **Antilog interpretation**: Focus on WHY they failed, not just THAT they failed

5. **Pattern recognition**: Look for commonalities across multiple analogs (convergence = strong signal)

6. **Context awareness**: Consider differences in market timing, resources, competition when applying analog lessons

## Common Pitfalls to Avoid

1. **Confirmation bias**: Don't only search for analogs that support hypothesis - actively seek antilogs
2. **Vanity metrics**: $10M revenue threshold prevents mistaking early traction for PMF
3. **Surface-level research**: "They succeeded" is not enough - understand specific tactics/strategies
4. **Ignoring context**: Analog from 2010 may not apply in 2026 market conditions
5. **Over-indexing on outliers**: One unicorn analog doesn't validate approach if most antilogs failed
6. **Skipping synthesis**: List of companies is not insight - must identify patterns

## Reference Files

- **Detailed criteria**: `references/analog-antilog-criteria.md` (load for research quality standards)
- **Synthesis template**: `assets/market-research-synthesis-template.md` (load when generating report)

## Post-Skill Actions

After completing this skill, the user should:
1. Review the generated `validation/market-research-synthesis.md` file
2. (Optional but recommended) Talk to 2-3 domain experts and document in `validation/expert-notes.md`
3. Run `/pmf-research-synthesis` to integrate expert advice and update narrative to V2
4. Then run `/pmf-interview-prep` to validate with customers

## Example Output Structure

The skill generates a comprehensive synthesis with this structure:
- Executive summary (key findings, confidence changes, riskiest dimension)
- Per-dimension analysis (analogs, antilogs, patterns, confidence, validation status)
- Cross-dimension themes
- Risk prioritization ranking
- Specific refinement recommendations
- Research sources cited

This provides an evidence-based foundation for deciding whether to proceed, pivot, or reset the PMF hypothesis.

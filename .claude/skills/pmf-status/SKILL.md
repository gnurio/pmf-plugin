---
name: pmf-status
description: Show current PMF project status and recommend next action. This skill should be used when checking where you are in the PMF workflow or deciding what to do next.
---

# PMF Status

This skill provides a quick overview of your current PMF validation state and recommends the next skill to run in the workflow.

## Purpose

Display current status showing:
1. Which PMF workflow stage you're in (Hypothesis → Broad Validation → Targeted Validation → Measurement)
2. What artifacts exist (narrative version, research files, interview count, etc.)
3. Overall confidence level and riskiest dimension
4. Specific next recommended action

## When to Use This Skill

Use this skill when:
- Starting a PMF session and need to know where you left off
- Completed a skill and want to confirm next step
- Have multiple PMF projects and need to check status of one
- Want to see progress overview before presenting to stakeholders

Always safe to use - this is a read-only skill that won't modify anything.

## Workflow

### Phase 1: Locate PMF Project

1. **Search for PMF projects**:
   ```
   Use Glob: **/pmf-*/pmf-narrative.md
   ```

2. **If multiple projects found**: 
   Use AskUserQuestion to select which project to show status for

3. **If no projects found**:
   Display: "No PMF projects found. Run `/pmf-hypothesis-builder` to create one."

### Phase 2: Detect Workflow State

Read and analyze project folder to determine state:

**Artifacts to check**:
- `pmf-narrative.md` (exists? which version?)
- `validation/market-research-synthesis.md` (exists?)
- `validation/expert-notes.md` (exists?)
- `validation/risk-prioritization.md` (exists?)
- `interviews/` (how many debrief files?)
- `validation/interview-synthesis.md` (exists?)
- `validation/targeted-validation-plan.md` (exists?)
- `measurement/pmf-metrics.md` (exists?)

**Workflow stages** (determined by artifacts):

1. **Stage 0: No project**
   - Artifacts: None
   - Status: "Not started"
   - Next: `/pmf-hypothesis-builder`

2. **Stage 1: Initial Hypothesis**
   - Artifacts: pmf-narrative.md V1 only
   - Status: "Hypothesis created, broad validation not started"
   - Next: `/pmf-market-research`

3. **Stage 2A: Market Research In Progress**
   - Artifacts: V1 + market-research-synthesis.md
   - Status: "Market research complete, synthesis pending"
   - Next: "Conduct expert calls (optional), then run `/pmf-research-synthesis`"

4. **Stage 2B: Broad Validation Complete**
   - Artifacts: V1 + market-research + risk-prioritization + pmf-narrative V2
   - Status: "Broad validation complete, riskiest dimension identified"
   - Next: Check confidence → interview prep or targeted validation

5. **Stage 3A: PMF Interviews In Progress**
   - Artifacts: V2 + interviews/debrief-*.md files
   - Status: "Conducted {count} PMF interviews, {X} remaining for 30-50 target"
   - Next: "Continue interviews, then run `/pmf-interview-synthesis`"

6. **Stage 3B: Interviews Complete, Synthesis Pending**
   - Artifacts: V2 + 30+ debrief files, no interview-synthesis.md
   - Status: "Interviews complete, ready for synthesis"
   - Next: `/pmf-interview-synthesis`

7. **Stage 3C: Ready for Targeted Validation**
   - Artifacts: V3 (post-interviews) + riskiest dimension confirmed
   - Status: "PMF interviews complete, ready for targeted validation"
   - Next: `/pmf-validation-planner`

8. **Stage 4: Targeted Validation In Progress**
   - Artifacts: V3+ + targeted-validation-plan.md
   - Status: "Running {technique} to validate {dimension}"
   - Next: "Complete validation, then run `/pmf-validation-results-analyzer`"

9. **Stage 5: Ready to Build & Measure**
   - Artifacts: V4+ with all dimensions confidence >7
   - Status: "PMF hypothesis validated, ready to build MVP"
   - Next: "Build product, then run `/pmf-metrics-setup`"

10. **Stage 6: Measuring PMF**
    - Artifacts: pmf-metrics.md exists
    - Status: "MVP live, measuring PMF metrics"
    - Next: "Collect data, then run `/pmf-status-evaluator`"

### Phase 3: Read Key Metrics

From `pmf-narrative.md`, extract:
- Current version (V1, V2, V3, etc.)
- Last updated date
- Product name and type
- Overall confidence (average across 6 dimensions)
- Riskiest dimension
- Validation status table

From other files (if they exist):
- Number of analogs/antilogs found (from market-research-synthesis.md)
- Number of interviews conducted (count debrief files)
- Targeted validation technique used (from validation plan)

### Phase 4: Display Status

Format output clearly:

```
# PMF Status: {Product Name}

**Stage**: {Stage name from above}
**Last updated**: {date from narrative}
**Overall confidence**: {average}/10
**Riskiest dimension**: {dimension} (Confidence: {score}/10)

## Current State

**PMF Narrative**: Version {V#}
**Artifacts present**:
- ✅ pmf-narrative.md (V{#})
- ✅/❌ validation/market-research-synthesis.md
- ✅/❌ validation/expert-notes.md
- ✅/❌ validation/risk-prioritization.md
- ✅/❌ interviews/{count} debrief files
- ✅/❌ validation/interview-synthesis.md
- ✅/❌ validation/targeted-validation-plan.md
- ✅/❌ measurement/pmf-metrics.md

## Progress by Dimension

| Dimension | Confidence | Status | Last Validated |
|-----------|------------|--------|----------------|
| Problem | {score}/10 | {✅ Validated / ⚠️ Needs validation / ❌ At risk} | {Stage where last updated} |
| Target Audience | {score}/10 | {status} | {stage} |
| Value Prop | {score}/10 | {status} | {stage} |
| Competitive Advantage | {score}/10 | {status} | {stage} |
| Growth Strategy | {score}/10 | {status} | {stage} |
| Business Model | {score}/10 | {status} | {stage} |

## Recommended Next Action

**Next skill**: `/pmf-{skill-name}`

**Why**: {1-2 sentence explanation of why this is the next step}

**Estimated time**: {time estimate for next skill}

**Prerequisites**: {Any manual work needed before running next skill}
```

### Phase 5: Provide Context

After displaying status, optionally explain:
- **If behind schedule**: "Typical timeline is {X} weeks for this stage, you're at {Y} weeks"
- **If stuck**: "Confidence hasn't increased in {N} versions - consider expert calls or pivot"
- **If ready to proceed**: "All prerequisites met, can run next skill immediately"

## Tips for Status Interpretation

**Confidence score trends**:
- Increasing (V1: 5 → V2: 7): Good, evidence validates hypothesis
- Flat (V1: 5 → V2: 5): Needs more validation, or consider pivot
- Decreasing (V1: 6 → V2: 4): Evidence contradicts hypothesis, pivot likely needed

**Workflow bottlenecks**:
- Stuck at market research: Need expert calls or deeper analog research
- Stuck at interviews: Need more participants or better screener questions
- Stuck at targeted validation: Validation technique not yielding clear results

**When to skip ahead**:
- High confidence (8+) across all dimensions after broad validation → Skip interviews, go straight to MVP
- Established org with existing product → Skip early stages, start at measurement

## Quality Checks

Status display should:
1. Clearly state current stage in workflow
2. Show which artifacts exist vs. missing
3. Recommend specific next skill (not vague "continue validation")
4. Provide confidence scores for all 6 dimensions
5. Highlight riskiest dimension
6. Estimate time for next step

## Example Status Output

```
# PMF Status: TaskMaster Pro

**Stage**: Broad Validation Complete
**Last updated**: 2026-01-20
**Overall confidence**: 6.2/10 → 7.0/10 (+0.8)
**Riskiest dimension**: Growth Strategy (Confidence: 5/10)

## Current State

**PMF Narrative**: Version V2 (Post-market research & expert advice)
**Artifacts present**:
- ✅ pmf-narrative.md (V2)
- ✅ validation/market-research-synthesis.md (38 analogs, 15 antilogs)
- ✅ validation/expert-notes.md (3 expert calls documented)
- ✅ validation/risk-prioritization.md
- ❌ interviews/ (0 interviews conducted)

## Progress by Dimension

| Dimension | Confidence | Status | Last Validated |
|-----------|------------|--------|----------------|
| Problem | 8/10 | ✅ Validated | Market research (V2) |
| Target Audience | 7/10 | ✅ Validated | Expert advice (V2) |
| Value Prop | 7/10 | ✅ Validated | Market research (V2) |
| Competitive Advantage | 6/10 | ⚠️ Needs validation | Market research (V2) |
| Growth Strategy | 5/10 | ⚠️ Needs validation (RISKIEST) | Expert advice (V2) |
| Business Model | 8/10 | ✅ Validated | Market research (V2) |

## Recommended Next Action

**Next skill**: `/pmf-interview-prep`

**Why**: Broad validation complete with moderate overall confidence (7.0/10). PMF interviews will validate all dimensions with target customers and confirm Growth Strategy is truly the riskiest before investing in targeted validation.

**Estimated time**: 30 min to prepare script + 3-4 weeks to conduct 30-50 interviews

**Prerequisites**: None - ready to proceed immediately
```

This status skill provides quick navigation and awareness of where you are in the PMF workflow.

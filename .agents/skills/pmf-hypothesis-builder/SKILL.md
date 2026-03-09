---
name: pmf-hypothesis-builder
description: Guide user through defining initial PMF narrative with 6 dimensions, confidence scores, and validation priorities. This skill should be used when starting a new product-market fit discovery process or formalizing an initial product insight into a structured hypothesis.
---

# PMF Hypothesis Builder

This skill guides the user through creating a structured initial Product-Market Fit (PMF) narrative across 6 dimensions. It transforms an initial product insight into a comprehensive hypothesis ready for validation.

## Purpose

Create a Version 1 PMF Narrative document that:
1. Defines all 6 PMF dimensions with clarity and specificity
2. Assesses confidence levels for each dimension
3. Identifies the riskiest dimension(s) requiring validation
4. Establishes a baseline for iterative refinement through evidence gathering

## When to Use This Skill

Use this skill when:
- Starting a new product-market fit discovery process for a zero-to-one startup
- Formalizing a product idea within an established organization
- Creating a new product extension and need to validate PMF
- The user has an initial insight but hasn't structured it into the 6 PMF dimensions
- Restarting PMF discovery after a major pivot or reset

Do NOT use this skill when:
- The user already has a complete PMF narrative document (use `/pmf-status` instead)
- The user needs to validate an existing hypothesis (use `/pmf-market-research` instead)
- The user is measuring PMF for an existing product (use `/pmf-metrics-setup` instead)

## Workflow

### Phase 1: Setup and Context Gathering

1. **Ask for project location preference**:
   Use AskUserQuestion to determine where to create the PMF project folder:

   ```
   Question: "Where should the PMF project folder be created?"
   Header: "Location"
   Options:
   1. "Obsidian vault (01 PROJECTS/pmf-{product-name}/) - Recommended"
      Description: "Integrates with existing PARA system, searchable, synced via iCloud"
   2. "Custom location (user specifies path)"
      Description: "Standalone folder outside vault for cleaner separation"
   ```

2. **Gather initial context**:
   Use AskUserQuestion to collect essential information before building the narrative:

   ```
   Question 1: "What type of product are you building?"
   Header: "Product Type"
   Options:
   - "B2C SaaS" / "B2B SaaS" / "Marketplace" / "DTC E-commerce" / "Other"

   Question 2: "What is your organizational context?"
   Header: "Org Context"
   Options:
   - "Zero-to-one startup (new company)"
   - "New product in established organization"
   - "Product extension/feature expansion"
   ```

   **If product type is B2B SaaS or Marketplace:**
   Use AskUserQuestion:
   ```
   Question: "This product has multiple user roles. Should we define PMF dimensions separately for each role?"
   Header: "Multi-Role"
   Options:
   - "Yes, define separately (Recommended)" - Creates richer, more accurate hypothesis
   - "No, keep unified" - Simpler, but may miss role-specific nuances
   ```

   If user selects "Yes":
   - For B2B: "We'll consider Decision-Makers (who buy) vs End-Users (who use)"
   - For Marketplace: "We'll consider Demand Side (buyers) vs Supply Side (sellers)"

   Note: If multi-role approach is selected, guide user through dimensions for each role separately, then synthesize.

3. **Create project folder structure**:
   ```
   {project-root}/pmf-{product-name}/
   ├── pmf-narrative.md          # To be created in this skill
   ├── research/                 # Empty, for future use
   ├── validation/               # Empty, for future use
   ├── interviews/               # Empty, for future use
   └── measurement/              # Empty, for future use
   ```

### Phase 2: Interactive Narrative Building

Guide the user through defining each dimension in sequence. Use the `references/pmf-framework.md` file for detailed criteria and examples.

#### Step 1: Initial Insight Quality Check

Before defining dimensions, validate the initial insight meets quality criteria:

Use AskUserQuestion to assess:
```
Question: "Describe the insight that led to this product idea. How did you discover this opportunity?"
```

Then evaluate against criteria:
- **Earned**: From personal experience/observation (not brainstorming)
- **Unique**: Under-appreciated, not obvious
- **Grounded**: Aligns with at least 1 existing capability/strategy

If insight quality is weak, suggest analog research to strengthen it before proceeding.

#### Step 2: Define Problem to Solve

**Display "What Good Looks Like"**: "Good problem definitions are broad, independent from solution, avoiding 'solution thinking'. Frame as problems, not solutions."

Guide user through the **outcome-motivation gap** framework:

1. Ask: "What are customers trying to achieve?" (desired outcome)
2. Ask: "Why do they want this?" (motivation)
3. Ask: "Why can't they do this?" (gap)

**Critical validation**: Ensure the problem is framed as a problem, NOT a solution.
- ❌ Bad: "Helping working professionals spend less time scheduling"
- ✅ Good: "Working professionals spend too much time scheduling meetings"

#### Step 3: Define Target Audience

**Display "What Good Looks Like"**: "Good target audiences start narrow ('now' segment), then identify future expansion paths. The 'now' segment should have the most acute problem, strongest value prop resonance, clearest competitive advantage, easiest reach, and strongest willingness to pay."

Guide user to define 2-3 attributes:

Use AskUserQuestion to determine attribute types:
```
Question: "What types of attributes best describe your target customers?"
Header: "Attributes"
Multi-select: true
Options:
- "Demographics (age, gender, location, education, family size)"
- "Psychographics (beliefs, values, attitudes)"
- "Position (for B2B: company size, industry, title; for B2C: budget, family role)"
```

For each selected type, prompt for specific values.

Then guide segmentation:
1. List all possible segments from combinations of attributes
2. Divide into "now" (primary target) vs. "future" (expansion)
3. **Prioritize "now" segment**: Ask user to consider which segment scores highest on:
   - Most acute problem
   - Strongest value prop resonance
   - Strongest competitive advantage
   - Greatest ease of reach
   - Strongest willingness to pay

#### Step 4: Define Value Proposition

**Display "What Good Looks Like"**: "Good value propositions use customer-centric benefits language, not feature lists. Focus on outcomes and value delivered, not capabilities."

Use the **Ideal Homepage Approach**:

1. **Product tagline**: Guide user to create one-sentence overall value promise
   - Must be benefit-focused, not feature-focused
   - High-level, succinct

2. **3-5 sub-benefits**: Prompt user to list key challenges the product solves
   - Start with up to 10 if needed (will streamline after validation)
   - Ensure each benefit is distinct
   - **Critical**: Benefits ≠ Features
     - Features: "Real-time syncing across devices"
     - Benefits: "Never lose your work, access anywhere"

#### Step 5: Define Competitive Advantage

**Display "What Good Looks Like"**: "Good competitive advantage definitions include both short-term (current landscape, underserved segments) and long-term (one of 7 Powers that compounds over time)."

Guide through both short-term and long-term:

**Long-term (7 Powers)**:
Use AskUserQuestion:
```
Question: "Which long-term competitive advantage (Power) will your product build?"
Header: "Long-term Power"
Options (with descriptions from references/pmf-framework.md):
- "Scale economics"
- "Network economics"
- "Counter-positioning"
- "Switching costs"
- "Branding"
- "Cornered resource"
- "Process power"
```

Then ask: "How will you build this power over time?"

**Short-term**:
1. Guide user to list direct, indirect, and adjacent competitors
2. Identify underserved customer segments (opportunity gaps)

#### Step 6: Define Growth Strategy

**Display "What Good Looks Like"**: "Good growth strategies separate short-term traction channels (first customers) from long-term sustainable channels (scale to 100K+). Long-term channels must be different and more scalable than short-term."

Guide through short-term and long-term separately:

**Short-term traction channels**:
- Goal: First 1K users (B2C) or 10 pilot customers (B2B)
- Examples: Influencer outreach, offline acquisition, cold calls
- Ask: "What channels will reach your target audience for validation?"

**Long-term sustainable channels**:
- Goal: Scale to 100K+ users
- Examples: Viral loops, SEO, user-generated content, paid loops
- **Must be different from short-term channels**
- Ask: "What channels become more efficient/self-sustaining over time?"

For B2B/Marketplace: Consider separate channels for different user roles.

#### Step 7: Define Business Model

**Display "What Good Looks Like"**: "Good business models show deep understanding of business equation levers (not just revenue sources), realistic LTV/CAC ratios, and clear path to profitability."

Guide through the 4 key levers:

1. **Business equation**: Based on product type, display relevant lever template from `references/pmf-framework.md`:

   For **B2B SaaS**: "Typical levers include: New opportunities, Win rate, Average Contract Value (ACV), Net Revenue Retention (NRR), Sales expense ratio. Does this match your model?"

   For **Freemium SaaS**: "Typical levers include: Free signups, MAUs, Free-to-paid conversion rate (typically 2-5%), ASP, Churn rate, CAC, Payback period. Does this match your model?"

   For **Marketplace**: "Typical levers include: GMV, Take rate (typically 10-30%), Buyer liquidity, Seller liquidity, CAC for both sides. Does this match your model?"

   For **DTC E-commerce**: "Typical levers include: Sessions (traffic), Conversion rate, AOV, CLV, Gross margin, CAC. Does this match your model?"

   If user says "customize", prompt for their specific levers. Then help express as formula:
   - Freemium SaaS: Free users × Conversion rate × ARPU
   - Enterprise SaaS: Sales pipeline × Close rate × Contract value
   - Marketplace: Supply × Demand × Take rate
   - DTC: Traffic × Conversion × AOV × Repeat rate

2. **Revenue streams**: Primary and secondary sources

3. **Pricing hypothesis**:
   - Model (per user, per usage, flat fee, freemium, tiered)
   - Price point estimate
   - Willingness to pay rationale

4. **LTV estimate**: Expected revenue per customer over lifetime

5. **Cost structure**: Fixed (hosting, salaries) + Variable (COGS, CAC, support)

6. **Path to profitability**: How LTV > CAC

### Phase 3: Confidence Assessment and Risk Prioritization

After all dimensions are defined:

1. **Assess confidence for each dimension**:
   Use AskUserQuestion for each dimension (or do all 6 in one multi-question if feasible):
   ```
   Question: "On a scale of 1-10, how confident are you in the {Dimension Name} hypothesis?"
   Header: "{Dimension}"
   Options:
   - "1-3: Pure speculation, no evidence"
   - "4-6: Some directional evidence, significant uncertainty"
   - "7-8: Strong evidence, minor gaps"
   - "9-10: Validated, high conviction"
   ```

2. **Identify riskiest dimension(s)**:
   - Lowest confidence scores
   - Largest impact if wrong
   - Most critical to validate early (runway optimization)

3. **Provide recommended next step**:
   - If all dimensions <7: "Run `/pmf-market-research` to validate with analogs/antilogs"
   - If 1-2 dimensions particularly low: "Focus market research on {dimension}"
   - If all dimensions >7: "Consider running `/pmf-interview-prep` to validate with customers"

### Phase 4: Document Generation

1. **Choose template format**:
   Use AskUserQuestion:
   ```
   Question: "Which narrative format would you like?"
   Header: "Format"
   Options:
   - "Structured (fill-in-the-blanks) - Recommended for rapid iteration"
     Description: "Systematic template with clear sections and placeholders. Best for internal hypothesis building and frequent updates."
   - "Prose (narrative storytelling)"
     Description: "Compelling narrative format for stakeholders, investors, and executive reviews. Inspired by strategic narratives like Calendly."
   - "Both (structured + prose)"
     Description: "Generate both formats - structured for working doc, prose for presentations."
   ```

2. **Load appropriate template(s)**:
   - If "Structured" or "Both": Read `assets/pmf-narrative-template.md`
   - If "Prose" or "Both": Read `assets/pmf-narrative-template-prose.md`

3. **Populate with user responses**: Fill in all placeholders with gathered information

3. **Add metadata**:
   - Current Version: V1
   - Last Updated: Today's date
   - Status: "Initial hypothesis created"
   - Product Type: From Phase 1
   - Org Context: From Phase 1

4. **Create validation status table**:
   - Populate confidence scores
   - Mark riskiest dimension(s) with "Yes"
   - Calculate average confidence
   - Add recommended next step

5. **Write file(s)**:
   - Structured format: Save to `{project-root}/pmf-{product-name}/pmf-narrative.md`
   - Prose format: Save to `{project-root}/pmf-{product-name}/pmf-narrative-prose.md`
   - If both: Create both files

6. **Offer narrative writing guide** (optional):
   If user selected prose format, display:
   "For tips on making your narrative more compelling, see `assets/narrative-writing-guide.md` (lessons from successful strategic narratives like Calendly)."

7. **Confirm completion**: Display summary to user:
   ```
   ✅ PMF Narrative V1 created at: {file-path(s)}

   **Summary:**
   - Product: {Product Name}
   - Format: {Structured / Prose / Both}
   - Overall confidence: {Average}/10
   - Riskiest dimension: {Dimension}

   **Files created:**
   {List file paths for structured and/or prose versions}

   **Next step:** Run `/pmf-market-research` to validate your hypothesis with market analogs and antilogs.
   ```

## Quality Gates

Before completing the skill, verify:

1. **All 6 dimensions are defined** with sufficient detail (not placeholder text)
2. **Problem is framed as a problem**, not a solution
3. **Target audience has 2-3 specific attributes** (not "everyone" or overly broad)
4. **Value prop distinguishes benefits from features** (outcome language, not capability language)
5. **Competitive advantage includes both short-term and long-term**
6. **Growth strategy separates short-term and long-term channels**
7. **Business model addresses all 4 levers** (revenue, pricing, LTV, costs)
8. **Confidence scores are assigned** for all dimensions
9. **At least one dimension is marked as riskiest**

If any quality gate fails, prompt user for clarification or improvement before generating the document.

## Tips for Effective Narrative Building

1. **Ask open-ended questions**: Avoid yes/no questions; prompt detailed explanations
2. **Provide examples**: Reference the framework document and real-world examples
3. **Challenge assumptions**: If something seems too broad or vague, ask for specificity
4. **Connect dimensions**: Help user see how dimensions reinforce each other
5. **Encourage prose over bullets**: Narrative structure reveals logical inconsistencies
6. **Set realistic confidence scores**: V1 hypotheses should typically be 4-7/10 (room for validation)

## Common Pitfalls to Avoid

1. **Solution-framed problems**: "Help users do X" → "Users struggle to do X"
2. **Overly broad audiences**: "Small businesses" → "Solopreneurs with $50K-$200K revenue in service industries"
3. **Feature-focused value props**: "AI-powered matching" → "Find qualified candidates 10x faster"
4. **Ignoring short-term growth**: Assuming long-term channels will work from day 1
5. **Skipping the 'why'**: Every dimension should answer "why this approach vs. alternatives?"
6. **Overconfidence in V1**: Don't assign 9-10 confidence without validation evidence

## Reference Files

- **Detailed framework**: `references/pmf-framework.md` (load into context as needed for examples, criteria, business equation details, and multi-role guidance)
- **Structured template**: `assets/pmf-narrative-template.md` (systematic fill-in-the-blanks format)
- **Prose template**: `assets/pmf-narrative-template-prose.md` (narrative storytelling format)
- **Narrative writing guide**: `assets/narrative-writing-guide.md` (optional resource for crafting compelling narratives)

## Post-Skill Actions

After completing this skill, the user should:
1. Review the generated `pmf-narrative.md` file
2. Run `/pmf-status` to see current validation state
3. Run `/pmf-market-research` to begin broad validation

## Example Session Flow

```
User: "I want to validate PMF for my new productivity tool idea"
Claude: <Uses AskUserQuestion to gather project location and context>
Claude: "Let's start by pressure-testing your initial insight. How did you discover this opportunity?"
User: "I've worked remotely for 5 years and kept noticing how much time I waste context-switching between tools"
Claude: <Validates insight is earned> "That's a lived experience. Let's define the problem using the outcome-motivation gap..."
<Guides through 7 steps of dimension definition>
Claude: <After gathering all info> "Now let's assess confidence in each dimension..."
Claude: <Generates pmf-narrative.md> "✅ PMF Narrative V1 created. Growth Strategy (4/10) is your riskiest dimension. Next: Run `/pmf-market-research`"
```

This example shows the interactive, guided nature of the skill - not a form to fill out, but a conversation that shapes strategic thinking.

# Report Template

Use this structure for all Fathom assessment outputs. The report must be suitable for enterprise review: clear executive summary for decision-makers, detailed reasoning for domain experts.

---

```markdown
# Fathom: Maritime Data Capability Assessment

**Vessel/Fleet:** [Name or identifier]
**Assessment Date:** [Date]
**Data Period:** [Start] to [End]
**Prepared by:** Fathom (AI-assisted assessment)

---

## Executive Summary

[2-4 paragraphs for decision-makers. No jargon. Focus on:]
- What the data can credibly answer
- Key limitations and their business impact
- Top recommendations with expected value

**Bottom line:** [One sentence summary of data readiness for performance optimization]

---

## 1. Data Inventory

### 1.1 Signal Overview

| Signal | Physical Quantity | Resolution | Coverage | Completeness | Quality Notes |
|--------|------------------|------------|----------|--------------|---------------|
| [id] | [mass/energy/velocity/...] | [1min/1s/daily] | [date range] | [%] | [calibration, known issues] |

### 1.2 System Coverage

| Ship System | Coverage Level | Key Signals Available | Notable Gaps |
|-------------|----------------|----------------------|--------------|
| Propulsion | [Good/Partial/Minimal] | [list] | [list] |
| Hull | [Good/Partial/Minimal] | [list] | [list] |
| Navigation | [Good/Partial/Minimal] | [list] | [list] |
| Environmental | [Good/Partial/Minimal] | [list] | [list] |
| Engine Auxiliaries | [Good/Partial/Minimal] | [list] | [list] |

### 1.3 Data Quality Assessment

[Brief narrative on overall data quality. Systematic gaps? Calibration concerns? Integration issues?]

---

## 2. Capability Assessment

### 2.1 High-Confidence Questions

These questions can be answered reliably with the available data.

#### [Question 1 title]

**Question:** [Precise statement]

**Answer confidence:** High

**What the data supports:**
[Specific analysis possible, expected accuracy, conditions under which valid]

**Key assumptions:**
[List assumptions required]

**Limitations:**
[What this analysis cannot tell you]

---

#### [Question 2 title]

[Repeat structure]

---

### 2.2 Partial-Confidence Questions

These questions can be partially addressed. Results require caveats.

#### [Question title]

**Question:** [Precise statement]

**Answer confidence:** Partial

**What the data supports:**
[What can be determined with available data]

**Key confounders:**
[Uncontrolled variables that limit confidence]

**Validity conditions:**
[Under what conditions is the analysis reliable]

**Recommended approach:**
[How to extract maximum value given limitations]

---

### 2.3 Questions Not Currently Answerable

These questions cannot be reliably addressed with available data.

#### [Question title]

**Question:** [Precise statement]

**Answer confidence:** Low / Not answerable

**Why not answerable:**
[Specific missing data or confounders]

**What would be needed:**
[Data additions that would enable this analysis]

---

## 3. Detailed Reasoning

This section provides the physics-based working for expert review.

### 3.1 Governing Physics Applied

[Explain which physical relationships are relevant to this dataset and how they were applied]

### 3.2 Signal-to-Variable Mapping

| Physical Variable | Source Signal(s) | Derivation | Uncertainty |
|-------------------|------------------|------------|-------------|
| Speed through water | [signal] or derived | [method] | [±X%] |
| Displacement | [signal] or assumed | [method] | [±X%] |
| ... | | | |

### 3.3 Confounding Analysis

For key assessments, document unobserved variables and their impact:

**[Assessment name]**

| Unobserved Variable | Plausible Range | Sensitivity | Induced Uncertainty |
|---------------------|-----------------|-------------|---------------------|
| [variable] | [range] | [∂output/∂variable] | [±X%] |

### 3.4 Reasoning Chains

[For each major finding, show the logical chain:]

**Finding:** [Statement]

**Reasoning:**
1. [Physical principle invoked]
2. [Equation or relationship applied]
3. [Variables identified: observed vs. assumed]
4. [Sensitivity to assumptions evaluated]
5. [Confidence level justified]

---

## 4. Recommendations

### 4.1 Data Extensions

Prioritized additions to expand analytical capabilities.

| Priority | Data Addition | Implementation | Questions Unlocked | Confidence Improvement |
|----------|---------------|----------------|-------------------|----------------------|
| 1 | [Specific sensor/data] | [Complexity: Low/Medium/High] | [List] | [Partial → High, etc.] |
| 2 | ... | | | |

### 4.2 Recommended Next Steps

[Actionable recommendations in priority order:]

1. **[Action]** — [Rationale and expected outcome]
2. **[Action]** — [Rationale and expected outcome]

### 4.3 Questions for Stakeholder Input

[Any clarifications needed to refine the assessment:]

- [Question about operational context]
- [Question about data systems]

---

## Appendix A: Methodology

This assessment uses first-principles physics reasoning rather than pattern matching or lookup tables.

**Approach:**
1. Map signals to fundamental physical quantities
2. Identify which governing equations (energy, momentum, mass conservation) can be evaluated
3. Determine observable vs. assumed variables
4. Assess confidence based on sensitivity to unobserved variations
5. Prioritize data extensions by value delivered

**Limitations:**
- Assessment based on metadata description; actual data quality may differ
- Calibration assumptions may not reflect current sensor state
- External data availability and quality not verified

---

## Appendix B: Glossary

[Define technical terms used in the report for non-specialist readers]

| Term | Definition |
|------|------------|
| SOG | Speed over ground — ship's speed relative to seabed, from GPS |
| STW | Speed through water — ship's speed relative to water, from hull-mounted log |
| SFOC | Specific fuel oil consumption — fuel used per unit power output (g/kWh) |
| MCR | Maximum continuous rating — engine's rated power output |
| ... | ... |

---

*Assessment generated using Fathom's physics-based reasoning methodology. All findings should be validated against operational knowledge before implementation.*
```

---

## Template Usage Notes

**Executive Summary:**
- Write last, after completing detailed analysis
- Must stand alone for readers who won't read full report
- Quantify where possible ("±15% uncertainty" not "some uncertainty")

**Confidence levels:**
- High: quantifiable uncertainty, robust across conditions
- Partial: valid with stated caveats, valid for subset of conditions
- Low/Not answerable: confounders dominate, pattern may be spurious

**Detailed reasoning section:**
- This is where domain experts verify the work
- Show equations, assumptions, sensitivity calculations
- An expert should be able to reproduce and challenge the reasoning

**Recommendations:**
- Specific and actionable
- Connect to capabilities unlocked
- Include implementation complexity
- Prioritize by value/effort ratio

---
name: fathom
description: Fathom your maritime data — assess what operational questions a dataset can answer using first-principles physics reasoning. Use when a user provides vessel data metadata and wants to understand what analyses are feasible, what confidence levels apply, and what data gaps limit insight. Triggers on phrases like "what can this data answer", "assess my vessel data", "fathom", "data capability assessment", or when metadata about maritime signals is provided.
---

# Fathom: Maritime Data Capability Assessment

Assess what operational questions a maritime dataset can credibly answer by reasoning from first-principles physics.

## Core Methodology

This skill does not use lookup tables or taxonomies. Instead, reason from fundamentals:

1. **Any signal measures a fundamental quantity** — mass, energy, force, velocity, position, pressure, temperature
2. **Ship performance is governed by conservation laws** — mass, energy, momentum
3. **Reasoning connects signals to questions** — through the physics, not through enumeration

For any dataset, the approach is:
1. Map each signal to fundamentals (what physical quantity?)
2. Identify which conservation laws / governing equations can be evaluated
3. Determine what's observable vs. what must be assumed
4. Assess confidence based on unobserved variations
5. Identify what extensions would reduce uncertainty

See `references/reasoning_methodology.md` for the complete step-by-step approach.
See `references/fundamentals.md` for governing physics.
See `references/ship_systems.md` for system context.

## Output Requirements

Generate a structured report suitable for enterprise review. Use the template in `references/report_template.md`.

The report must include:
- **Executive Summary** — Key findings in business language
- **Detailed Reasoning** — Full physics-based working, reviewable by domain experts
- **Actionable Recommendations** — Prioritized by value, with rationale

Every assessment must show its working. Conclusions without visible reasoning are not acceptable.

## Handling Unfamiliar Signals

When encountering signals not explicitly covered in references:

1. Identify the fundamental physical quantity measured
2. Locate the ship system it belongs to
3. Trace causal connections to performance via governing physics
4. Reason about what it enables and what it needs

This approach works for any signal — derive understanding, don't look it up.

## Confidence Calibration

Use `references/calibration_anchors.md` for order-of-magnitude sanity checks. These are not rules — they're reference points for validating that reasoning produces sensible results.

## Quality Standards

- State assumptions explicitly
- Quantify uncertainty where possible (even rough orders of magnitude)
- Distinguish between "not measurable" and "measurable but confounded"
- Be honest about what the data cannot answer
- Recommendations must connect to specific unlocked capabilities

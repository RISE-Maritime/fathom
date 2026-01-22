# Reasoning Methodology

The systematic approach for assessing what any maritime dataset can answer.

## Phase 1: Signal Analysis

For each signal in the dataset, establish its meaning and value.

### Step 1.1: Identify Fundamental Quantity

What physical quantity does this signal measure?

- Mass, energy/power, force, velocity, position/geometry, pressure, temperature?
- Is it a direct measurement or derived/calculated?
- What are the units and what do they imply?

### Step 1.2: Locate in Ship System

Where does this measurement come from?

- Propulsion, hull, navigation, engine auxiliaries, electrical, cargo?
- What component or subsystem specifically?
- What is the physical sensing mechanism?

### Step 1.3: Assess Measurement Quality

How trustworthy is this signal?

- Sample rate: Appropriate for phenomena of interest?
- Completeness: Systematic gaps or random?
- Accuracy: What's the expected sensor uncertainty?
- Calibration: Any drift concerns?
- Failure modes: How does this sensor fail?

### Step 1.4: Trace Causal Connections

How does this signal connect to ship performance?

- What governing equations does it appear in?
- What can be calculated if combined with other signals?
- What questions does it help answer?
- What other signals would it need?

## Phase 2: Dataset Integration

After analyzing individual signals, assess the dataset as a whole.

### Step 2.1: Map Coverage of Governing Equations

For each key governing relationship, what's observable?

**Energy balance (fuel to motion):**
- [ ] Fuel energy input (fuel flow × LCV)
- [ ] Engine losses (exhaust temp, cooling flows)
- [ ] Shaft power output (torque × RPM)
- [ ] Propulsive losses (thrust vs shaft power)
- [ ] Resistance dissipation (total resistance × speed)

**Force balance (thrust = resistance):**
- [ ] Thrust (from propeller model + measurements)
- [ ] Calm water resistance (speed, displacement, trim, hull condition)
- [ ] Added resistance (wind, waves, current, shallow water)

**Mass balance:**
- [ ] Displacement tracking (drafts or component masses)
- [ ] Fuel inventory (consumption + remaining)

### Step 2.2: Identify Observable vs. Assumed Variables

For every variable in the relevant governing equations:

| Variable | Status | Source | Uncertainty |
|----------|--------|--------|-------------|
| Speed | Observable | SOG from GPS | ±0.1 knot |
| Displacement | Derived | Daily draft readings | ±2-3% |
| Weather | Not observed | Must assume or filter | Unknown |

### Step 2.3: Characterize Confounding

For variables that are not directly observed:

- What is the likely range of variation in the dataset?
- How sensitive is the analysis to this variation?
- Can operating conditions be filtered to reduce variation?
- What's the magnitude of potential error if ignored?

## Phase 3: Question Assessment

For each question of interest, evaluate answerability.

### Step 3.1: State the Physical Phenomenon

What physical process or relationship does this question probe?

Write it precisely:
- "How does fuel consumption vary with speed?" → Speed-power relationship
- "Is the hull fouling?" → Change in frictional resistance over time
- "What's the optimal trim?" → Trim-resistance relationship

### Step 3.2: Write the Governing Relationship

What equation or causal chain governs this phenomenon?

Express it formally:
```
P = R(V, Δ, trim, weather, fouling) × V / η(J, condition)
```

Identify every variable in the relationship.

### Step 3.3: Map Variables to Observables

For each variable in the governing relationship:

**Directly observed:** Which signal provides this?
**Derivable:** From which signals, with what assumptions?
**Assumed/Uncontrolled:** Must be held constant or ignored

### Step 3.4: Evaluate Sensitivity to Unobserved Variables

For each uncontrolled variable:

- What's the plausible range in this dataset?
- What's the partial derivative (sensitivity)?
- What error does this induce in the answer?

Example:
```
Question: Speed-fuel relationship
Unobserved: Current (assumed zero)
Plausible range: ±1 knot
Sensitivity: P ∝ V³, so at 12 knots, ±1 knot = ±25% power error
Conclusion: Current uncertainty dominates. Answer unreliable without STW or current correction.
```

### Step 3.5: Determine Validity Conditions

Under what conditions is the analysis valid?

- Filter criteria (calm weather only, laden voyages only, etc.)
- Assumption conditions (constant displacement, steady state, etc.)
- Time periods (before/after drydock, seasonal)

### Step 3.6: Assign Confidence Level

**High confidence:**
- All governing variables observed or bounded within ±X%
- Sensitivity analysis shows acceptable error
- Result valid across broad operating conditions

**Partial confidence:**
- Key variables uncontrolled but can be filtered/bounded
- Result valid for subset of conditions
- Trends observable but causation not isolatable

**Low confidence:**
- Unobserved variations likely dominate signal
- Cannot distinguish effect of interest from confounders
- Pattern may be spurious

### Step 3.7: Identify Highest-Value Data Extension

What single addition would most improve this assessment?

- Which unobserved variable has the largest sensitivity?
- Is there a practical way to measure or estimate it?
- What confidence improvement would result?

## Phase 4: Synthesis

Bring together all question assessments into coherent findings.

### Step 4.1: Group by Confidence

- What can be answered with high confidence?
- What is partially answerable with caveats?
- What cannot currently be answered?

### Step 4.2: Identify Cross-Cutting Gaps

Which missing data affects multiple questions?

Prioritize data extensions that unlock several capabilities.

### Step 4.3: Formulate Actionable Recommendations

For each recommendation:
- What specific data would be added?
- What questions would it unlock or improve?
- What's the approximate implementation complexity?
- What confidence improvement is expected?

## Reasoning Integrity Checks

After completing the assessment, verify:

- [ ] Every conclusion traces to specific governing physics
- [ ] Assumptions are stated explicitly, not implicit
- [ ] Sensitivity to unobserved variables has been estimated
- [ ] Confidence levels are justified, not asserted
- [ ] Recommendations connect to specific capability improvements
- [ ] An expert could reproduce this reasoning

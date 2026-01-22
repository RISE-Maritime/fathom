# Worked Examples

Complete reasoning demonstrations showing the methodology in practice.

---

## Example 1: Tanker with Minimal Instrumentation

### Dataset Metadata

```yaml
vessel:
  type: tanker
  dwt: 115000

signals:
  - id: gps_sog
    description: Speed over ground
    sample_rate: 1min
    coverage: 2022-01-01 to 2024-06-30
    completeness: 96%

  - id: me_fo_consumption
    description: Main engine fuel oil flow
    unit: kg/h
    sample_rate: 1min
    completeness: 92%
    notes: Coriolis flowmeter

  - id: me_rpm
    description: Main engine RPM
    sample_rate: 1min
    completeness: 94%
```

### Phase 1: Signal Analysis

**gps_sog**
- Fundamental quantity: Velocity (speed over ground)
- System: Navigation
- Quality: High completeness, GPS accuracy ~±0.1 knot
- Causal connection: Key variable in power-speed relationship, but measures ground speed, not water speed. Current effects embedded.

**me_fo_consumption**
- Fundamental quantity: Mass flow rate → proxy for power input
- System: Propulsion / engine fuel system
- Quality: Coriolis meter is accurate (±0.5%). High completeness.
- Causal connection: Input to energy balance. With SFOC assumption, estimates brake power.

**me_rpm**
- Fundamental quantity: Rotational velocity
- System: Propulsion / engine
- Quality: Good
- Causal connection: Operating point indicator. With propeller curve, relates to thrust loading.

### Phase 2: Dataset Integration

**Energy balance coverage:**
- [x] Fuel input: me_fo_consumption
- [ ] Engine losses: not measured
- [ ] Shaft power: not measured (no torque)
- [ ] Thrust: not measured
- [x] Speed: gps_sog (but SOG not STW)

**Force balance coverage:**
- [ ] Thrust: not directly measurable
- [ ] Calm water resistance variables:
  - [x] Speed (SOG only)
  - [ ] Displacement: not measured
  - [ ] Trim: not measured
  - [ ] Hull condition: not measured
- [ ] Added resistance:
  - [ ] Wind: not measured
  - [ ] Waves: not measured
  - [ ] Current: not measured

**Unobserved variables:**
| Variable | Plausible Range | Sensitivity | Impact |
|----------|----------------|-------------|---------|
| Displacement | 60-115k tonnes (ballast to laden) | P ∝ Δ^(2/3) | ±30-40% power |
| Current | ±1.5 knots | P ∝ V³ | ±40-50% power |
| Weather | calm to Beaufort 6 | variable | ±5-30% power |
| Fouling | 0-25% over dataset period | direct | ±0-25% power |

### Phase 3: Question Assessment

**Question: What is the optimal speed for fuel efficiency?**

Phenomenon: Speed-power-fuel relationship
Governing equation: FC = P(V, Δ, weather, fouling) / η_engine(load)

Assessment:
- Speed: observed (SOG), not STW
- Displacement: NOT observed — ballast vs laden is 2:1 ratio for tanker
- Weather: NOT observed
- Fouling: NOT observed

This question is **not answerable with confidence**. The unobserved variables (displacement, current, weather) each induce errors larger than typical optimization gains (5-10%). Any apparent "optimal speed" is an artifact of the operating condition mix in the data.

**Question: Can we detect hull fouling?**

Phenomenon: Resistance increase over time at constant conditions
Governing equation: R_fouling appears in R_total, manifesting as increased fuel at same speed/loading

Assessment:
- Need to compare fuel-at-speed across time
- But: displacement uncontrolled (ballast vs laden)
- And: weather uncontrolled
- And: SOG ≠ STW (current variation)

This question is **answerable at low confidence only**. 
- Can detect *step changes* (pre/post drydock) if we filter to same voyage type (e.g., laden Ras Tanura → Singapore)
- Cannot track gradual fouling — confounders dominate
- Large fouling events (>20% impact) might be visible as statistical outliers

**Question: Is engine efficiency degrading?**

Phenomenon: SFOC change over time
Governing equation: SFOC = FC / P_brake

Assessment:
- FC: observed
- P_brake: NOT directly observed. Would need shaft power or reliable load signal.
- me_rpm alone doesn't give power without propeller curve and ship speed through water

This question is **not answerable**. Without shaft power or torque measurement, cannot separate engine efficiency from propulsive efficiency changes.

### Phase 4: Synthesis

**High confidence:** None

**Partial confidence:**
- Gross operational patterns (voyage frequency, speed distributions, utilization)
- Pre/post drydock step change in fuel consumption (filter to similar routes)

**Not answerable:**
- Speed optimization (displacement/weather confounding)
- Continuous fouling tracking (displacement/weather confounding)
- Engine efficiency trending (no power measurement)
- Weather impact quantification (no weather data)

**Recommended data extensions (prioritized):**

1. **Draft sensors (fwd/aft)** — Enables displacement normalization. Highest value single addition. Reduces largest confounder for this vessel type.

2. **Weather data integration** (hindcast service or onboard anemometer) — Enables weather filtering/normalization. Relatively low cost if using external service.

3. **Shaft power meter** — Enables true engine vs propulsive efficiency separation. Higher cost but unlocks engine condition monitoring.

---

## Example 2: Container Ship with Rich Instrumentation

### Dataset Metadata

```yaml
vessel:
  type: container
  teu: 8500

signals:
  - id: sog
    sample_rate: 10s
    completeness: 98%

  - id: stw_long
    description: Speed through water (longitudinal)
    sample_rate: 10s
    completeness: 91%
    notes: Doppler log, last calibrated 8 months ago

  - id: me_power
    description: Main engine shaft power
    unit: kW
    sample_rate: 1min
    completeness: 94%
    notes: Shaft power meter (torque × RPM)

  - id: me_fo_flow
    sample_rate: 1min
    completeness: 93%

  - id: draft_fwd
    sample_rate: manual, ~2 per day
    completeness: 85%

  - id: draft_aft
    sample_rate: manual, ~2 per day
    completeness: 85%

  - id: wind_speed_apparent
    sample_rate: 1min
    completeness: 88%

  - id: wind_dir_apparent
    sample_rate: 1min
    completeness: 88%

  - id: heading
    sample_rate: 1min
    completeness: 97%
```

### Phase 2: Dataset Integration (abbreviated)

**Energy balance:**
- [x] Fuel input: me_fo_flow
- [x] Shaft power: me_power — rare and valuable
- [x] Speed: SOG and STW both available

**Force balance:**
- [x] Power at propeller: me_power with efficiency assumption
- [x] Speed through water: stw_long (with calibration caveat)
- [x] Displacement: derivable from drafts (daily resolution)
- [x] Wind: derivable true wind from apparent + SOG + heading
- [ ] Waves: not measured
- [ ] Current: derivable as SOG - STW (valuable!)

This is a well-instrumented dataset. Key unobserved variable is waves.

### Phase 3: Question Assessment

**Question: Speed-power optimization**

Assessment:
- Speed through water: observed (STW)
- Power: directly measured (shaft power meter)
- Displacement: derivable from drafts (daily, interpolate)
- Wind: derivable (enables normalization or filtering)
- Current: derivable as SOG - STW
- Waves: NOT observed — correlated with wind but not deterministic

**Confidence: High for calm weather conditions, Partial overall**

Method:
1. Calculate true wind from apparent wind, heading, SOG
2. Filter to low wind conditions (< 15 knots) as proxy for calm seas
3. Bin by displacement (from draft interpolation)
4. Develop P = f(V_STW) curves per displacement bin
5. These represent hull+propeller characteristic with minimal weather contamination

Remaining uncertainty: STW calibration drift (log fouling), wave presence in "calm" filter, trim effect within displacement bins.

**Question: Hull fouling monitoring**

Assessment:
With shaft power and STW available, can compute propulsive resistance proxy:
```
R_proxy = P_shaft × η_prop / V_STW
```

Track R_proxy over time at normalized conditions:
- Constant V_STW (bin by speed)
- Constant displacement (bin by draft)
- Calm weather (filter by wind threshold)

**Confidence: High**

Can detect gradual fouling as increasing R_proxy over time. Drydock events should show step recovery.

Caveat: Speed log calibration drift will appear as apparent fouling. If STW drifts low, R_proxy increases artificially. Recommend cross-check against current (SOG - STW) for anomalies.

**Question: Engine efficiency monitoring**

Assessment:
```
SFOC = me_fo_flow / me_power
```

Both directly measured. Can track SFOC vs load (power/MCR).

**Confidence: High**

SFOC trending is robust. Compare to baseline at reference load points. Degradation appears as upward SFOC drift.

Remaining uncertainty: Fuel LCV variation (±2-3%) between bunker batches. If bunker records available, can normalize.

### Phase 4: Recommendations

This dataset is already well-equipped. Priority additions:

1. **Wave data** (hindcast service or onboard sensor) — Main remaining gap. Would upgrade speed-power relationship from calm-weather-only to all-weather normalized.

2. **STW calibration tracking** — Implement periodic validation against docking logs or current-free passages (e.g., compare SOG and STW in river/canal transits).

3. **Bunker fuel analysis** — LCV per batch would enable absolute SFOC comparison rather than relative trending.

---

## Example 3: Unfamiliar Signals

### Dataset includes unknown signal

```yaml
- id: tc_inlet_filter_dp
  description: Turbocharger inlet filter differential pressure
  unit: mbar
  sample_rate: 1min
  completeness: 89%
```

### Reasoning from Fundamentals

**Step 1: Fundamental quantity**
Differential pressure — pressure drop across a component.

**Step 2: Locate in ship system**
"tc" = turbocharger, "inlet filter" = air intake system.
This measures pressure drop across the turbocharger air inlet filter.

**Step 3: Governing physics**
```
ΔP_filter = f(air flow rate, filter resistance)
Filter resistance increases with fouling/blockage
Air flow rate depends on engine load
```

At constant engine load, increasing ΔP indicates filter fouling.

**Step 4: Causal connection to performance**
```
High filter ΔP → Restricted airflow → Lower scavenge pressure → 
  → Reduced air/fuel ratio → Incomplete combustion or power derating
  → Increased SFOC, potentially increased emissions
```

**Step 5: Assessment**
This signal enables:
- Filter condition monitoring (track ΔP at reference loads)
- Predictive maintenance (schedule filter cleaning/replacement)
- Context for engine efficiency deviations

Needs:
- Engine load signal to normalize ΔP
- Baseline values from clean filter state

**Conclusion:** Valuable for engine health monitoring. Combined with other engine signals (SFOC, exhaust temps), helps diagnose efficiency deviations. Does not directly inform hull performance questions.

---

## Common Reasoning Errors to Avoid

**Error: Conflating correlation with causation**
> "Fuel consumption correlates with wind speed, therefore wind causes X% of consumption."

Correct reasoning: Correlation observed. But wind correlates with waves, and both correlate with voyage patterns (seasonal). Without controlled analysis, cannot attribute causation.

**Error: Ignoring confounders because they're inconvenient**
> "We'll just assume displacement is constant."

Correct reasoning: For container ship, displacement varies 30%+. Assuming constant induces ~20% power analysis error. State the assumption explicitly and bound its impact.

**Error: Precision without accuracy**
> "The optimal speed is 12.34 knots."

Correct reasoning: Given unobserved weather and current, optimal speed is approximately 12-13 knots under calm conditions. False precision obscures uncertainty.

**Error: Treating derived quantities as observations**
> "We measure current as SOG - STW."

Correct reasoning: Current is *derived* from two observations with their own errors. STW has calibration uncertainty. Derived current inherits both errors and may have systematic bias.

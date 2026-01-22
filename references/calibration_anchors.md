# Calibration Anchors

Order-of-magnitude values for sanity-checking reasoning. These are not rules — they're reference points from typical merchant vessel operations.

## Speed and Power

**Speed-power sensitivity:**
```
At constant displacement and conditions:
P ∝ V^n where n ≈ 3-4 for typical merchant ships

Rule of thumb: 10% speed increase → 30-40% power increase
```

**Typical service speeds:**
| Vessel Type | Service Speed | Slow Steaming |
|-------------|---------------|---------------|
| Container | 18-22 knots | 14-16 knots |
| Tanker | 13-15 knots | 10-12 knots |
| Bulk carrier | 13-15 knots | 10-12 knots |
| RoRo | 16-20 knots | 14-16 knots |

**Power levels:**
| Vessel Size | Installed MCR | Typical Operating |
|-------------|---------------|-------------------|
| Handysize (~35k dwt) | 6-8 MW | 4-6 MW |
| Panamax (~75k dwt) | 10-14 MW | 7-10 MW |
| Capesize (~180k dwt) | 15-20 MW | 10-14 MW |
| VLCC (~300k dwt) | 25-35 MW | 15-25 MW |
| Large container (15k TEU) | 50-70 MW | 35-50 MW |

## Fuel Consumption

**SFOC reference values:**
```
Modern slow-speed diesel (MAN B&W, WinGD): 160-180 g/kWh at optimal load
Optimal load: typically 70-85% MCR
Low load penalty: +10-15% SFOC at 50% MCR, +20-30% at 25% MCR
```

**Daily consumption (main engine only):**
| Operating Mode | Typical Range |
|----------------|---------------|
| Full speed | 30-200 t/day depending on size |
| Eco speed | 20-60% of full speed consumption |
| Slow steaming | 30-50% of full speed consumption |
| Port/idle | 2-10 t/day (auxiliaries + hotel) |

## Displacement and Loading

**Displacement-power relationship:**
```
P ∝ Δ^(2/3) approximately

10% displacement increase → ~6-7% power increase at same speed
```

**Typical displacement variation:**
| Vessel Type | Laden/Ballast Ratio |
|-------------|---------------------|
| Tanker | 2.0-2.2 |
| Bulk carrier | 1.8-2.0 |
| Container | 1.3-1.5 |
| RoRo | 1.1-1.3 |

## Resistance Components

**Calm water resistance breakdown (typical, design speed):**
```
Frictional: 60-80% (higher at low Froude numbers)
Residuary (wave + form): 15-30%
Air: 2-5% (higher for container ships)
Appendages: 2-5%
```

**Added resistance magnitudes:**

| Condition | Added Resistance |
|-----------|------------------|
| Moderate wind (15-20 kn beam) | +5-15% |
| Strong wind (25-30 kn head) | +20-40% |
| Moderate waves (Hs 2-3m head) | +10-25% |
| Heavy weather (Hs 4-5m head) | +30-60% |
| Moderate fouling (12 months) | +5-15% |
| Heavy fouling (24 months, poor coating) | +20-40% |

**Current effect:**
```
1 knot current at 12 knot ship speed = 8% STW error
Power ∝ V³, so: 1 knot current → ~25-30% power attribution error

This is often the largest single confounder in performance analysis.
```

## Trim

**Trim effect on resistance:**
```
Typical range: ±2-5% across operational trim envelope
Optimal trim: often 0.5-1.5m by stern for laden, varies in ballast
Sensitivity highest at low/high speed extremes
```

## Hull Fouling

**Fouling progression (resistance penalty):**
```
Clean hull: baseline
6 months (good coating, temperate): +3-5%
12 months (good coating, temperate): +5-10%
12 months (poor coating, tropical): +15-25%
24 months (poor coating, tropical): +25-40%

Post-drydock: returns to ~baseline (depends on prep quality)
```

**Speed loss at constant power:**
```
10% resistance increase → ~3% speed loss
20% resistance increase → ~6% speed loss
```

## Engine Performance

**Cylinder-to-cylinder variation:**
```
Exhaust temp spread: ±15-20°C normal, >30°C indicates problem
Peak pressure spread: ±2-3 bar normal
```

**Turbocharger health:**
```
RPM at given load: ±2-3% normal variation
Degrading trend: 1-2% per year typical
Step change >5%: investigate (fouling, damage)
```

**Scavenge air system:**
```
Air cooler ΔT effectiveness: typically 85-95%
Fouled cooler: ΔT drops 10-20%, scav air temp rises
Effect: 1°C scav air temp rise → ~0.3-0.5% power loss
```

## Data Quality

**Typical sensor uncertainties:**
| Measurement | Typical Uncertainty |
|-------------|---------------------|
| GPS speed | ±0.1 knot |
| Speed log (STW) | ±1-3% (plus calibration drift) |
| Fuel flow (Coriolis) | ±0.5% |
| Fuel flow (volumetric) | ±1-2% (plus density uncertainty) |
| Shaft power | ±1-2% |
| Draft (sensor) | ±2-5 cm |
| Draft (visual) | ±5-10 cm |
| Wind (anemometer) | ±5-10% speed, ±5° direction |

**Completeness thresholds:**
```
>95%: Good for most analyses
85-95%: Usable, check for systematic gaps
<85%: Assess gap patterns carefully — bias likely
```

## Voyage Phases

**Steady-state filtering:**
```
Exclude: first/last 10-30 minutes of voyage (acceleration/deceleration)
Exclude: rate of turn > 0.5°/min (maneuvering)
Exclude: speed < 5-6 knots (not in sea passage mode)
Exclude: rapid power changes (>10% in 5 minutes)
```

**Averaging periods:**
```
Short-term (engine response): 1-10 minutes
Voyage segment: 4-24 hours
Performance trending: 30-90 days
Seasonal patterns: 6-12 months
```

## Sanity Checks

Use these to verify reasoning produces sensible results:

- If calculated resistance is negative: something is wrong
- If SFOC < 150 or > 250 g/kWh: check calculations or sensor data
- If trim effect > 10%: likely other confounders present
- If fouling rate > 5%/month: check for displacement changes
- If weather accounts for > 50% of fuel variation: likely overfit or missing variable

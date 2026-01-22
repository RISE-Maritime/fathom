# Fundamentals

The physics that governs ship performance. All assessment reasoning traces back to these principles.

## Fundamental Physical Quantities

Every maritime signal ultimately measures one of these:

| Quantity | Examples | Units |
|----------|----------|-------|
| Mass | Cargo, fuel, displacement, ballast | kg, tonnes |
| Energy / Power | Fuel energy, shaft power, heat | kW, kJ, kWh |
| Force | Thrust, resistance, wind load | kN, N |
| Velocity | Ship speed, flow rates, RPM | m/s, knots, kg/s, rev/min |
| Position / Geometry | Location, draft, trim, angles | m, degrees |
| Pressure | Cylinder, manifold, hydraulic, atmospheric | bar, kPa |
| Temperature | Exhaust, cooling, cargo, ambient | °C, K |

When encountering any signal, first identify which fundamental quantity it measures.

## Conservation Laws

### Conservation of Energy

Energy in = Energy out + Stored energy change

**Fuel-to-motion energy chain:**
```
Fuel chemical energy (ṁ_fuel × LCV)
  → Engine thermal cycle
    → Brake power (P_brake) + Exhaust heat + Cooling losses + Friction
      → Shaft power (P_shaft) after gearbox losses
        → Thrust power (P_thrust = T × V_advance) + Propeller losses
          → Ship kinetic energy change + Resistance dissipation
```

At steady state: Thrust power = Resistance × Ship speed

**Key implication:** To assess efficiency at any stage, you need measurements bounding that stage. Fuel flow alone tells you input; without shaft power, you cannot separate engine efficiency from propulsive efficiency.

### Conservation of Momentum (Force Balance)

At steady speed: Thrust = Total Resistance

```
Thrust = f(propeller geometry, RPM, advance ratio, water properties)

Total Resistance = R_frictional + R_residuary + R_air + R_added
  
where:
  R_frictional ∝ wetted_surface × V² × f(Reynolds number, roughness)
  R_residuary = f(hull form, Froude number) — wave-making, form drag
  R_air ∝ frontal_area × V_relative_wind² × C_wind(angle)
  R_added = R_waves + R_current_effective + R_shallow_water + R_fouling
```

**Key implication:** To isolate any resistance component, all others must be measured or controlled.

### Conservation of Mass

Mass in = Mass out + Accumulation

**Fuel system:**
```
Bunker intake = Consumption + Remaining + Losses
ṁ_consumed = Σ(engine consumption) + boiler + auxiliary
```

**Displacement:**
```
Δ = Lightship + Cargo + Fuel + Fresh water + Ballast + Stores
```

Draft/trim measurements + hydrostatic tables → Displacement

**Key implication:** Displacement changes continuously. Without tracking, it confounds all resistance-based assessments.

## Governing Relationships

### Speed-Power Relationship

```
P_delivered = R_total × V / η_propulsive

where η_propulsive = η_hull × η_rotative × η_open_water
```

Simplified approximation for calm water:
```
P ∝ Δ^(2/3) × V^n

where n ≈ 3 for friction-dominated (low speed)
      n ≈ 4-5 for wave-dominated (high speed, displacement hulls)
```

**Sensitivity:** At typical speeds, 10% speed increase → 30-50% power increase.

### Propeller Performance

```
Advance ratio: J = V_a / (n × D)
Thrust coefficient: K_T = T / (ρ × n² × D⁴)
Torque coefficient: K_Q = Q / (ρ × n² × D⁵)
Open water efficiency: η_0 = (J / 2π) × (K_T / K_Q)
```

Propeller operates on a characteristic curve. Deviation indicates:
- Hull resistance change (fouling, loading)
- Propeller damage or fouling
- Wake field changes

### Engine Performance

```
SFOC = ṁ_fuel / P_brake [g/kWh]

SFOC = f(load fraction, ambient conditions, fuel quality, engine condition)
```

Typical SFOC curve: minimum at 70-85% MCR, rises at low load and overload.

```
Brake thermal efficiency: η_th = P_brake / (ṁ_fuel × LCV)
Typical values: 40-50% for modern slow-speed diesels
```

### Hydrostatics

```
Δ = ρ_water × ∇ (displaced volume)

∇ = f(draft_fwd, draft_aft, hull geometry)
```

Hydrostatic tables (from hull design) convert draft readings to displacement and trim.

```
Trim = draft_aft - draft_fwd
Trim affects resistance: typically 2-5% variation across operational trim range
```

## Thermodynamic Relationships

### Heat Exchangers (Coolers)

```
Q̇ = ṁ × c_p × ΔT = U × A × LMTD

where:
  Q̇ = heat transfer rate
  ṁ = mass flow rate
  ΔT = temperature change
  U = overall heat transfer coefficient (degrades with fouling)
  A = heat transfer area
  LMTD = log mean temperature difference
```

Monitoring ΔT at constant load detects fouling/degradation.

### Turbocharger

```
Compressor power = ṁ_air × c_p × (T_out - T_in) / η_compressor
Turbine power = ṁ_exhaust × c_p × (T_in - T_out) × η_turbine

At equilibrium: Compressor power = Turbine power (minus bearing losses)
```

Turbocharger RPM at given engine load is a health indicator.

## Causal Structure

The master causal chain for fuel consumption:

```
FUEL CONSUMPTION
    ↑
Engine efficiency (SFOC at load point)
    ↑
Brake power required
    ↑
Shaft power required (+ gearbox losses)
    ↑
Thrust required / propulsive efficiency
    ↑
Total resistance × speed
    ↑
┌───────────────────────────────────────────────┐
│ Calm water resistance (hull, speed, loading)  │
│ + Wind resistance (wind speed, direction)     │
│ + Wave added resistance (sea state)           │
│ + Current effect (on speed through water)     │
│ + Shallow water effect (under-keel clearance) │
│ + Hull fouling (roughness increase)           │
└───────────────────────────────────────────────┘
```

To attribute fuel changes to any specific cause, all other branches must be measured or held constant.

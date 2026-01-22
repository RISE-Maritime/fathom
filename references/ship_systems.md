# Ship Systems

How ship systems connect to fundamental physical quantities. Use this to locate unfamiliar signals within the overall system structure.

## Propulsion System

**Function:** Convert fuel energy to ship motion

**Components and their physics:**

| Component | Fundamental Quantities | Governing Physics |
|-----------|----------------------|-------------------|
| Main engine | Energy conversion, mass flow | Thermodynamic cycle, combustion |
| Gearbox (if present) | Power, rotational speed | Mechanical efficiency, torque conversion |
| Shaft line | Power, rotational speed, torque | Mechanical transmission |
| Propeller | Force (thrust), power, velocity | Momentum transfer to water |
| Rudder | Force, angle | Hydrodynamic lift/drag |

**Key performance questions this system addresses:**
- Engine efficiency (how well fuel converts to shaft power)
- Propulsive efficiency (how well shaft power converts to thrust)
- Propeller condition (changes in characteristic curve)

**Signals you might encounter:**
- Fuel flow, fuel temperature, fuel pressure
- Cylinder pressures, exhaust temperatures
- Turbocharger RPM, boost pressure
- Shaft RPM, shaft torque, shaft power
- Propeller pitch (if CPP)

## Hull System

**Function:** Provide buoyancy and minimize resistance

**Components and their physics:**

| Component | Fundamental Quantities | Governing Physics |
|-----------|----------------------|-------------------|
| Hull shell | Position (draft), force (resistance) | Hydrostatics, hydrodynamics |
| Ballast system | Mass distribution | Stability, trim optimization |
| Hull coating | Surface roughness | Frictional resistance |

**Key performance questions this system addresses:**
- Hull fouling progression
- Optimal trim for efficiency
- Resistance characteristics

**Signals you might encounter:**
- Draft sensors (fwd, aft, midship)
- Ballast tank levels
- Hull stress monitoring
- Speed through water (hull-mounted log)

## Navigation System

**Function:** Determine position, motion, and environmental conditions

**Components and their physics:**

| Component | Fundamental Quantities | Governing Physics |
|-----------|----------------------|-------------------|
| GPS | Position, velocity (SOG) | Satellite ranging |
| Gyrocompass | Angular position (heading) | Gyroscopic precession |
| Speed log | Velocity (STW) | Doppler/correlation |
| Echo sounder | Position (depth) | Acoustic reflection |
| Anemometer | Velocity (wind) | Mechanical/ultrasonic sensing |
| Motion sensors | Acceleration, angular velocity | Inertial measurement |

**Key performance questions this system addresses:**
- Actual speed over/through water
- Environmental conditions encountered
- Operating patterns and utilization

**Signals you might encounter:**
- Position (lat/lon), SOG, COG
- Heading, rate of turn
- STW (longitudinal, transverse)
- Depth, under-keel clearance
- Apparent/true wind speed and direction
- Pitch, roll, heave

## Engine Auxiliary Systems

**Function:** Support main engine operation

**Subsystems:**

### Fuel System
- Quantities: Mass flow, temperature, pressure, density
- Physics: Fluid dynamics, combustion chemistry
- Performance link: Fuel quality affects SFOC, emissions

### Lubrication System
- Quantities: Pressure, temperature, flow rate
- Physics: Tribology, heat transfer
- Performance link: Bearing condition, friction losses

### Cooling System
- Quantities: Temperature, flow rate, pressure
- Physics: Heat transfer
- Performance link: Thermal efficiency, component life

### Air Intake System
- Quantities: Pressure, temperature, mass flow
- Physics: Thermodynamics, fluid flow
- Performance link: Combustion efficiency, power output

### Exhaust System
- Quantities: Temperature, pressure, composition
- Physics: Thermodynamics, emissions chemistry
- Performance link: Thermal efficiency, turbocharger performance

**Signals you might encounter:**
- Fuel viscosity, fuel temp at injectors
- LO pressure, LO temp, sump level
- Jacket water temp in/out, HT/LT cooling
- Scavenge air pressure, air cooler ΔT
- Exhaust temp per cylinder, exhaust manifold pressure

## Electrical System

**Function:** Generate and distribute electrical power

**Components and their physics:**

| Component | Fundamental Quantities | Governing Physics |
|-----------|----------------------|-------------------|
| Generators | Power (electrical), rotational speed | Electromagnetic induction |
| Switchboards | Power distribution, voltage, current | Electrical circuits |
| Motors | Power (mechanical), rotational speed | Electromagnetic torque |
| Batteries/storage | Energy, power | Electrochemistry |

**Performance link:** Auxiliary power consumption is part of total fuel consumption. Shaft generators couple electrical and propulsion systems.

**Signals you might encounter:**
- Generator power output, frequency, voltage
- Bus voltage, current, power factor
- Individual consumer loads
- Battery state of charge, charge/discharge rate

## Cargo System (Vessel-Type Dependent)

**Function:** Handle cargo safely and efficiently

**Physics connections:**
- Mass: Cargo weight directly affects displacement
- Position: Cargo distribution affects trim and stability
- Temperature: Reefer cargo, heated cargo, LNG boil-off
- Pressure: Tank pressures for gas/chemical carriers

**Performance link:** Cargo handling affects port time, cargo condition affects energy consumption (reefers, reliquefaction).

## HVAC and Hotel Systems

**Function:** Maintain habitable conditions

**Physics:** Thermodynamics, heat transfer, mass transfer (humidity)

**Performance link:** Usually minor for cargo vessels, significant for passenger vessels.

## Inferring Signal Meaning

When encountering an unfamiliar signal:

1. **Parse the signal name** — often indicates system and quantity
   - `me_` = main engine
   - `ae_` = auxiliary engine  
   - `_temp` = temperature
   - `_press` = pressure
   - `_flow` = flow rate

2. **Identify the system** — where does this measurement live?

3. **Identify the fundamental quantity** — what physical thing is being measured?

4. **Trace the causal path** — how does this connect to ship performance?

5. **Assess information value** — what question does this help answer, and what else would be needed?

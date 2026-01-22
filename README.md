# Fathom

**Fathom your maritime data** — assess what operational questions a dataset can answer using first-principles physics reasoning.

## What is Fathom?

Fathom is an AI agent skill that helps ship owners and maritime operators understand what their operational data can credibly answer before investing in analysis. Instead of using lookup tables or taxonomies, Fathom reasons from fundamental physics to assess data capabilities.

Given metadata about available signals (sensors, sample rates, coverage, quality), Fathom produces a structured assessment:

- **What questions can be answered** with high confidence
- **What questions are partially answerable** with explicit caveats
- **What questions cannot be answered** and why
- **What data extensions** would unlock new capabilities

## Why Fathom?

Ship owners face a chicken-and-egg problem: understanding what your data can answer requires expensive consulting, but you need that understanding to decide whether to invest.

Fathom lowers the cost to scope by providing physics-based capability assessment that:

- Reasons from first principles, not pattern matching
- Handles unfamiliar signals by tracing them to fundamentals
- Produces enterprise-ready reports with detailed reasoning
- Identifies highest-value data investments

## Installation

TODO

## Usage

Provide metadata about your dataset:

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
```

Then ask: *"Fathom this dataset"* or *"What questions can this data answer?"*

Fathom will produce a structured report covering data inventory, capability assessment, detailed physics reasoning, and prioritized recommendations.

## How It Works

Fathom doesn't use lookup tables. Instead, it:

1. **Maps signals to fundamental quantities** — mass, energy, force, velocity, pressure, temperature
2. **Identifies governing physics** — conservation of energy, momentum, mass
3. **Traces causal chains** — from fuel input through engine, shaft, propeller, to ship motion
4. **Assesses observability** — what's measured vs. what must be assumed
5. **Quantifies uncertainty** — how unobserved variables affect confidence

This approach works for any signal, including ones not explicitly documented, by reasoning from fundamentals.

## Skill Contents

```
fathom/
├── SKILL.md                              # Core methodology
└── references/
    ├── fundamentals.md                   # Governing physics
    ├── ship_systems.md                   # System-to-fundamentals mapping
    ├── reasoning_methodology.md          # Step-by-step assessment approach
    ├── calibration_anchors.md            # Order-of-magnitude reference values
    ├── worked_examples.md                # Complete reasoning demonstrations
    └── report_template.md                # Enterprise output format
```

## Example Output

See [`references/worked_examples.md`](references/worked_examples.md) for complete assessment examples including:

- Minimal dataset (tanker with SOG + fuel only)
- Rich dataset (container ship with shaft power, STW, drafts, wind)
- Unfamiliar signal reasoning

## Contributing

Contributions welcome. Key areas:

- Additional worked examples for different vessel types
- Calibration anchors for specialized vessels (offshore, passenger, etc.)
- Translations of the report template

## License

Apache 2.0 License — see [LICENSE](LICENSE)

## Acknowledgments

Developed at RISE Research Institutes of Sweden as part of maritime digitalization research.

---

*"To fathom" — to understand deeply; also a nautical unit of depth (6 feet), used for sounding the sea floor.*

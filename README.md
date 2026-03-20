# 🎨 design-system-extractor

A Claude Skill that reverse-engineers any UI screenshot into a complete, systematic design system — with personality scoring, design tokens, component inventory, light/dark mode anatomy, Figma sticker sheet spec, and a downloadable Markdown export.

---

## What It Does

Upload a screenshot of any UI. Claude will generate:

| Output | Description |
|--------|-------------|
| **Style Classification** | Product type, visual style, platform |
| **Personality Scores** | 5-dimension scoring: Warmth / Energy / Softness / Density / Formality |
| **Color Token Map** | Full color system with semantic tokens in `color.primary.500` format |
| **Typography Scale** | Font classification + H1–Caption scale with weights and line heights |
| **Spacing & Layout** | 8pt grid, spacing tokens, layout rhythm |
| **Shape & Depth** | Radius scale, border usage, shadow system |
| **Component System** | Button / Input / Card / Modal + all variants × states × tokens |
| **Light & Dark Mode** | Token diff anatomy for key components |
| **Design Patterns** | Navigation, forms, data display, feedback patterns |
| **Figma Sticker Sheet Spec** | Canvas layout, naming conventions, variant grouping guide |
| **Design Token JSON** | Complete structured JSON: color / spacing / radius / typography |
| **Personality Presets** | Named preset + Energetic and Formal variants |
| **Personality Slider Engine** | Input 5 slider values → full token system regeneration |

All output is saved as a single downloadable `.md` file.

---

## Installation

### Option A — Install `.skill` file directly

1. Download [`design-system-extractor.skill`](./design-system-extractor.skill)
2. In Claude.ai, open **Settings → Skills**
3. Click **Install from file** and select the `.skill` file

### Option B — Manual setup

Copy the contents of [`design-system-extractor/SKILL.md`](./design-system-extractor/SKILL.md) into your Claude Project instructions or use it as a system prompt prefix.

---

## Usage

### Basic — Extract a design system
```
[upload a UI screenshot]
"Analyze this screenshot and generate a design system"
```

### Advanced — With personality override
```
[upload a UI screenshot]
Personality Override:
  Warmth: 70
  Energy: 80
  Softness: 40
  Density: 60
  Formality: 30
```

### Trigger phrases
- "Extract the design tokens from this UI"
- "Reverse engineer the design language"
- "Create a sticker sheet from this app"
- "Generate a token JSON from this screenshot"
- "Make it more warm / formal / energetic"

---

## Output Example

```
## Style Classification
Product Type: Consumer App
Visual Style: Apple-like
Platform: iOS
Dominant Aesthetic: A refined, minimal mobile interface with generous whitespace and a monochromatic palette.

## Personality Scores
Warmth:    35 — cool gray background, desaturated blue primary
Energy:    55 — moderate contrast, visible CTA hierarchy
Softness:  80 — 16px card radius, diffuse shadows, pill buttons
Density:   30 — generous padding, few elements per screen
Formality: 65 — system font, strict grid, restrained color

Personality Summary: A calm, refined consumer product with Apple-like softness and professional restraint.
Preset Name: "Refined Minimal"
```

---

## Skill Structure

```
design-system-extractor/
└── SKILL.md        — Full 15-step extraction pipeline
design-system-extractor.skill   — Packaged install file
README.md
LICENSE
```

---

## Personality Slider Engine

The skill includes an optional adjustment engine. Provide 5 values (0–100) and Claude will regenerate the entire token system to match:

| Dimension | Effect |
|-----------|--------|
| Warmth ↑  | Warmer hues, higher saturation |
| Energy ↑  | Higher contrast, bolder weights |
| Softness ↑ | Larger radius, diffuse shadows |
| Density ↑ | Tighter spacing, more compact layout |
| Formality ↑ | Neutral palette, strict grid, professional type |

---

## Requirements

- Claude.ai (Pro / Team / Enterprise) with Skills enabled
- A UI screenshot (any platform — mobile, web, desktop)

---

## License

MIT — free to use, modify, and redistribute.

---

## Contributing

PRs welcome. Suggested improvements:
- Add CSS variable export alongside JSON tokens
- Add Tailwind config export
- Add iOS / Android platform-specific token formats
- Add component code generation (React / SwiftUI)

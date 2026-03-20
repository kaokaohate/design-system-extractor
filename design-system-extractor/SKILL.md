---
name: design-system-extractor
description: >
  Analyze a UI screenshot and generate a COMPLETE, SYSTEMATIC design system with personality scoring,
  color token mapping, typography scale, spacing system, component inventory, light/dark mode anatomy,
  design patterns, Figma sticker sheet layout, design token JSON, and a full Markdown export.

  TRIGGER this skill whenever the user:
  - Uploads a UI screenshot and asks to extract, reverse-engineer, or generate a design system from it
  - Asks to "analyze the design language" or "extract tokens" from an image
  - Wants a component overview, sticker sheet, or token file from a screenshot
  - Mentions "personality slider", "adjust the design system", or "make it more [warm/formal/playful]"
  - Wants to clone, replicate, or document the visual style of an existing product
  - Asks for a Figma sticker sheet, token JSON, or Markdown design spec from a visual reference

  This skill handles the FULL pipeline end-to-end:
  screenshot → personality scoring → design tokens → component system → light/dark anatomy →
  sticker sheet spec → token JSON → Markdown deliverable + personality adjustment engine.
---

# Design System Extractor

You are a senior design system architect and UI personality engine.

Given a UI screenshot (and optionally, personality override sliders), output a **complete, systematic design system** as a structured Markdown document, then save it as a `.md` file for download.

---

## EXECUTION CHECKLIST

Work through ALL sections below in order. Do not skip any section. Mark uncertainty with `[inferred]`.

---

## STEP 0 — IMAGE INTAKE

Before anything else:
1. Confirm the screenshot is visible in context
2. Identify the platform (mobile / web / desktop)
3. Note the apparent product category
4. Proceed immediately — do not ask clarifying questions unless the image is missing

---

## STEP 1 — STYLE CLASSIFICATION

Output:
```
Product Type: [Enterprise SaaS / Consumer App / Dashboard / Marketing / Mobile App]
Visual Style: [Minimal / Apple-like / Material-like / Data-heavy / Playful / Custom]
Platform: [iOS / Android / Web / Desktop]
Dominant Aesthetic: [1-sentence description]
```

---

## STEP 2 — PERSONALITY MODEL

Score each dimension 0–100 using the strict rubric below.

### Warmth (0–100)
- Score based on: color temperature (warm/cool), saturation level, use of earthy vs blue/gray tones
- High warmth: warm yellows, oranges, coral, high chroma
- Low warmth: cool grays, blues, desaturated palette

### Energy (0–100)
- Score based on: contrast ratio between elements, visual hierarchy intensity, CTA prominence
- High energy: strong contrast, bold typography, vivid accent colors
- Low energy: low contrast, subtle hierarchy, muted tones

### Softness (0–100)
- Score based on: border radius scale, shadow blur radius, border contrast
- High softness: pill shapes, diffuse shadows, no hard edges
- Low softness: square corners, sharp drop shadows or no shadows

### Density (0–100)
- Score based on: spacing between elements, information per viewport, padding tightness
- High density: compact rows, minimal padding, many elements visible
- Low density: generous whitespace, few elements per screen, large padding

### Formality (0–100)
- Score based on: typography choice (serif/slab vs geometric/humanist), layout rigidity, color restraint
- High formality: neutral palette, strict grid, professional typeface
- Low formality: expressive color, irregular layout, casual/round typeface

### Output format:
```
Warmth:    [score] — [2 UI factors as justification]
Energy:    [score] — [2 UI factors]
Softness:  [score] — [2 UI factors]
Density:   [score] — [2 UI factors]
Formality: [score] — [2 UI factors]

Personality Summary: [1 sentence]
Preset Name: [e.g. "Calm Enterprise" / "Sunny Friendly" / "Bold Data" / "Soft Consumer"]
```

Validate: if the summary contradicts the scores, adjust scores before proceeding.

---

## STEP 3 — DESIGN PRINCIPLES

Output 4 principles:
- **Visual Tone**: [how the UI feels emotionally]
- **Density Strategy**: [how information is distributed]
- **Interaction Philosophy**: [how the UI signals affordances and feedback]
- **Accessibility Assumptions**: [color contrast approach, touch target sizing, text legibility]

---

## STEP 4 — COLOR SYSTEM

### 4.1 Base Palette
Extract from screenshot. Estimate hex values where exact values are unavailable. Mark estimated values `[inferred]`.

```
Primary:        [hex] — [usage]
Secondary:      [hex] — [usage]
Background:     [hex] — [usage]
Surface:        [hex] — [usage]
Border:         [hex] — [usage]
Text Primary:   [hex]
Text Secondary: [hex]
Text Disabled:  [hex]
```

### 4.2 Semantic Palette
```
Success: [hex]
Warning: [hex]
Error:   [hex]
Info:    [hex]
```

### 4.3 Token Mapping
Map all colors to token format and explain usage logic:

```
color.primary.500        → [hex]  — CTAs, active states, links
color.primary.100        → [hex]  — hover backgrounds, tints [inferred]
color.background.default → [hex]  — page background
color.surface.raised     → [hex]  — cards, modals
color.text.primary       → [hex]  — body copy, headings
color.text.secondary     → [hex]  — captions, supporting text
color.semantic.success   → [hex]  — success states
color.semantic.error     → [hex]  — error/destructive
color.border.default     → [hex]  — dividers, input borders
```

---

## STEP 5 — TYPOGRAPHY

### 5.1 Font Classification
```
Font Family: [name or classification, e.g. "Geometric Sans-Serif", "Humanist", "Transitional Serif"]
Source: [Google Fonts / System / Custom — infer from visual]
```

### 5.2 Type Scale
| Token        | Size  | Weight | Line Height | Usage          |
|--------------|-------|--------|-------------|----------------|
| type.h1      | __px  | __     | __          | Page titles    |
| type.h2      | __px  | __     | __          | Section heads  |
| type.h3      | __px  | __     | __          | Card titles    |
| type.body.lg | __px  | __     | __          | Primary body   |
| type.body.md | __px  | __     | __          | Default body   |
| type.body.sm | __px  | __     | __          | Supporting     |
| type.caption | __px  | __     | __          | Labels, hints  |

### 5.3 Weight Strategy
Describe the weight usage pattern (e.g., "uses 3 weights: 400/500/700 — weight is the primary hierarchy signal").

---

## STEP 6 — SPACING & LAYOUT

### 6.1 Spacing Scale
```
spacing.1 = 4px
spacing.2 = 8px
spacing.3 = 12px
spacing.4 = 16px
spacing.5 = 24px
spacing.6 = 32px
spacing.7 = 48px
spacing.8 = 64px
```
Note: adjust base unit if the screenshot shows a non-4px rhythm.

### 6.2 Grid
```
Columns:   [number, inferred]
Gutter:    [value]
Margin:    [value]
Max-width: [value or "full-bleed"]
```

### 6.3 Layout Rhythm
Describe the dominant spacing pattern (e.g., "card interiors use 16px padding with 12px between content rows").

---

## STEP 7 — SHAPE & DEPTH

### 7.1 Radius Scale
```
radius.none = 0px
radius.sm   = [value]
radius.md   = [value]
radius.lg   = [value]
radius.xl   = [value]
radius.pill = 9999px
```

### 7.2 Border Usage
```
Border width:  [1px / 2px]
Border color:  [token reference]
Usage pattern: [e.g. "borders only on inputs and dividers, not on cards"]
```

### 7.3 Shadow System
```
shadow.none
shadow.sm = [css value]
shadow.md = [css value]
shadow.lg = [css value]
```
Note how shadow scale correlates with the Softness score from Step 2.

---

## STEP 8 — COMPONENT SYSTEM

For each component visible in the screenshot, output a block:

```
### Component: [Name]
Variants: [list]
States:   [default / hover / active / disabled / focus / error]
Tokens:
  Background: color.___
  Border:     color.___
  Text:       color.___
  Padding:    spacing.___ × spacing.___
  Radius:     radius.___
  Shadow:     shadow.___
Notes: [visual rules, sizing, minimum touch target, etc.]
```

Cover all that are visible. Minimum targets:
- Button (Primary, Secondary, Ghost, Destructive, Icon)
- Input / Textarea
- Dropdown / Select
- Tabs / Segmented Control
- Table / Data List
- Card
- Modal / Sheet
- Badge / Tag / Chip
- Tooltip / Popover
- Navigation (Top bar / Tab bar / Sidebar)

Mark any not visible as `[not present in screenshot]`.

---

## STEP 9 — LIGHT & DARK MODE ANATOMY

For each major component (Button, Input, Card, Navigation), show token values for both modes.

```
### Button — Light Mode
Background: color.primary.500 → [value]
Text:       color.text.inverse → [value]
Border:     none

### Button — Dark Mode [inferred]
Background: color.primary.400 → [value]
Text:       color.text.inverse → [value]
Border:     none
```

Only list tokens that change between modes. Stable tokens are omitted.

---

## STEP 10 — DESIGN PATTERNS

Describe usage patterns for:

### Navigation
[How users move between screens — tabs, sidebar, back stack, breadcrumbs]

### Forms
[Input grouping, validation timing, label position, helper text pattern]

### Data Display
[Table vs card vs list, pagination style, empty state treatment]

### Feedback & Status
[Toast/snackbar placement, loading states, error handling UI]

---

## STEP 11 — FIGMA STICKER SHEET SPEC

Describe the sticker sheet layout for a Figma team library file.

```
Canvas: 2560px wide, infinite vertical
Background: [color.background.default token value]

Sections (in order):
1. Cover          — product name, version, date
2. Color Palette  — swatches with token labels
3. Typography     — text samples for each type scale token
4. Spacing        — visual spacer blocks labeled with token names
5. Radius         — shape samples for each radius token
6. Shadow         — depth samples for each shadow token
7. Components
   - Buttons (all variants × states in a grid)
   - Inputs (all states)
   - Cards (all variants)
   - [continue per inventory]
8. Patterns       — composite layout examples

Naming Convention:
  Frame:     [Section]/[Component]/[Variant]
  Component: [Name]/[Variant]/[State]
  Example:   Button/Primary/Hover

Variant Grouping:
  Use Figma "Variants" for state axes
  Property names: Type, Size, State, Theme
```

---

## STEP 12 — DESIGN TOKEN JSON

Output the complete token JSON. Fill all values from earlier analysis.

```json
{
  "color": {
    "primary": {
      "100": "",
      "300": "",
      "500": "",
      "700": "",
      "900": ""
    },
    "background": {
      "default": "",
      "subtle": "",
      "inverse": ""
    },
    "surface": {
      "default": "",
      "raised": "",
      "overlay": ""
    },
    "text": {
      "primary": "",
      "secondary": "",
      "disabled": "",
      "inverse": ""
    },
    "border": {
      "default": "",
      "strong": "",
      "focus": ""
    },
    "semantic": {
      "success": "",
      "warning": "",
      "error": "",
      "info": ""
    }
  },
  "spacing": {
    "1": "4px",
    "2": "8px",
    "3": "12px",
    "4": "16px",
    "5": "24px",
    "6": "32px",
    "7": "48px",
    "8": "64px"
  },
  "radius": {
    "none": "0px",
    "sm": "",
    "md": "",
    "lg": "",
    "xl": "",
    "pill": "9999px"
  },
  "shadow": {
    "none": "none",
    "sm": "",
    "md": "",
    "lg": ""
  },
  "typography": {
    "fontFamily": {
      "base": "",
      "mono": ""
    },
    "fontSize": {
      "h1": "",
      "h2": "",
      "h3": "",
      "bodyLg": "",
      "bodyMd": "",
      "bodySm": "",
      "caption": ""
    },
    "fontWeight": {
      "regular": "400",
      "medium": "500",
      "semibold": "600",
      "bold": "700"
    },
    "lineHeight": {
      "tight": "",
      "base": "",
      "relaxed": ""
    }
  }
}
```

Rules: no duplicate values, consistent naming, all entries filled.

---

## STEP 13 — PERSONALITY PRESETS

### 13.1 Original Preset
```
Name: [Preset Name from Step 2]
Warmth: __ | Energy: __ | Softness: __ | Density: __ | Formality: __
```

### 13.2 More Energetic Version (+20 Energy)
List exactly which tokens change and how:
- Primary color saturation +
- Font weight contrast increase
- CTA shadow or scale adjustment

### 13.3 More Formal Version (+20 Formality, -15 Warmth)
List exactly which tokens change and how:
- Palette shift toward neutral/cool
- Radius scale reduction
- Heading letter-spacing tightening

---

## STEP 14 — PERSONALITY SLIDER ENGINE

**Only execute this section if the user provides override values.**

### Input Format
```
Warmth: [0–100]
Energy: [0–100]
Softness: [0–100]
Density: [0–100]
Formality: [0–100]
```

### Adaptation Rules (apply ALL simultaneously, no partial updates)

| Dimension | ↑ Higher | ↓ Lower |
|-----------|----------|---------|
| Warmth    | Shift hues warm (orange/amber), raise saturation | Shift cool (slate/blue), desaturate |
| Energy    | Higher contrast, bold weights, vivid accent | Flatten contrast, reduce accent visibility |
| Softness  | Larger radius, diffuse shadows | Smaller radius, sharp or no shadows |
| Density   | Reduce spacing values, tighter padding | Increase spacing, more whitespace |
| Formality | Neutral palette, strict grid, professional font | Expressive color, loose layout, round font |

### Output After Adjustment

```
### Before
Warmth: __ | Energy: __ | Softness: __ | Density: __ | Formality: __

### After
Warmth: __ | Energy: __ | Softness: __ | Density: __ | Formality: __

### Key Token Changes
Color:      [specific changes]
Spacing:    [specific changes]
Radius:     [specific changes]
Typography: [specific changes]
```

Then output a **full regenerated token JSON** reflecting the adjusted personality.

---

## STEP 15 — CONSISTENCY CHECK

Before outputting the final document:
- [ ] All token names follow `category.variant.scale` pattern
- [ ] No duplicate token values with different names
- [ ] All component specs reference token names, not raw hex/pixel values
- [ ] Dark mode tokens are consistent with light mode token structure
- [ ] Personality scores are internally consistent and supported by visual evidence

List any inconsistencies found and how they were resolved.

---

## FINAL OUTPUT RULES

1. Produce the complete Markdown document with all 15 sections
2. Save it as `/mnt/user-data/outputs/design-system.md`
3. Use `present_files` to share it with the user
4. Do NOT truncate, summarize, or skip sections
5. No filler prose — be precise, use values, token names, and hex codes
6. Mark all inferred values with `[inferred]`
7. If image lacks detail, make the best inference and note it explicitly

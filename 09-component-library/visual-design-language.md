---
Status: v0.1 — extracted from Figma (2026-06-28)
Source: https://www.figma.com/design/vPCSXGvVY2QutVrKmdyloo/Docside
Canvases used: Brand Building Blocks · Visual Design · Visual Design 2
---

# Visual Design Language

This document is the authoritative visual reference for all page iterations generated in this repo. When producing mockups, components, or screen specs, all values here supersede intuition or convention.

---

## 1. Color System

Colors are named. Always use the named token in specs; raw hex is for reference.

### 1.1 Primary — Ocean

| Name | Hex | Use |
|---|---|---|
| Ocean Deepest | `#051722` | Darkest background |
| Midnight Slate | `#0E2735` | Dark surface, footer |
| Ocean Dark | `#103D57` | Sidebar fill |
| Deep Ocean | `#115073` | **Primary brand blue** — nav, hero, CTAs |
| Ocean Mid | `#2C7096` | Active states, borders |
| Ocean | `#5590B1` | Secondary interactive |
| Ocean Light | `#8BB0C5` | Muted interactive |
| Ocean Pale | `#BFD0DB` | Dividers on dark |
| Ocean Ghost | `#DBE7EF` | Highlight tints |
| Ocean Whisper | `#EEF4F8` | Subtle background tints |

### 1.2 Neutral — Warm Gray

| Name | Hex | Use |
|---|---|---|
| Graphite | `#161616` | **Primary body text** |
| Ink | `#2D2D2B` | Secondary text |
| Ash | `#434341` | Tertiary text |
| Muted | `#70706C` | Placeholder, disabled |
| Stone | `#868682` | Subdued labels |
| Silver | `#B3B2AD` | Dividers on light |
| Haze | `#CAC9C2` | Borders, card strokes |
| Paper White | `#E0DFD8` | Subtle tint, separator |
| Linen | `#ECECE8` | Secondary background |
| Parchment | `#F6F5F3` | **Default page background** |
| White | `#FFFFFF` | Card/modal surface |

### 1.3 Accent — Coral / Label

Used exclusively for: labels, category tags, section eyebrows, call-to-action highlights. Never for body copy.

| Name | Hex |
|---|---|
| Label Deepest | `#2D140D` |
| Label Dark | `#5A281A` |
| Label Dark Mid | `#863C28` |
| Label Mid | `#B35035` |
| **Label** | **`#E06442`** (primary accent) |
| Label Light | `#E68368` |
| Label Pale | `#ECA28E` |
| Label Ghost | `#F3C1B3` |
| Label Whisper | `#F9E0D9` |

### 1.4 Semantic / Functional

| Use | Value |
|---|---|
| Image overlay — dark | `rgba(5, 23, 34, 0.5)` |
| Image overlay — hero tint | `rgba(8, 22, 55, 0.37)` |
| Image overlay — soft | `rgba(0, 0, 0, 0.2)` |
| Card accent header | `#E5F1F7` |
| CTA gradient | `linear-gradient(135deg, rgba(0,160,170,1) 9%, rgba(4,73,109,1) 93%)` |
| Panel glow shadow | `10px 10px 40px 0px rgba(27, 148, 185, 0.3)` |

---

## 2. Typography

Three font families; each has a strict role.

### 2.1 DM Sans — Display and Body

Primary typeface. Used for all headings, body copy, and UI text.

**Display**

| Style | Weight | Size | Line-height | Letter-spacing |
|---|---|---|---|---|
| Hero Title | Light 300 | 80px | 16px | -3.75% |
| Hero Highlight | ExtraBold 800 | 80px | 16px | -3.75% |
| Subtitle | SemiBold 600 | 48px | 0.16em | -2% |

**Headings (desktop)**

| Level | Weight | Size | Line-height | Letter-spacing |
|---|---|---|---|---|
| H1 | SemiBold 600 | 60px | 64px | -3.33% |
| H2 | SemiBold 600 | 48px | 48px | -4.17% |
| H3 | Medium 500 → SemiBold 600 | 40px | 40px | -5% |
| H4 | SemiBold 600 | 32px | 36px | -6.25% |
| H5 | SemiBold 600 | 24px | 28px | -4.17% |
| H6 | SemiBold 600 | 20px | 24px | -5% |

**Body**

| Scale | Weight | Size | Line-height | Letter-spacing |
|---|---|---|---|---|
| Body-XL | Regular 400 | 24px | 28px | -4.17% |
| Body-Lg | Regular 400 | 20px | 24px | -5% |
| Body-Md | Regular 400 | 16px | 20px | -6.25% |
| Body-Sm | Regular 400 | 14px | 16px | -7.14% |
| Body-Xsm | Regular 400 | 12px | 16px | -8.33% |

SemiBold 600 variants exist at every body scale (Body-XL-SemiBold … Body-Xsm-SemiBold) for emphasis within running text.

### 2.2 Readex Pro — Labels

Used exclusively for section eyebrows, category tags, and form field labels. Always UPPERCASE. Always in `#E06442` (Label) unless reversed on dark.

| Scale | Weight | Size | Line-height | Letter-spacing |
|---|---|---|---|---|
| Label-Lg | Bold 700 | 20px | 24px | +5% |
| Label-MD | Bold 700 | 16px | 20px | +6.25% |
| Label-Sm | Bold 700 | 14px | 16px | +7.14% |

Paragraph spacing: 16px. The positive letter-spacing and uppercase set distinguish Readex Pro from all DM Sans text at a glance — critical for hierarchy.

### 2.3 Plus Jakarta Sans — UI Micro

Used in component internals (badge text, chip labels) at 12–14px. ExtraBold 800 for Label-Sm contexts; Regular 400 for annotations.

---

## 3. Spacing and Layout

### 3.1 Canvas

| Property | Value |
|---|---|
| Desktop frame | 1920 × 1080 |
| Sidebar width | 317px |
| Sidebar (content area) | 317 × 712 px |

### 3.2 Elevation and Depth

| Level | Shadow |
|---|---|
| Panel / modal | `10px 10px 40px 0px rgba(27, 148, 185, 0.3)` |
| Card | `1px solid #CAC9C2` (stroke only) |

### 3.3 Border Radius

| Context | Radius |
|---|---|
| Small card / flowchart node | 7px |
| Form card / input area | 15px |
| Rounded panel / section block | 20px |
| Avatar / icon circle | 35px |
| CTA button icon block | 10px |

### 3.4 Stroke

| Context | Value |
|---|---|
| Card border | 3.5px solid `#D4D4D4` |
| Card divider | 1px solid `#CAC9C2` |
| Sketch / wireframe lines | 2px solid `#000000` |

---

## 4. Surface Patterns

How backgrounds layer across page sections:

| Surface | Fill | Use |
|---|---|---|
| Page default | `#F6F5F3` (Parchment) | Most content sections |
| Card / modal | `#FFFFFF` | Any contained element |
| Hero / dark section | `#115073` (Deep Ocean) | Nav, top hero, CTA bands |
| Darkest hero | `#0E2735` (Midnight Slate) | Footer, deep-dark sections |
| Card accent header | `#E5F1F7` | Top band inside detail cards |
| Section divider | `1px solid #CAC9C2` | Between card zones |

Image backgrounds always carry a `rgba(5,23,34,0.5)` overlay minimum. Hero tints use `rgba(8,22,55,0.37)` inside a blurred panel inset.

---

## 5. Screen Vocabulary (from Figma canvases)

These are the named screens in the Figma file. When writing specs or mockups for any of these, pull color, type, and spatial values from §1–4 above.

| Screen | Canvas | Notes |
|---|---|---|
| Upload your offer PDF | Visual Design | Upload zone, 25 MiB PDF limit; two-pane shell |
| Manage and Upload Documents | Visual Design 2 | Warm off-white + Deep Ocean variants both exist |
| Submit an Offer | Visual Design 2 | Off-white and dark variants |
| My Properties | Visual Design 2 | Off-white + dark variants |
| User Selects a Property | Visual Design 2 | Off-white + dark variants |
| New Property | Visual Design 2 | Property creation flow |
| Property Created | Visual Design 2 | Confirmation state |
| Links | Visual Design 2 | Multiple link-list variants |
| Hero | Visual Design | Background image + dark overlay + hero text |
| Wireframe / flow | Wireframe Sketch Design | Architecture reference, not a pixel spec |

---

## 6. Key Component Patterns

### Upload Zone

- Outer frame: white card, 15px radius, `1px solid #CAC9C2`
- Accent header band: `#E5F1F7`, `15px 15px 0 0` radius, 101px tall
- Divider: `1px solid #CAC9C2`
- Eyebrow label: Readex Pro Bold, `#E06442`, UPPERCASE
- Descriptor: DM Sans Regular 400, 20px, `#2D2D2B`, e.g. "PDF only, up to 25 MiB."
- CTA icon block: 54×54px, `10px` radius, teal-to-navy gradient

### Two-Pane Shell

- Left sidebar: `317px`, fill `#103D57` (Ocean Dark) or `#CCCCCC` for wireframe
- Sidebar top block: `317 × 113px`, rounded top `20px`
- Sidebar bottom block: `317 × 73px`, rounded bottom `20px`
- Main area: fills remaining width (1603px at 1920 canvas)

### Card

- White fill, `7px` radius (flowchart) or `15–20px` (content cards)
- `3.5px solid #D4D4D4` border
- Panel glow when elevated: `10px 10px 40px 0px rgba(27,148,185,0.3)`

### Gradient CTA Button

- Fill: `linear-gradient(135deg, rgba(0,160,170,1) 9%, rgba(4,73,109,1) 93%)`
- Icon inset: 54×54px, 10px radius
- Icon color: white

---

## 7. What this file is not

- It does not define interaction states (see `08-states-and-edge-cases.md`).
- It does not define copy voice (see `10-copy-guidelines.md`).
- It does not define components structurally — only their visual shape. Structural specs belong in a companion `component-specs.md` once screen mockups have proven their form (per the existing README).
- Pixel-perfect implementation belongs in the main repo (`manderso90/docside`).

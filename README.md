# 🌸 Pregnancy Due Date Calculator — #002 of 100

> **100 Websites Challenge — #002.** A warm, beautifully designed Pregnancy Due Date Calculator built as a single self-contained React component. Three calculation methods, trimester tracking, a 10-milestone timeline, and zero external dependencies.

![React](https://img.shields.io/badge/React-18-61DAFB?style=flat-square&logo=react)
![Challenge](https://img.shields.io/badge/100%20Websites-002%2F100-c06a4a?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

---

## ✨ Features

### 3 Calculation Methods
| Tab | Input | Method |
|-----|-------|--------|
| **Last Period** | First day of last menstrual period + optional cycle length | Naegele's Rule — LMP + 280 days, adjusted for cycle length |
| **Conception Date** | Estimated conception date | 266 days (38 weeks) forward from conception |
| **Weeks Along** | How many weeks pregnant you currently are | Back-calculates LMP, then applies Naegele's Rule |

### Results Panel
- **Due date hero** — Full weekday + date displayed in large elegant type
- **Days to go** — Exact days remaining (or days past due date)
- **Weeks + days pregnant** — e.g., "14w 3d pregnant"
- **Early delivery window** — 38–41 week range shown as a pill badge
- **Pregnancy progress bar** — Animated fill showing exact % complete
- **Trimester indicator** — 3 cards with current trimester highlighted
- **Stats grid** — Weeks pregnant, days remaining, months along, total days pregnant
- **Estimated conception date** — Calculated and displayed regardless of input method
- **10-milestone timeline** — Each milestone shows done / current / upcoming status with a description

### Milestones Tracked
| Week | Milestone |
|------|-----------|
| 4    | Positive Pregnancy Test |
| 8    | First Prenatal Visit |
| 12   | End of First Trimester |
| 16   | Anatomy Scan Preparation |
| 20   | Anatomy Ultrasound — halfway! |
| 24   | Viability Milestone |
| 28   | Third Trimester Begins |
| 32   | Growth Scan |
| 36   | Full Term Approaching |
| 40   | Estimated Due Date 🌸 |

### UX Details
- Adjustable cycle length (20–45 days) for LMP method
- Week stepper with ▲▼ buttons for the "Weeks Along" tab
- Input validation with shake animation for out-of-range or future dates
- Staggered entrance animations on all result cards
- Reset button to start over cleanly
- Fully responsive from 360px mobile to wide desktop

---

## 🎨 Design

**Aesthetic:** Warm, organic, morning-journal feel — completely different from the dark luxury style of #001.

**Typography**
| Font | Weights | Usage |
|------|---------|-------|
| Cormorant Garamond | 300, 400, 600, 700 | Display headings, due date, large numbers |
| Nunito | 300, 400, 500, 600, 700 | Body text, buttons, labels |
| Nunito Sans | 300, 400, 600 | Captions, uppercase labels, hints |

**Color Palette**
| Token | Value | Usage |
|-------|-------|-------|
| `--cream` | `#fdf6ee` | Page background |
| `--parchment` | `#f5e9d8` | Card backgrounds, tab bar |
| `--blush` | `#f2c4b0` | Progress fill start, accents |
| `--rose` | `#d98a72` | Inputs focus, progress mid |
| `--terracotta` | `#c06a4a` | Primary brand color, headings |
| `--sage` | `#8aaa8a` | Secondary accent, trimester 2 |
| `--sage-dark` | `#5c7a5c` | Sage text on pale backgrounds |
| `--ink` | `#3a2f2a` | Primary text |
| `--muted` | `#a08878` | Labels, hints, secondary text |

**Background:** Three layered radial gradients (blush, sage, cream) with three animated floating blur blobs that drift continuously.

---

## 🚀 Getting Started

### Option A — Standalone React app

```bash
npx create-react-app my-pregnancy-calculator
cd my-pregnancy-calculator
# Copy PregnancyCalculator.jsx into src/
# Replace src/App.js with:
```

```jsx
import PregnancyCalculator from './PregnancyCalculator';

export default function App() {
  return <PregnancyCalculator />;
}
```

```bash
npm start
```

### Option B — Drop into an existing project

```jsx
import PregnancyCalculator from './components/PregnancyCalculator';

// Render anywhere — it's fully self-contained
<PregnancyCalculator />
```

No CSS imports needed. All styles are injected via an internal `<style>` tag. No third-party dependencies beyond React.

---

## 📐 How the Calculations Work

### Last Period (LMP) — Naegele's Rule
```
Due Date = LMP + 280 days + (cycleLength - 28) days
```
The cycle length adjustment accounts for cycles that are shorter or longer than the standard 28 days. A 35-day cycle shifts the due date 7 days later; a 21-day cycle shifts it 7 days earlier.

### Conception Date
```
LMP (estimated) = Conception Date − 14 days
Due Date        = LMP + 280 days
```
Assumes ovulation (and therefore conception) occurred on day 14 of the cycle.

### Weeks Along
```
LMP (estimated) = Today − (weeks × 7 days)
Due Date        = LMP + 280 days
```

### Progress Percentage
```
Progress % = (days since LMP / total pregnancy days) × 100
```
Clamped between 0% and 100%. Accounts for cycle-length-adjusted total duration.

### Early Delivery Window
```
Early boundary = Due Date − 14 days  (38 weeks)
Late boundary  = Due Date + 7 days   (41 weeks)
```

---

## 🗂️ File Structure

```
pregnancy-calculator/
├── PregnancyCalculator.jsx   # The entire app — one file, fully self-contained
└── README.md
```

### Internal structure of `PregnancyCalculator.jsx`

```
PregnancyCalculator.jsx
├── css (string)              — All styles as a tagged template literal
├── MILESTONES (array)        — 10 key pregnancy milestones with week + description
├── TRIMESTERS (array)        — Trimester definitions with icon, name, week range
├── addDays()                 — Date utility
├── fmtDate()                 — Full long-form date formatter
├── fmtShort()                — Short date formatter for the window range
├── calcFromLMP()             — Core calculation: LMP + cycle → all result values
├── calcFromConception()      — Wraps calcFromLMP after back-calculating LMP
├── calcFromWeeks()           — Wraps calcFromLMP after back-calculating LMP from weeks
├── getTrimester()            — Returns 0, 1, or 2 based on current week
└── PregnancyCalculator       — Main component (tabs, validation, results render)
```

---

## 📋 Input Validation

| Input | Rules |
|-------|-------|
| Last period date | Must be in the past · Max 42 weeks ago (294 days) |
| Conception date | Must be in the past |
| Weeks along | Must be between 1 and 42 |

Errors display inline with a shake animation. The calculate button does nothing until inputs are valid.

---

## 📦 Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| `react` | ^18.0.0 | UI framework |
| `react-dom` | ^18.0.0 | DOM rendering |

No date libraries. No UI component libraries. No CSS frameworks. Everything is native JavaScript `Date` API and self-written CSS.

---

## ♿ Accessibility Notes

- All form inputs use native `<input type="date">` and `<input type="number">` — fully keyboard and screen-reader accessible
- Color is never the sole indicator of state (trimester cards use border + background changes)
- Focus states are preserved on all interactive elements
- The week stepper buttons are labeled via visible ▲▼ symbols

---

## 🗺️ Roadmap

- [ ] Baby size comparison (e.g., "the size of a lemon at week 14")
- [ ] Zodiac sign of expected baby
- [ ] Printable / shareable due date card
- [ ] Save state to `localStorage` so results persist on refresh
- [ ] Dark mode toggle

---

## ⚠️ Disclaimer

This calculator is for **informational and educational purposes only**. Due dates are estimates — only about 5% of babies are born on their exact due date. Always consult your healthcare provider or OB-GYN for medical advice and accurate dating via ultrasound.

---

## 📄 License

MIT © Fahad — free to use, fork, and build on.

---

> *Part of the **100 Websites in 100 Days** challenge — one production-quality website shipped every day.*
> *#001 — Age Calculator · **#002 — Pregnancy Due Date Calculator** · #003 — Medicine Reminder*

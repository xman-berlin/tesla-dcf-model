# Tesla DCF Valuation Model

Interaktives Browser-basiertes Tool zur DCF-Bewertung von Tesla (2025-2035) mit einstellbaren Annahmen für alle Geschäftssegmente.

## About

Dieses Tool modelliert den fairen Wert von Tesla basierend auf Discounted Cash Flow Analyse. Es berücksichtigt nicht nur aktuelle Revenue-Streams (Automotive, Energy, Services), sondern auch zukünftige Potenziale wie Robotaxi, FSD Software, Optimus und Terafab. Alle Annahmen sind über Slider und Inputs anpassbar, Ergebnisse werden in Echtzeit aktualisiert.

## Tech Stack

| Layer | Choice |
|-------|--------|
| UI | Single HTML-Datei, CSS Grid/Flexbox |
| Charts | Chart.js |
| Logic | Pure JavaScript (clientseitig) |
| Export | CSV-Download |

## Getting Started

### Prerequisites

- Moderner Browser (Chrome, Firefox, Safari, Edge)
- Keine Installation nötig

### Installation

```bash
git clone git@github.com:<user>/tesla-dcf-model.git
cd tesla-dcf-model
```

### Usage

```bash
open index.html
```

Oder einfach `index.html` im Browser öffnen.

## Features

### Einstellbare Assumptions (Sidebar)

- **Automotive** – Lieferwachstum, ASP, Margen
- **Energy & Storage** – Wachstum, Megafactory-Ausbau
- **FSD Software** – Subscriber-Wachstum, Abo-Preis, Lizensierung
- **Robotaxi** – Flottengröße, Preis/Meile, Utilization
- **Optimus** – Units, ASP, Margin-Skalierung
- **Terafab** – Platzhalter für zukünftige Revenue-Streams
- **DCF-Parameter** – WACC, Terminal Growth, Steuersatz

### Tabs

1. **Dashboard** – KPI-Karten, Revenue-Chart, FCF-Chart, Szenarien
2. **Revenue Detail** – Segment-Tabellen mit Units, ASP, Revenue, Margin
3. **DCF Calculation** – FCF-Berechnung, Terminal Value, Fair Value per Share
4. **Sensitivity** – Heatmaps und Tornado Charts

### Szenarien

| Szenario | WACC | Terminal Growth | Robotaxi | Optimus |
|----------|------|-----------------|----------|---------|
| Bull | 9% | 4% | 1.5x | 2.0x |
| Base | 11% | 3% | 1.0x | 1.0x |
| Bear | 13% | 2% | 0.5x | 0.3x |

## Project Status

- [x] HTML-Grundstruktur + CSS Layout
- [x] Assumptions-Panel (Slider/Inputs/Toggles)
- [x] Berechnungslogik (JavaScript)
- [x] Dashboard KPI-Karten
- [x] Charts (Revenue, FCF, Segment Mix)
- [x] Revenue Detail Tabelle
- [x] DCF Calculation Tabelle
- [x] Sensitivity Heatmap + Tornado Chart
- [x] CSV-Export
- [x] Polishing

See [plan.md](./plan.md) for the full implementation plan.

## Data Sources

| Source | Data |
|--------|------|
| Tesla 10-K 2024 (SEC) | Revenue, Margins, Shares |
| Tesla Q4 2025 Earnings | Energy, FSD Subscribers, Deliveries |
| Wolfe Research (Feb 2026) | Robotaxi $250B by 2035 |
| Deutsche Bank (Sep 2024) | Optimus $10B by 2035 |
| Goldman Sachs (Jan 2026) | Humanoid Market $38B by 2035 |
| ARK Invest (2024) | $24T Global Robotics TAM |

## Disclaimer

Dies ist kein Investment-Rat. Alle Annahmen sind spekulativ.

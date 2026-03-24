# Tesla DCF Valuation Model – Interaktives Web-Tool

## Status: Plan freigegeben, Implementierung ausstehend

## Ziel
Ein interaktives Browser-basiertes Tool zur DCF-Bewertung von Tesla (2025-2035) mit einstellbaren Annahmen für alle Geschäftssegmente, inklusive zukünftiger Revenue-Streams wie Robotaxi, Optimus, FSD und Terafab.

---

## Technologie
- **Single HTML-Datei** – kein Build-Prozess, im Browser öffnen
- **Chart.js** – für Visualisierungen
- **Pure JavaScript** – Berechnungen clientseitig
- **CSS Grid/Flexbox** – responsives Layout
- **CSV-Export** – für Numbers-Import

## Dateistruktur
```
tesla-dcf-tool/
├── index.html          # Hauptdatei (alles in einer Datei)
└── README.md           # Bedienungsanleitung
```

---

## Datenbasis (aktuell März 2026)

### Tesla 2025 (FY, aus Q4 2025 Earnings)
| Kennzahl | Wert |
|---|---|
| Total Revenue | $94.8B (erster Umsatzrückgang ever, -3% YoY) |
| Automotive Revenue | $69.5B (-10% YoY) |
| Energy Generation & Storage | $12.8B (+27% YoY) |
| Services & Other | $12.5B (+19% YoY) |
| Lieferungen 2025 | ~1.79M Units |
| Operating Margin | ~6-7% |
| Free Cash Flow | ~$3.6B (2024) |
| Cash & Investments | $36.6B |
| Shares Outstanding | 3.216B |
| Net Cash Position | ~$32B (nach Abzug Schulden) |

### FSD Software
- 1.1M aktive Subscribers (Ende 2025, erstmalig offiziell disclosed)
- $99/Monat Abonnement
- +38% YoY Subscriber-Wachstum
- Uebergang zu reinem Abo-Modell ab Feb 2026

### Robotaxi (Quellen: Wolfe Research Feb 2026, Tesla Earnings)
- Start: Austin, Juni 2025 (supervised), Jan 2026 (unsupervised)
- Expansion 2026: Dallas, Houston, Phoenix, Miami, Orlando, Tampa, Las Vegas
- Flotte 2026: ~7,200 Fahrzeuge geplant
- Wolfe Research: $30B Revenue by 2030, $250B by 2035
- Annahmen: 30% AV-Penetration, 50% Tesla-Marktanteil, $1/Meile
- Gross Breakeven: 2027 erwartet
- Musk: <$0.20/Meile mit Cybercab moeglich bis 2030

### Optimus (Quellen: Goldman Sachs, Deutsche Bank, Tesla Earnings)
- Goldman Sachs: $38B humanoid market by 2035
- Deutsche Bank: $10B Tesla-Optimus-Revenue by 2035 (200K Units x $50K)
- Target-Preis: $20K-$30K bei Skalierung
- Produktion: Ende 2026 (intern), 2027 (extern)
- Fremont-Factory: Model S/X Produktion eingestellt, Umbau fuer Optimus
- Musk: "$10T+ long-term potential"
- Roadmap: 2025 ~800 Units intern -> 2027 10K-50K -> 2030 100K-1M

### Energy Storage
- 46.7 GWh deployed in 2025 (+49% YoY)
- Revenue: $12.8B (+27% YoY)
- Record Margins 5 Quartale in Folge
- Megafactories: Lathrop (CA), Shanghai, Houston (50 GWh geplant)
- Megapack 3 + Mega Block Launch 2026
- Starke Nachfrage von Data Centern (xAI: $430M in 2025)

---

## UI-Layout

### Sidebar (links, ~300px breit)
Akkordeon-Struktur, pro Segment eine Sektion:

#### 1. Automotive
- Slider: Lieferwachstum 2026-2030 (0-25%, Default: 10%)
- Slider: Lieferwachstum 2031-2035 (0-15%, Default: 7%)
- Input: ASP ($30K-$50K, Default: $38,800)
- Slider: Gross Margin (12-25%, Default: 18%)
- Toggle: Neue guenstige Modelle (+ Input fuer erwartete Units/ASP)

#### 2. Energy & Storage
- Slider: Jaehrliches Wachstum (10-50%, Default: 25%)
- Slider: Gross Margin (20-35%, Default: 26%)

#### 3. Services
- Slider: Jaehrliches Wachstum (5-25%, Default: 15%)

#### 4. FSD Software
- Input: Aktuelle Subscribers (Default: 1.1M)
- Slider: Wachstum p.a. (10-50%, Default: 30%)
- Input: Preis/Monat ($50-$200, Default: $99)
- Toggle: Externe Lizensierung (+ Input Revenue-Schaetzung)

#### 5. Robotaxi
- Input: Startjahr (Default: 2026)
- Slider: Flotte 2026 (1K-20K, Default: 7,200)
- Slider: Flottenwachstum p.a. (50-300%, Default: 150%)
- Slider: Preis/Meile ($0.20-$2.00, Default: $1.00)
- Slider: Utilization Rate (30-80%, Default: 55%)
- Slider: Meilen pro Fahrzeug/Tag (50-300, Default: 150)

#### 6. Optimus
- Input: Startjahr Produktion (Default: 2027)
- Slider: Units 2027 (1K-100K, Default: 25K)
- Slider: Units 2030 (50K-2M, Default: 500K)
- Slider: Units 2035 (200K-10M, Default: 2M)
- Slider: ASP ($15K-$100K, Default: $30K)
- Slider: Gross Margin Initial (5-20%, Default: 10%)
- Slider: Gross Margin at Scale (25-50%, Default: 40%)

#### 7. Terafab (Platzhalter)
- Toggle: Aktivieren
- Input: Startjahr
- Input: Revenue-Schaetzung pro Jahr

#### 8. DCF-Parameter
- Slider: WACC (7-15%, Default: 10%)
- Slider: Terminal Growth Rate (1-5%, Default: 3%)
- Slider: Steuersatz (10-25%, Default: 18%)
- Input: Shares Outstanding (Default: 3.216B)
- Input: Net Debt (Default: -$32B, also Net Cash)

### Main Area (rechts)

#### Tab-Leiste
- Tab 1: Dashboard
- Tab 2: Revenue Detail
- Tab 3: DCF Calculation
- Tab 4: Sensitivity

#### Tab 1: Dashboard (Default)
- **KPI-Karten oben:**
  - Fair Value per Share (gross, prominent)
  - Total Revenue 2035
  - Total FCF 2035
  - Implied Market Cap

- **Chart 1: Revenue Forecast 2025-2035** (Stacked Area Chart)
  - Stacked: Automotive (blau), Energy (gruen), Services (grau), FSD (orange), Robotaxi (rot), Optimus (lila), Terafab (gestrichelt)

- **Chart 2: Revenue Mix 2025 vs 2035** (Donut Charts nebeneinander)

- **Chart 3: FCF Development** (Bar Chart 2025-2035)

- **Chart 4: Valuation Summary** (Horizontal Bar: Bull/Base/Bear)

#### Tab 2: Revenue Detail
- Tabelle pro Segment: Jahr | Units | ASP | Revenue | COGS | Gross Profit | Margin
- Editierbare Zeilen fuer manuelle Overrides

#### Tab 3: DCF Calculation
- Tabelle: Jahr | FCF | Discount Factor | PV(FCF)
- Terminal Value Berechnung
- Enterprise Value -> Equity Value -> Per Share
- Formel-Erklaerung sichtbar

#### Tab 4: Sensitivity
- **Heatmap:** WACC (X-Achse) x Terminal Growth (Y-Achse) = Fair Value
- **2D Sensitivity:** Robotaxi-Marktanteil x Optimus-Units = Fair Value
- **Tornado Chart:** Welche Assumption hat groessten Impact auf Fair Value?

### Footer
- CSV-Export Button
- Reset to Defaults Button
- Disclaimer: "Dies ist kein Investment-Rat. Alle Annahmen sind spekulativ."

---

## Berechnungslogik (JavaScript Pseudocode)

### Revenue Projections

```javascript
// Automotive
for (let year = 2026; year <= 2035; year++) {
  const growth = year <= 2030 ? autoGrowthEarly : autoGrowthLate;
  units = units * (1 + growth);
  revenue = units * asp;
  grossProfit = revenue * autoMargin;
}

// Energy
for (let year = 2026; year <= 2035; year++) {
  revenue = revenue * (1 + energyGrowth);
  grossProfit = revenue * energyMargin;
}

// FSD
for (let year = 2026; year <= 2035; year++) {
  subscribers = subscribers * (1 + fsdGrowth);
  revenue = subscribers * monthlyPrice * 12;
}

// Robotaxi
for (let year = 2026; year <= 2035; year++) {
  if (year >= robotaxiStartYear) {
    fleet = fleet * (1 + fleetGrowth);
    milesPerYear = fleet * milesPerDay * 365 * utilization;
    revenue = milesPerYear * pricePerMile;
  }
}

// Optimus
for (let year = 2026; year <= 2035; year++) {
  if (year >= optimusStartYear) {
    units = interpolate(optimusStartYear, optimusEndYear, unitsStart, unitsEnd);
    revenue = units * asp;
    margin = interpolate(0.10, optimusMarginScale, progress);
    grossProfit = revenue * margin;
  }
}
```

### DCF Calculation

```javascript
// Operating Expenses (als % von Revenue)
const opex = totalRevenue * opexPercent; // Default: 10%

// EBIT
const ebit = totalGrossProfit - opex;

// Taxes
const taxes = Math.max(0, ebit * taxRate);

// Net Income (vereinfacht)
const netIncome = ebit - taxes;

// Free Cash Flow
const depreciation = totalRevenue * 0.05; // ~5% von Revenue
const capex = totalRevenue * capexPercent; // Default: 12%
const fcf = netIncome + depreciation - capex;

// Terminal Value
const terminalValue = fcf2035 * (1 + terminalGrowth) / (wacc - terminalGrowth);

// Present Values
let pvFCFs = 0;
for (let i = 0; i < 10; i++) {
  pvFCFs += fcfs[i] / Math.pow(1 + wacc, i + 1);
}
const pvTerminal = terminalValue / Math.pow(1 + wacc, 10);

// Enterprise & Equity Value
const enterpriseValue = pvFCFs + pvTerminal;
const equityValue = enterpriseValue + netCash;
const fairValuePerShare = equityValue / sharesOutstanding;
```

### Szenarien

```javascript
const scenarios = {
  bull: { wacc: 0.09, terminalGrowth: 0.04, robotaxiMultiplier: 1.5, optimusMultiplier: 2.0 },
  base: { wacc: 0.11, terminalGrowth: 0.03, robotaxiMultiplier: 1.0, optimusMultiplier: 1.0 },
  bear: { wacc: 0.13, terminalGrowth: 0.02, robotaxiMultiplier: 0.5, optimusMultiplier: 0.3 }
};
```

---

## Erweiterbarkeit

### Terafab hinzufuegen
1. Toggle in Assumptions aktivieren
2. Startjahr und Revenue-Schaetzung eingeben
3. Dashboard-Charts zeigen neuen Stream automatisch

### Weitere Segments
- Kopiere die Struktur von Robotaxi/Optimus-Bloecken
- Fuege neue Sektion in Sidebar hinzu
- Fuege neue Farbe und Datenreihe in Charts hinzu

---

## Referenzen

| Quelle | Daten |
|---|---|
| Tesla 10-K 2024 (SEC) | Revenue, Margins, Shares |
| Tesla Q4 2025 Earnings | Energy, FSD Subscribers, Deliveries |
| Wolfe Research (Feb 2026) | Robotaxi $250B by 2035 |
| Deutsche Bank (Sep 2024) | Optimus $10B by 2035 |
| Goldman Sachs (Jan 2026) | Humanoid Market $38B by 2035 |
| ARK Invest (2024) | $24T Global Robotics TAM |

---

## Implementierungs-Reihenfolge

- [ ] 1. HTML-Grundstruktur + CSS Layout (Sidebar + Main)
- [ ] 2. Assumptions-Panel (alle Slider/Inputs/Toggles)
- [ ] 3. Berechnungslogik (JavaScript)
- [ ] 4. Dashboard KPI-Karten
- [ ] 5. Charts (Revenue Forecast, FCF, Segment Mix)
- [ ] 6. Revenue Detail Tabelle
- [ ] 7. DCF Calculation Tabelle
- [ ] 8. Sensitivity Heatmap + Tornado Chart
- [ ] 9. CSV-Export Funktion
- [ ] 10. Polishing: Tooltips, Responsiveness, Defaults

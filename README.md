# Dr. Polamarasetty Praveen Kumar

**Energy Asset Optimisation, Multi-Market Bidding, MILP Dispatch, Risk Analytics**

📧 praveenindia.p@gmail.com &nbsp;|&nbsp; 📍 Porto, Portugal &nbsp;|&nbsp; 🟢 Available: July 2026 &nbsp;|&nbsp; 🇪🇺 EU Work Authorization

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat-square&logo=linkedin)](https://linkedin.com/in/polamarasetty-praveen-kumar-2a3a422a1)
[![Google Scholar](https://img.shields.io/badge/Google%20Scholar-H--Index%2022%20·%201%2C500%2B%20citations-4285F4?style=flat-square&logo=googlescholar)](https://scholar.google.com/citations?user=8EFqCyAAAAAJ)
[![Publications](https://img.shields.io/badge/Publications-70%2B-orange?style=flat-square)]()

---

## About Me

Energy systems researcher and industrial-grade software engineer with deep expertise in **hybrid plant optimisation, multi-market bidding and scheduling, and MILP-based dispatch**.

Built a production-grade **14-gate multi-market MILP bidding and scheduling system** (DA + IDA1/2/3 + XBID + aFRR + mFRR + ISP dispatch simulation + settlement + analytics) for the real **Alqueva hybrid plant** (518.4 MW PSP + 5 MWp PV + 1 MW / 2 MWh BESS, Portugal / MIBEL). System uses IBM CPLEX, auto-selects ML forecasters (Naive / Ridge / LightGBM via walk-forward CV), and applies a permanent **13-invariant physical checker** that blocks any bid with a constraint violation before it propagates. Risk framework includes historical VaR/CVaR (95 % & 99 %) and Monte Carlo bootstrap confidence intervals (n=10,000).

---

## ⚡ Flagship Project: Alqueva 24-Hour Energy Trading Optimizer

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=flat-square&logo=python)](https://python.org)
[![CPLEX](https://img.shields.io/badge/Solver-CPLEX%2022.1-brightgreen?style=flat-square&logo=ibm)](https://ibm.com/cplex)
[![Fallback](https://img.shields.io/badge/Fallback-HiGHS%20%7C%20CBC-green?style=flat-square)]()
[![MILP](https://img.shields.io/badge/Optimisation-MILP-orange?style=flat-square)]()
[![Markets](https://img.shields.io/badge/Markets-DA%20%7C%20IDA1--3%20%7C%20XBID%20%7C%20aFRR%20%7C%20mFRR-purple?style=flat-square)]()
[![Grid](https://img.shields.io/badge/Grid-MIBEL%20%2F%20OMIE%20%2F%20REN-red?style=flat-square)]()

Production-grade MILP trading pipeline for the **Alqueva hybrid plant** operating in the Iberian electricity market (MIBEL / OMIE).

### Plant

| Asset | Specification |
|-------|--------------|
| **PSP: Pumped Storage** | 4 × 129.6 MW reversible Francis units, 518.4 MW generation / 446.4 MW pumping |
| **PV: Floating Solar** | 5 MWp, commissioned 2022, temperature derate + annual degradation model |
| **BESS: Battery** | 1 MW / 2 MWh, SOC 10–95 %, η_charge = η_discharge = 0.90 |
| **Upper Reservoir** | Alqueva, 3,150 hm³ usable, head range 54.7–73.0 m |
| **Lower Reservoir** | Pedrógão, 54 hm³ usable, binding constraint on long pumping sequences |

### 15-Phase Pipeline

| Phase | Gate | Scope |
|-------|------|-------|
| **1: DA** | OMIE D-1 12:00 | H1–H24 energy bids |
| **2A: IDA1** | OMIE SIDC D-1 15:00 | Position delta re-optimisation, H1–H24 |
| **2B: IDA2** | OMIE SIDC D-1 22:00 | Position delta, H3–H24 |
| **2C: IDA3** | OMIE SIDC D 10:00 | Position delta, H12–H24 (H1–H11 frozen) |
| **2D: XBID** | SIDC continuous H-1 | Cross-border continuous intraday |
| **3A: aFRR** | PICASSO DA+1h | Symmetric ±MW capacity, FAT 5 min |
| **3B: mFRR** | MARI DA+1h | Symmetric ±MW capacity, FAT 12.5 min |
| **4A: RT Dispatch** | 96 ISPs × 15 min | REN signal simulation |
| **4B: aFRR Activation** | Real-time | TSO activation response |
| **4C: mFRR Activation** | Real-time | TSO activation response |
| **5A: Energy Settlement** | Post-delivery | DA / IDA imbalance reconciliation |
| **5B: Reserve Settlement** | Post-delivery | aFRR / mFRR payment calculation |
| **5C: Imbalance Settlement** | Post-delivery | REN 15-min ISP penalty calculation |
| **5D: Analytics** | End-of-day | KPI report, 5-sheet Excel, 9 figures |

### Architecture Highlights

- **Single shared MILP model**: `core_milp_solver.py` used by all 15 phases; each phase passes its own horizon, frozen variables, and market constraints.
- **`--from-phase` hot-restart**: re-enter at any phase without re-running earlier phases; production-safe for intraday gate re-optimisation
- **ComponentStore**: typed dataclass store (GateResults, DispatchPlan, SettlementSheet) shared across phases; zero file I/O between phases
- **13-invariant physical checker**: re-derives dispatch from solved schedule; checks mode exclusivity, min stable load, ramp rates, reservoir bounds, BESS SoC, energy balance, no-double-sell, FAT deliverability; raises `BidCheckError` on any violation before propagation
- **ML forecasting pipeline**: DA price, aFRR, mFRR, PV power, water inflow forecasters each auto-select best model (Naive / Ridge / LightGBM) via 4-fold walk-forward CV; 17 engineered features for DA price (lag 24h/48h/168h/336h, rolling mean/std, cyclical calendar)
- **Risk analytics**: historical VaR (95%/99%) and CVaR/Expected Shortfall; Monte Carlo bootstrap (n=10,000 resamples); annualised Sharpe ratio; max drawdown; P&L attribution by stream
- **Immutable audit trail**: append-only JSON-lines log of every decision (solve / check / approve / submit) with market-time timestamps; designed for regulatory inspection
- **CPLEX 22.1 primary / HiGHS fallback**: automatic solver detection; same model runs on any machine
- **15-min ISP resolution**: 96 intervals/day matching REN grid operator standard (Mar 2025 regulatory)

---

## 🛠️ Technical Skills

| Area | Detail |
|------|--------|
| **Optimisation** | MILP formulation, Pyomo, IBM CPLEX, HiGHS, CBC, unit commitment, piecewise-linear turbine/pump curves, McCormick linearization, 24-hour scheduling horizon |
| **Energy Markets** | OMIE DA/IDA, SIDC IDA1/2/3 (post-Jun 2024 reform), aFRR via PICASSO (FAT 5 min), mFRR via MARI (FAT 12.5 min, live 27 Nov 2024), XBID continuous intraday, ISP imbalance settlement (15-min from 19 Mar 2025), FCR non-remunerated headroom reservation |
| **Risk & P&L** | VaR & CVaR: historical simulation + Monte Carlo bootstrap (n=10,000), confidence intervals, Sharpe ratio (annualised), max drawdown, P&L attribution by stream, pre-trade risk checks, audit logging |
| **ML & Forecasting** | LightGBM, Ridge regression, Naive baseline, walk-forward CV (4 folds), lag/rolling/cyclical calendar features, DA price, aFRR, mFRR, PV power, inflow forecasters |
| **Programming** | Python, pandas, NumPy, Pyomo, scikit-learn, LightGBM, openpyxl, SQLite, Git/GitHub, YAML config, CLI design, pytest |
| **Systems & Data** | OMIE live API, PICASSO/MARI/REN structured data, ENTSO-E market frameworks, ERA5 reanalysis (PV weather), SQLite position/reserve/delivery/audit stores, Excel report generation |
| **Asset Knowledge** | Pumped-storage hydropower (Francis reversible units), floating solar PV, BESS (SoC tracking, cycle degradation), reservoir dynamics (upper/lower bounds, natural inflow), head-dependent efficiency curves |

---

## 💼 Professional Experience

### Energy Optimisation Engineer (PostDoc Researcher)
**INESC TEC, Centre for Power and Energy Systems (CPES), Porto, Portugal**, *Feb 2025 – Present*

*STOR-HY (Horizon Europe GA 101172905), Alqueva Hybrid Plant: 4 × 129.6 MW reversible Francis PSP + 5 MWp Floating PV + 1 MW / 2 MWh BESS*

- Built a 14-gate end-to-end automated bidding and scheduling pipeline covering DA, IDA1/2/3, XBID, aFRR, mFRR, ISP dispatch simulation, activations, settlement, and daily analytics: all orchestrated from a single `run_production.py` with full audit logging; IDA bids are position deltas (post-June-2024 MIBEL reform); IDA3 restricted to hours 12–24
- ML forecasting pipeline: DA price, aFRR, mFRR, PV power, and water inflow forecasters each auto-select best model (Naive / Ridge / LightGBM) via 4-fold walk-forward CV; 17 engineered features for DA price (lag 24h/48h/168h/336h, rolling mean/std, cyclical calendar encodings)
- Physical plant modelling: piecewise-linear turbine efficiency curves (4 Francis units, 129.6 MW each); pump flow linearized for MILP compatibility; full upper/lower reservoir dynamics with monthly natural inflow; BESS SoC tracking with binary charge/discharge commitment and cycle-weighted degradation cost
- Permanent 13-invariant physical checker: re-derives dispatch from solved schedule before any result propagates: checks mode exclusivity, min stable load, ramp rates, reservoir bounds, BESS SoC, energy balance, no-double-sell, and FAT deliverability; raises `BidCheckError` on any violation
- Risk analytics framework: historical VaR (95%/99%) and CVaR/Expected Shortfall; Monte Carlo bootstrap (n=10,000 resamples); annualised Sharpe ratio and max drawdown; all metrics exported to Excel Risk sheet
- Immutable audit trail: append-only JSON-lines logging every decision with market-time timestamps; designed for regulatory inspection and post-trade accountability
- Participated in consortium technical meetings with **EDP Produção, EDP New Energy Technologies, EDF, and GE Vernova** within the STOR-HY Horizon Europe project

---

### Assistant Professor
**GMR Institute of Technology, Rajam, India, Dept. Electrical & Electronics Engineering**, *Jul 2021 – Jan 2025*

Power systems and renewable energy teaching; hybrid energy systems research.

---

### PhD Research Scholar
**IIT Roorkee, Dept. of Hydro and Renewable Energy**, *Jul 2018 – Jul 2021*

- Designed and optimized hybrid renewable energy systems (PV, wind, biomass, BESS) for rural electrification in India
- Applied metaheuristic optimization in MATLAB to minimize LCC and LCOE across multiple battery technologies and dispatch strategies
- Published complete optimization code on MathWorks File Exchange (open-source, reproducible research)

---

### Assistant Professor
**GMR Institute of Technology, Rajam, India, Dept. Electrical & Electronics Engineering**, *May 2013 – Jun 2018*

Power systems and electrical engineering teaching; early research in smart grids and hybrid microgrids.

---

## 🎓 Education

| Degree | Institution | Year |
|--------|-------------|------|
| **Ph.D.**: Renewable Energy | IIT Roorkee, India | 2018 – 2021 |
| **M.E.**: Power Electronics Drives & Control | Andhra University, India | 2010 – 2012 |
| **B.Tech**: Electrical & Electronics Engineering | JNTU Kakinada, India | 2006 – 2010 |

---

## 🤝 Industrial Collaborations & Funded Projects

**STOR-HY**, Horizon Europe GA 101172905, 2025–Present  
Partners: EDP Produção, EDP New Energy Technologies, EDF, GE Vernova  
*Built core MILP optimisation system for the Alqueva hybrid plant*

**SE-HYDRO**, Horizon Europe GA 101269565, Started May 2026  
16-partner consortium: NTUA (coordinator), ANDRITZ HYDRO, EDP, GE Vernova, PPC Greece, Smart Innovation Norway  
*Co-authored successful Horizon Europe grant proposal; contributing to AI-based energy management and digital twin frameworks for hydro pilot sites in Greece, France, Portugal and Serbia*

---

## 📚 Research Impact

[![Publications](https://img.shields.io/badge/Publications-70%2B-blue?style=flat-square)]()
[![H-Index](https://img.shields.io/badge/H--Index-22-green?style=flat-square)]()
[![Citations](https://img.shields.io/badge/Citations-1%2C500%2B-orange?style=flat-square)]()

[Google Scholar Profile →](https://scholar.google.com/citations?user=8EFqCyAAAAAJ)

---

*All code is production-grade Python: modular, typed, config-driven, and built to industrial trading desk standards.*  
**Available from July 2026, EU Work Authorization, Porto, Portugal**

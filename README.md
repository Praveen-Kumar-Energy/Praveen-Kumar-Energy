![Header](https://capsule-render.vercel.app/api?type=waving&color=0:1a1a2e,30:16213e,60:0f3460,100:533483&height=260&section=header&text=Dr.%20Praveen%20Kumar&fontSize=52&fontColor=ffffff&fontAlignY=38&fontAlign=50&desc=⚡%20Energy%20Asset%20Optimisation%20%20|%20%20MILP%20Dispatch%20%20|%20%20Iberian%20Power%20Markets&descSize=17&descAlignY=58&descAlign=50&animation=fadeIn&stroke=ffffff&strokeWidth=1)

<br/>

<p align="center">
  <a href="https://linkedin.com/in/polamarasetty-praveen-kumar-2a3a422a1">
    <img src="https://img.shields.io/badge/LinkedIn-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white"/>
  </a>
  &nbsp;
  <a href="mailto:praveenindia.p@gmail.com">
    <img src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white"/>
  </a>
  &nbsp;
  <a href="https://scholar.google.com/citations?user=8EFqCyAAAAAJ">
    <img src="https://img.shields.io/badge/Google%20Scholar-4285F4?style=for-the-badge&logo=google-scholar&logoColor=white"/>
  </a>
  &nbsp;
  <a href="https://in.mathworks.com/matlabcentral/fileexchange/117260-optimization-of-off-grid-microgrid-with-different-batteries">
    <img src="https://img.shields.io/badge/MathWorks-FF6600?style=for-the-badge&logo=mathworks&logoColor=white"/>
  </a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/📍%20Porto%2C%20Portugal-555?style=flat-square"/>
  &nbsp;
  <img src="https://img.shields.io/badge/🟢%20Available-July%202026-2E7D32?style=flat-square"/>
  &nbsp;
  <img src="https://img.shields.io/badge/🇪🇺%20EU%20Work%20Authorization-003399?style=flat-square"/>
</p>

<br/>

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=500&size=22&pause=1200&color=58A6FF&center=true&vCenter=true&repeat=true&width=650&height=45&lines=Energy+Trading+Engineer;MILP+Optimisation+%7C+IBM+CPLEX;DA+%2F+IDA+%2F+XBID+%2F+aFRR+%2F+mFRR+Pipeline;Iberian+Power+Markets+%E2%80%94+MIBEL+%2F+OMIE;Risk+Analytics+%7C+VaR+%2F+CVaR+%2F+Monte+Carlo;70%2B+Publications+%7C+H-Index+23+%7C+1%2C538+Citations"/>
</p>

<br/>

---

## 👤 About Me

> *Energy systems researcher and industrial-grade software engineer with deep expertise in hybrid plant optimisation, multi-market bidding and scheduling, and MILP-based dispatch.*

Built a production-grade **14-gate multi-market MILP bidding and scheduling system** — DA, IDA1/2/3, XBID, aFRR, mFRR, ISP dispatch simulation, settlement, and analytics — for the real **Alqueva hybrid plant** (518.4 MW PSP + 5 MWp PV + 1 MW/2 MWh BESS, Portugal / MIBEL). System uses IBM CPLEX, auto-selects ML forecasters via walk-forward CV, and applies a permanent **13-invariant physical checker** that blocks any bid with a constraint violation before it propagates. Risk framework includes historical VaR/CVaR and Monte Carlo bootstrap confidence intervals.

---

## ⚡ Flagship Project: Alqueva 24-Hour Energy Trading Optimizer

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/IBM%20CPLEX-1D3557?style=for-the-badge&logo=ibm&logoColor=white"/>
  <img src="https://img.shields.io/badge/MILP-Optimisation-FF6B35?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/HiGHS%20%7C%20CBC-Fallback-4CAF50?style=for-the-badge"/>
  <br/><br/>
  <img src="https://img.shields.io/badge/DA%20%7C%20IDA1--3-Markets-7B2FBE?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/XBID-Continuous-9C27B0?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/aFRR%20%7C%20mFRR-Ancillary-6A0DAD?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/MIBEL%20%7C%20OMIE%20%7C%20REN-Grid-C62828?style=for-the-badge"/>
</p>

<br/>

<table align="center">
<tr>
<td align="center" width="50%">

### 🏭 Plant

| Asset | Specification |
|:------|:-------------|
| **PSP** | 4 × 129.6 MW Francis units, 518.4 MW gen / 446.4 MW pump |
| **PV** | 5 MWp floating solar, commissioned 2022 |
| **BESS** | 1 MW / 2 MWh, SOC 10–95 % |
| **Upper Res.** | Alqueva, 3,150 hm³ |
| **Lower Res.** | Pedrógão, 54 hm³ |

</td>
<td align="center" width="50%">

### 🏗️ Architecture

| Principle | Detail |
|:----------|:-------|
| **Core solver** | Single shared MILP model, all 15 phases |
| **Hot-restart** | `--from-phase` re-entry at any gate |
| **Data layer** | ComponentStore, zero inter-phase file I/O |
| **Safety** | 13-invariant physical checker pre-propagation |
| **Forecasting** | Naive / Ridge / LightGBM via walk-forward CV |
| **Risk** | VaR, CVaR, Monte Carlo bootstrap |
| **Audit** | Immutable JSON-lines, market-time timestamps |
| **Solver fallback** | CPLEX primary, HiGHS / CBC auto-detected |

</td>
</tr>
</table>

<br/>

### 🔄 15-Phase Pipeline

<div align="center">

| Phase | Gate | Scope |
|:-----:|:-----|:------|
| **1** | OMIE DA &nbsp; D-1 12:00 | Day-ahead energy bids, H1–H24 |
| **2A** | OMIE SIDC &nbsp; D-1 15:00 | IDA1 position delta re-optimisation |
| **2B** | OMIE SIDC &nbsp; D-1 22:00 | IDA2 position delta re-optimisation |
| **2C** | OMIE SIDC &nbsp; D 10:00 | IDA3 position delta re-optimisation |
| **2D** | SIDC continuous &nbsp; H-1 | XBID cross-border intraday |
| **3A** | PICASSO &nbsp; DA+1h | aFRR symmetric ±MW capacity |
| **3B** | MARI &nbsp; DA+1h | mFRR symmetric ±MW capacity |
| **4A** | 96 ISPs × 15 min | Real-time dispatch simulation |
| **4B** | Real-time | aFRR TSO activation response |
| **4C** | Real-time | mFRR TSO activation response |
| **5A** | Post-delivery | DA / IDA energy settlement |
| **5B** | Post-delivery | aFRR / mFRR reserve settlement |
| **5C** | Post-delivery | REN ISP imbalance settlement |
| **5D** | End-of-day | KPI report, 5-sheet Excel, 9 figures |

</div>

---

## 🛠️ Technical Skills

<p align="center">
  <img src="https://skillicons.dev/icons?i=python,matlab,git,github,vscode,sqlite&theme=dark&perline=6"/>
</p>

<br/>

<div align="center">

| Area | Skills |
|:-----|:-------|
| **Optimisation** | MILP formulation, Pyomo, IBM CPLEX, HiGHS, CBC, unit commitment, piecewise-linear curves, McCormick linearization |
| **Energy Markets** | OMIE DA/IDA, SIDC IDA1/2/3 (post-Jun 2024), aFRR via PICASSO, mFRR via MARI, XBID continuous, ISP imbalance, FCR headroom |
| **Risk & Analytics** | VaR & CVaR, Monte Carlo bootstrap, Sharpe ratio, max drawdown, P&L attribution, pre-trade risk checks, audit logging |
| **ML & Forecasting** | LightGBM, Ridge regression, Naive baseline, walk-forward CV, lag/rolling/cyclical calendar features |
| **Programming** | Python, pandas, NumPy, Pyomo, scikit-learn, LightGBM, openpyxl, SQLite, YAML config, pytest |
| **Data & Systems** | OMIE live API, PICASSO/MARI/REN data, ENTSO-E frameworks, ERA5 reanalysis, Excel report generation |
| **Asset Knowledge** | PSP Francis units, floating PV, BESS SoC/degradation, reservoir dynamics, head-dependent efficiency |

</div>

---

## 📊 GitHub Stats

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=Praveen-Energy-Trading&show_icons=true&theme=tokyonight&hide_border=true&count_private=true&bg_color=0d1117&title_color=58a6ff&icon_color=58a6ff&text_color=c9d1d9" height="170"/>
  &nbsp;&nbsp;
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Praveen-Energy-Trading&layout=compact&theme=tokyonight&hide_border=true&bg_color=0d1117&title_color=58a6ff&text_color=c9d1d9" height="170"/>
</p>

<p align="center">
  <img src="https://github-readme-activity-graph.vercel.app/graph?username=Praveen-Energy-Trading&theme=tokyo-night&hide_border=true&area=true&bg_color=0d1117&color=58a6ff&line=58a6ff&point=ffffff" width="95%"/>
</p>

<p align="center">
  <img src="https://github-profile-trophy.vercel.app/?username=Praveen-Energy-Trading&theme=tokyonight&no-frame=true&margin-w=10&column=6&no-bg=true"/>
</p>

---

## 💼 Professional Experience

### 🔬 Energy Optimisation Engineer — PostDoc Researcher
**INESC TEC, Centre for Power and Energy Systems (CPES)** &nbsp; `Porto, Portugal` &nbsp; `Feb 2025 – Present`

*STOR-HY · Horizon Europe GA 101172905 · Alqueva Hybrid Plant: 4 × 129.6 MW PSP + 5 MWp PV + 1 MW/2 MWh BESS*

- Built a 14-gate end-to-end automated bidding and scheduling pipeline covering DA, IDA1/2/3, XBID, aFRR, mFRR, ISP dispatch simulation, activations, settlement, and daily analytics; orchestrated from `run_production.py` with full audit logging; IDA bids are position deltas (post-June-2024 MIBEL reform)
- ML forecasting: DA price, aFRR, mFRR, PV power, and water inflow forecasters auto-select best model (Naive / Ridge / LightGBM) via 4-fold walk-forward CV with lag, rolling, and cyclical calendar features
- Physical plant modelling: piecewise-linear turbine efficiency curves; full upper/lower reservoir dynamics with monthly natural inflow; BESS SoC tracking with charge/discharge commitment
- Permanent 13-invariant physical checker: re-derives dispatch from solved schedule before propagation; checks mode exclusivity, ramp rates, reservoir bounds, BESS SoC, energy balance, and FAT deliverability
- Risk analytics: historical VaR (95%/99%) and CVaR/Expected Shortfall; Monte Carlo bootstrap; annualised Sharpe ratio and max drawdown
- Immutable audit trail: append-only JSON-lines log of every decision with market-time timestamps; designed for regulatory inspection
- Participated in consortium meetings with **EDP Produção, EDP New Energy Technologies, EDF, and GE Vernova**

---

### 🎓 Assistant Professor
**GMR Institute of Technology, Rajam, India** &nbsp; `Jul 2021 – Jan 2025`

Power systems and renewable energy teaching; hybrid energy systems research.

---

### 🔬 PhD Research Scholar
**IIT Roorkee, Dept. of Hydro and Renewable Energy** &nbsp; `Jul 2018 – Jul 2021`

- Designed and optimized hybrid renewable energy systems (PV, wind, biomass, BESS) for rural electrification in India
- Applied metaheuristic optimization in MATLAB to minimize LCC and LCOE across multiple battery technologies and dispatch strategies
- Published complete optimization code on MathWorks File Exchange (open-source, reproducible research)

**PhD Code (MATLAB):** [Optimization of Off-Grid Microgrid with Different Batteries](https://in.mathworks.com/matlabcentral/fileexchange/117260-optimization-of-off-grid-microgrid-with-different-batteries) &nbsp; `MathWorks File Exchange` &nbsp; `MATLAB R2018a–R2022a`

---

### 🎓 Assistant Professor
**GMR Institute of Technology, Rajam, India** &nbsp; `May 2013 – Jun 2018`

Power systems and electrical engineering teaching; early research in smart grids and hybrid microgrids.

---

## 🎓 Education

<div align="center">

| Degree | Institution | Year |
|:------:|:------------|:----:|
| **Ph.D.** in Renewable Energy | IIT Roorkee, India | 2018 – 2021 |
| **M.E.** in Power Electronics Drives & Control | Andhra University, India | 2010 – 2012 |
| **B.Tech** in Electrical & Electronics Engineering | JNTU Kakinada, India | 2006 – 2010 |

</div>

---

## 🤝 Industrial Collaborations

<table align="center">
<tr>
<td width="50%" valign="top">

### STOR-HY
`Horizon Europe GA 101172905` `2025–Present`

**Partners:** EDP Produção, EDP New Energy Technologies, EDF, GE Vernova

Built core MILP optimisation system for the Alqueva hybrid plant

</td>
<td width="50%" valign="top">

### SE-HYDRO
`Horizon Europe GA 101269565` `May 2026–`

**Consortium (16 partners):** NTUA, ANDRITZ HYDRO, EDP, GE Vernova, PPC Greece, Smart Innovation Norway

Co-authored grant proposal; AI-based energy management and digital twin frameworks for hydro pilot sites across Europe

</td>
</tr>
</table>

---

## 📚 Research Impact

<p align="center">
  <img src="https://img.shields.io/badge/Publications-70%2B-1565C0?style=for-the-badge&logo=bookstack&logoColor=white"/>
  &nbsp;
  <img src="https://img.shields.io/badge/H--Index-23-2E7D32?style=for-the-badge&logo=google-scholar&logoColor=white"/>
  &nbsp;
  <img src="https://img.shields.io/badge/Citations-1%2C538-E65100?style=for-the-badge&logo=google-scholar&logoColor=white"/>
</p>

<p align="center">
  <a href="https://scholar.google.com/citations?user=8EFqCyAAAAAJ">
    <img src="https://img.shields.io/badge/View%20Full%20Google%20Scholar%20Profile-4285F4?style=for-the-badge&logo=google-scholar&logoColor=white"/>
  </a>
</p>

<br/>

<p align="center">
  <i>All code is production-grade Python: modular, typed, config-driven, and built to industrial trading desk standards.</i>
  <br/><br/>
  <b>📍 Porto, Portugal &nbsp;|&nbsp; 🟢 Available July 2026 &nbsp;|&nbsp; 🇪🇺 EU Work Authorization</b>
</p>

![Footer](https://capsule-render.vercel.app/api?type=waving&color=0:533483,40:0f3460,70:16213e,100:1a1a2e&height=140&section=footer)

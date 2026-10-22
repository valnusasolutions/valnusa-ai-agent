# VALNUSA AI Agent — Prototype v1.0

**Industrial Maintenance & Reliability Intelligence Platform — demonstration prototype**

> **VALNUSA** — *Value of Nusantara* · **Powered by Excellence**
>
> ⚠️ **This is a demonstration prototype built entirely on simulated data.** No sensor, PLC, SCADA, MQTT broker or control system is connected. Nothing in this app can start, stop or modify real equipment. AI output is decision support requiring qualified human review.

---

## 1. What this is

A complete, mobile-first single-page application demonstrating the full industrial reliability journey:

**Asset registry → sensor data → monitoring → anomaly detection → AI-assisted analysis → maintenance recommendation → work order → reliability dashboard**, plus a lightweight industrial CRM.

Built with **HTML5 + CSS3 + vanilla JavaScript** only. No framework, no build step, no backend, no API keys.

| Item | Value |
|---|---|
| Version | Prototype v1.0 |
| Deployment | Static files (GitHub Pages, Netlify, any web host) |
| Storage | Browser `localStorage` (demo records) — no server |
| Charts | Hand-built SVG renderer (no external chart library, works offline) |
| Demo fleet | 17 assets · 6 sites · 6 industries · 6 customers |
| Ind. sectors supported | 10 configured sectors (data model is industry-agnostic) |

---

## 2. Quick start (2 minutes)

### Option A — run locally, no hosting
1. Download `source/` (or the single `index.html`).
2. Double-click `index.html` — it opens in any modern browser, including on a phone.
   *(For the single-file build, no other files are needed.)*

### Option B — deploy to GitHub Pages (recommended for a shareable demo link)

**From an Android phone (no PC required):**

1. Install the **GitHub** mobile app (or open `github.com` in Chrome).
2. Create a new **public** repository, e.g. `valnusa-ai-agent`.
3. Upload the contents of the `source/` folder so the repository root contains:
   ```
   index.html
   assets/css/styles.css
   assets/js/data.js … app.js
   ```
   (Or upload only the single-file `index.html` — it works on its own.)
4. In the repository open **Settings → Pages**.
5. Under **Build and deployment → Source** choose **Deploy from a branch**, branch **main**, folder **/ (root)**, then **Save**.
6. Wait 1–2 minutes. Your demo link appears as:
   `https://<your-username>.github.io/valnusa-ai-agent/`
7. Open the link in Chrome on Android → menu **⋮ → Add to Home screen** for an app-like launch.

### Option C — Netlify Drop
Open `app.netlify.com/drop` on any device and drag the `source` folder onto the page. You get an instant HTTPS demo URL.

**Requirements:** any modern browser (Chrome 90+, Safari 14+, Edge 90+). No installation, no login.

---

## 3. Modules

| # | Module | What it does |
|---|---|---|
| 1 | **Overview** | 6 KPI cards, equipment health gauge, status distribution, downtime exposure & savings opportunity, active alarms, highest-risk assets, industry portfolio, maintenance activity |
| 2 | **Asset Monitoring** | 17 assets with live status (Normal / Warning / Critical / Offline), search + status + industry filters, compact asset cards with sensor readings and sparklines |
| 3 | **Asset Detail** | Full asset record: customer, process, strategy, runtime, MTBF/MTTR, availability; all sensor readings with limits; interactive trend chart per sensor with warning/critical lines; alarm history; maintenance history; linked work orders |
| 4 | **AI Intelligence** | Fleet-wide rules-based assessment: risk score /10, measured findings with trend direction, possible failure modes (hypotheses), prioritised recommended actions, per-asset and fleet reports |
| 5 | **Maintenance** | Work orders (Open → Assigned → In Progress → Completed → Verified), PM schedule, maintenance history + RCA template, MTBF / MTTR / availability / downtime KPIs |
| 6 | **IoT Simulator** | Start / Pause / Reset, adjustable 1–5 s interval, per-asset condition forcing (Natural / Normal / Warning / Critical), timestamped event log, live reading ticker |
| 7 | **CRM** | 6 industrial accounts with full profiles, 7-stage opportunity pipeline board, weighted forecast, follow-up activity list, opportunity creation and stage changes |
| 8 | **Reports** | 7 previewable reports with CSV export and print-to-PDF |
| 9 | **AI Assistant** | Floating chat assistant (rules-based, works on live app data) — prioritisation, asset explanations, checklists, proposals, CRM priorities |

### Sensor library & thresholds

| Sensor | Unit | Trigger | Warning | Critical |
|---|---|---|---|---|
| Vibration | mm/s | above | 4.5 | 7.1 |
| Temperature | °C | above | 75 | 95 (overridable per asset, e.g. kiln 260/320) |
| Pressure | bar | above | 16 | 19 |
| Flow rate | m³/h | below | 85% of baseline | 70% of baseline |
| Motor current | A | above | 112% of baseline | 125% of baseline |
| Power | kW | above | 110% | 122% |
| Speed | rpm | both | ±6–10% | ±12–20% |
| Level | % | below | 35 | 20 |
| Voltage | kV | both | 30.5 / 34.5 | 29 / 36 |
| Differential pressure | kPa | above | 180 | 240 |

Thresholds are visible in **Settings → Configured Thresholds** and can be overridden per asset (`th` property in `data.js`).

---

## 4. Suggested demo walkthrough (covers every acceptance criterion)

1. **Overview** – note the simulated-data badges, KPI cards, health gauge, alarms and risk ranking.
2. **Asset Monitoring** – filter by *Critical*, search `P-101`, open the asset card.
3. **Asset Detail (P-101)** – read the sensor panel, switch trending sensors, view the warning lines on the chart, read the AI analysis, then press **Generate maintenance report**.
4. **AI Intelligence** – filter by risk level, open a report, press **Fleet report**.
5. **Maintenance** – press **+ Work Order**, create one from a template, open it, advance it through the status flow.
6. **IoT Simulator** – press **Start**, force `P-102` to **Critical**, watch the alarm, overview KPIs and AI risk update; press **Reset**.
7. **CRM** – open an opportunity, move its stage, create a new opportunity, open a customer profile.
8. **Reports** – preview each report, export CSV, print / save as PDF.
9. **AI Assistant** – tap the ✦ button, ask “Which assets require immediate attention?” or “Why is P-101 showing a warning?”.
10. **Settings** – review thresholds, export demo data as JSON, reset the demo.

---

## 5. Project structure

```
source/
├── index.html                  # app shell, navigation, assistant panel
└── assets/
    ├── css/styles.css          # full design system (mobile-first, responsive)
    └── js/
        ├── data.js             # demo data: customers, assets, sensors, CRM, work orders,
        │                       #   failure-mode knowledge base, report catalogue
        ├── engine.js           # state, telemetry simulation, thresholds, rule engine,
        │                       #   alarms, KPIs, reliability calculations, persistence
        ├── ui.js               # shared UI: SVG charts, gauge, modal, toast, pills
        ├── views-core.js       # Overview, Monitoring, Asset detail, AI Intelligence
        ├── views-ops.js        # Maintenance, Simulator, CRM, Reports, Settings
        ├── assistant.js        # rules-based assistant (intent matching over live data)
        └── app.js              # hash router, event delegation, actions, boot
```

**Single-file build:** `index.html` at the project root is the same application with CSS and JS inlined — deploy that one file if you want the absolute simplest setup.

### Data model (relationships)

```
Customer (C1…C6) ──┬── Site ── Process
                   ├── Assets (17) ──┬── Sensors (per-equipment tag set)
                   │                 ├── Telemetry readings (120-point history per tag)
                   │                 ├── Alarms (raised / cleared)
                   │                 ├── Maintenance history
                   │                 └── Work orders
                   └── Opportunities ── Follow-up activities
```

Every asset carries: ID, name, category, manufacturer, model, customer, site, industry, process, criticality (A/B/C), operating status, sensor configuration, maintenance strategy, install date, runtime, thresholds and baseline values.

---

## 6. Safety, security and honest limits

**By design:**
- All telemetry is generated in the browser and labelled **SIMULATED DATA** throughout the interface.
- Possible failure causes are always presented as **hypotheses**, clearly separated from measured values and from technician verification.
- No control actions exist: the app cannot start, stop or change equipment.
- No credentials, API keys or backend endpoints. Nothing is transmitted anywhere.

**Limitations of v1.0:**
- Data does not persist to a server (browser `localStorage` only, per device).
- No authentication or multi-user roles.
- The "AI" is a deterministic rule engine (thresholds + trend analysis + failure-mode library), **not** a live LLM.
- Reliability figures (MTBF/MTTR/availability) are demo calculations, not audited plant history.
- Cost, savings and downtime-exposure figures use placeholder Indonesian rupiah rates for illustration only.
- Single plant-level context; no multi-tenant isolation.

---

## 7. Roadmap

| Phase | Scope |
|---|---|
| **1 — Prototype v1.0 (this build)** | Responsive UI, simulated telemetry, asset monitoring, rule-based anomaly detection, AI assistant simulation, maintenance flow, CRM, reports, static deployment |
| **2 — MVP v1.1** | Authentication + roles, PostgreSQL/Supabase persistence, full CRUD for customers/assets, real LLM API integration (server-side), Excel/Sheets import-export, richer reporting |
| **3 — IoT Pilot v2.0** | Sensor + gateway integration, MQTT/HTTP ingestion, time-series storage, push/e-mail alerts, historical analytics, customer-specific dashboards |
| **4 — Commercial Platform** | Multi-tenant architecture, RBAC, reliability analytics, maintenance optimisation, SLA/service management, subscription or project commercial model |

### Migration path (how to move off the prototype)

1. **Frontend** – the view layer is isolated in `views-*.js`; each view returns HTML from a state object. Porting to React/Vue means converting each view into a component and keeping `engine.js` logic as a service module.
2. **Backend** – replace `VN.state` + `localStorage` with API calls; the data shapes in `data.js` map directly to PostgreSQL tables (`customers`, `sites`, `assets`, `sensors`, `readings`, `alarms`, `work_orders`, `opportunities`, `follow_ups`).
3. **Telemetry** – replace `VN.tick()` with an MQTT/HTTP subscriber writing to a time-series table; keep `evaluateAll()` as the alarm evaluation step.
4. **AI** – swap `analyse()` for a server-side LLM call; keep the current rules engine as the deterministic pre-filter and always label hypotheses vs measured data.
5. **Security** — put the LLM and database behind a server (never expose keys in the frontend), add authentication, and follow OT/IT segmentation guidance before any plant connection.

---

## 8. Branding

- Product: **VALNUSA AI Agent**, Prototype v1.0
- Meaning: **VALNUSA — Value of Nusantara**
- Tagline: **Powered by Excellence**
- Business line: Industrial Maintenance & Reliability Solutions
- Palette: dark navy navigation `#0c1a26`, teal brand `#0f766e`, status green `#16a34a` / amber `#d97706` / red `#dc2626`, light surfaces `#f4f7fa`

VALNUSA is presented as an independent industrial solutions brand.

---

© VALNUSA — demonstration prototype. All plant data shown is simulated.

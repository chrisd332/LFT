# Lupus Flare Tracker & Early Warning Engine 

> A client-side predictive health dashboard designed to correlate latent environmental, dietary, and mechanical stress triggers with Systemic Lupus Erythematosus (SLE) disease activity.

[![Live Demo](https://img.shields.io/badge/Live_Demo-GitHub_Pages-5C4879?style=for-the-badge)](https://<your-username>.github.io/lupus-flare-tracker/)
[![License: MIT](https://img.shields.io/badge/License-MIT-4A3962?style=for-the-badge)](LICENSE)
[![Stack: Vanilla JS / Tailwind / Plotly](https://img.shields.io/badge/Stack-Vanilla_JS_%7C_Tailwind_%7C_Plotly-725C93?style=for-the-badge)](#technical-architecture)

---

## Executive Summary

Systemic Lupus Erythematosus (SLE) flares rarely present instantaneously; they are frequently precipitated by delayed physiological responses to ambient UV radiation, barometric pressure instability, high-impact mechanical strain, and inflammatory dietary markers. 

Existing tracking solutions suffer from two critical pain points:
1. **Patient Logging Fatigue:** Burdensome 20+ question surveys that patients abandon during acute flare episodes.
2. **Clinical Data Overload:** Unstructured, multi-page diary logs that rheumatologists cannot parse within a standard 15-minute appointment.

This project addresses both challenges by combining a **sub-minute 5-question micro-log**, **automated geocoded weather ingestion**, and a **time-lagged cross-correlation engine ($T-1$ to $T-3$ days)** that generates an exportable, one-page clinical summary mapped directly to rheumatological evaluation standards.

---

## Key Features

* **5-Question Rapid Check-In:** Designed specifically for accessibility during flare episodes (VAS pain scale, fatigue level, sleep duration, flare onset flag, and date).
* **Automated Environmental Enrichment:** Background ingestion of hourly UV Index and barometric pressure fluctuations ($\Delta P$) via the Open-Meteo REST API using natural language City/State geocoding.
* **Full-Spectrum Nutritional Biomarkers:** Natural-language parsing of daily meals estimating rolling 30-day means for:
  * Sodium ($< 2,000\text{ mg}$ renal target)
  * Dietary Cholesterol ($< 200\text{ mg}$ cardiovascular target)
  * Saturated Fat, Added Sugars, Dietary Fiber, and Potassium.
* **Mechanical Exertion & Strain Tracking:** Captures physical intensity and joint overexertion markers.
* **Time-Lagged Predictive Correlation Matrix:** Evaluates 24-, 48-, and 72-hour latent intervals ($T-1$, $T-2$, $T-3$) using Pearson correlation coefficients to uncover hidden, delayed flare triggers.
* **48-Hour Acute Vulnerability Index:** Real-time composite risk gauge alerting patients to upcoming environmental and lifestyle vulnerability windows.
* **Rheumatologist 1-Page Summary Brief:** A print-optimized (`Ctrl+P` / `Cmd+P`) appointment brief featuring 30-day biomarker scorecards, high-confidence triggers, and a 14-day chronological log with physician sign-off lines.

---

## Technical Architecture

This application was engineered as a zero-dependency, client-side web application to guarantee cross-platform reliability, immediate responsiveness, and zero data leakage:

* **Data Layer:** Browser-persistent local storage simulating a relational schema across daily symptoms, environmental metrics, and dietary/exercise logs.
* **Frontend Design System:** Tailwind CSS configured with a muted amethyst/slate-mauve clinical color palette, geometric square architecture, and layered elevation shadows.
* **Visualization Layer:** Plotly.js for interactive multivariate time-series overlays and dynamic correlation heatmaps.
* **External APIs:** Open-Meteo Geocoding & Weather APIs (CORS-friendly, no API key required).

---

## Analytical Methodology

Autoimmune flares exhibit time latency. The application calculates rolling Pearson correlation coefficients ($r$) across variable time offsets:

$$r = \frac{\sum_{i=1}^{n} (X_{i - \text{lag}} - \bar{X})(Y_i - \bar{Y})}{\sqrt{\sum_{i=1}^{n} (X_{i - \text{lag}} - \bar{X})^2 \sum_{i=1}^{n} (Y_i - \bar{Y})^2}}$$

Where:
* $X_{i - \text{lag}}$ represents candidate exposures (Max UV, Barometric Delta, Strenuous Activity, High Sodium) at lag offsets of 1, 2, or 3 days prior.
* $Y_i$ represents the acute patient-reported Visual Analog Scale (VAS) pain score on day $i$.

---

## Local Quickstart

Because this platform requires no compilation or backend server, running it locally takes seconds:

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/](https://github.com/)<your-username>/lupus-flare-tracker.git
   cd lupus-flare-tracker
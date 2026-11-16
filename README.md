# EthanolCalc — Ethanol Blend Calculator

A scientific fuel-blend instrument with a BMW E92 335is-style analog cluster dial.

**Live:** https://interrupt-l-l-c.github.io/EthanolCalc/

## What it does

- Computes exact volumes of high-ethanol fuel (e.g. E85) and base petrol needed to reach a target ethanol %, from the fuel currently in the tank to a chosen **fill-to** volume — Full · ¾ · ½ · ¼ · Custom (default Full tank).
- Optional **fill cost**: enter base and high-fuel prices (any currency) to see what the fill costs — you pay only for what you add.
- Estimates AKI and RON from configurable fuel anchors (linear model — estimates, not lab measurements).
- Works with **any petrol tank capacity**, in US gallons or liters (1 US gal = 3.785411784 L, exact).
- Advanced **ethanol target table** with CSV export (collapsed by default, alongside the fuel-model and fill-cost panels).

## The gauge

The dial emulates the E92 instrument cluster: chrome bezel, black face, white needle, amber illumination.

- **20 divisions** — the five major marks read **E, ¼, ½, ¾, F**; minor ticks are unlabeled.
- Adjustable in **0.5 steps** (41 marks total). Each division = 1/20 of the tank = 5%.
- Inner amber scale shows tank percent (0/25/50/75/100), mirroring the dual-scale BMW layout.
- Drag the dial, use the slider, tap ±0.5, use the E/¼/½/¾/F presets, or use arrow keys (Home/End, PageUp/PageDown).

## Accuracy

- Pure calculation core, independent of the UI, implementing the volume-balance equations with a 1e-7 validity tolerance.
- A **21-check calibration self-test runs on every page load** (golden examples, error states, unit round-trips, gauge geometry, fill-to/cost cases, and a 126-case mass-balance/feasibility property sweep). If any check fails, results are disabled and a CAL fault is shown.
- Impossible blends are rejected with explicit physical error states that report the reachable ethanol bound (target out of range, tank full, fill-to below current fuel, current fuel already too strong) instead of returning nonsense numbers.

## Usage notes

- Single static HTML file, no dependencies, no network calls — works offline once loaded.
- Inputs persist in your browser (localStorage); nothing is sent anywhere.
- Octane figures are estimates. Verify critical blends with a fuel sample or ethanol sensor before running them.

## Deployment

This repo is the public deploy artifact only. Source and planning live in a private repo; updates are pushed here via its `scripts/deploy-web.sh`, and GitHub Pages serves `index.html` from `main`.

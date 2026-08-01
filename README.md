# Star Citizen 4.9 Mining & Ship Configuration Console

![Star Citizen Banner](https://img.shields.io/badge/Star%20Citizen-Alpha%204.9-orange?style=flat-square&logo=robertsspaceindustries)
![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=flat-square&logo=python)
![HTML5/JS](https://img.shields.io/badge/Frontend-HTML5%20%2F%20JS-green?style=flat-square&logo=html5)
![License](https://img.shields.io/badge/License-MIT-lightgrey?style=flat-square)

An advanced, offline-capable unified console and tactical suite designed for **Star Citizen Alpha 4.9**. This toolkit integrates real-time telemetry analysis, an RS signature scanner, resource location mapping, rock composition breakdown, modular ship customization, and an economic crafting calculator into a single, high-performance interface.

---

## 🌟 Key Features

### 1. RS Signature Scanner & Telemetry
* **Radar & Cross-Section Analysis:** Simulated threat and target scanning based on cross-section (CS), electromagnetic (EM), and infrared (IR) signatures.
* **Component Emission Tuning:** Real-time tracking of power plant output, cooler efficiency, and shield generation bleed.

### 2. Resource Locator & Planet Mapping
* **Stanton System Database:** Comprehensive data on planetary bodies, moons, asteroid belts, and Lagrange points (Hurston, Crusader, microTech, ArcCorp).
* **Yield Probability Grids:** Filter locations by mineral rarity (Quantanium, Bexalite, Taranite, Gold, Laranite, etc.).

### 3. Rock Composition & Fracture Analysis
* **Instability & Resistance Metrics:** Input rock mass, fracture resistance, and instability thresholds.
* **Optimal Laser Head Selector:** Recommends optimal mining heads (Lancet, Arbor, Helix) and module combinations (Torrent, Surge, Stampede) to prevent catastrophic overcharges.

### 4. Modular Ship Customizer
* **Loadout Simulation:** Configure weapons, shields, power plants, quantum drives, and coolers across multi-crew and single-seat industrial/combat hulls (MOLE, Prospector, Constellation, Corsair, etc.).
* **Power & Heat Balancing:** Instantly calculates total power draw vs. generation capacity.

### 5. Crafting & Refining Calculator
* **Refinery Yield Estimator:** Calculate expected output and profit margins across various refining methods (Dinyx Solation, Cinch, Thermochemical).
* **Component Crafting Cost Analysis:** Track raw material requirements versus market resale values.

---

## 📁 Project Structure

```text
sc-4.9-console/
├── index.html              # Main unified web console interface
├── css/
│   └── styles.css          # Sci-fi HUD styling (RSI / Aegis inspired dark theme)
├── js/
│   ├── scanner.js          # RS signature and telemetry logic
│   ├── mining.js           # Rock fracture & resource calculation models
│   ├── shipconfig.js       # Ship loadout and power grid simulation
│   └── ui.js               # Interactive dashboard controllers
├── data/
│   ├── minerals.json       # Alpha 4.9 mining yield and stability data
│   ├── ships.json          # Hull specifications, hardpoints, and power pools
│   └── locations.json      # Stanton system planetary & belt coordinates
├── README.md               # Project documentation
└── LICENSE                 # MIT License

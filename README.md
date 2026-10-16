<div align="center">

# ☕ Cafno

### Precision Caffeine Half-Life & Sleep Clearance Tracker

[![Flutter](https://img.shields.io/badge/Flutter-%2302569B.svg?style=for-the-badge&logo=Flutter&logoColor=white)](https://flutter.dev/)
[![Dart](https://img.shields.io/badge/dart-%230175C2.svg?style=for-the-badge&logo=dart&logoColor=white)](https://dart.dev/)
[![License: Custom](https://img.shields.io/badge/License-Proprietary%20%2F%20Custom-orange.svg?style=for-the-badge)](LICENSE)

<p align="center">
  <b>Ever wondered if that 4:00 PM cold brew is going to ruin your sleep tonight?</b><br>
  Cafno models real-time pharmacokinetic caffeine decay to project active stimulation levels straight to your bedtime.
</p>

</div>

---

## 🌟 The Purpose

Most health apps treat caffeine as a static daily counter—alerting you once you hit 400 mg, but ignoring when you drank it. In reality, caffeine doesn't instantly leave your body; its biological half-life averages **5.0 hours**. A late-afternoon espresso can still leave significant active stimulant in your bloodstream at midnight, blocking adenosine receptors and sabotaging deep (REM) sleep.

**Cafno** solves this by:
1. **Modeling Multi-Dose Exponential Decay** so you know the exact active caffeine in your body right now.
2. **Projecting Levels to Your Exact Bedtime** to answer the critical question: *"Can I have another cup without wrecking my sleep?"*
3. **Offering an Interactive 24-Hour Scrub Curve** to inspect future clearance hour by hour.
4. **Providing a Distraction-Free, Industrial UI** designed in warm roasted orange and deep espresso black with zero bloat or forced accounts.

---

## ✨ Key Features

| Feature | Description |
| :--- | :--- |
| ⚡ **Pharmacokinetic Half-Life Engine** | Stacks and calculates exponential clearance ($t_{1/2} = 5.0\text{h}$) across all drinks logged throughout the day. |
| 📈 **Interactive 24-Hour Scrub Chart** | Touch or drag along the curve to view pinned crosshairs, exact time offsets, and remaining active milligrams ($y$-value). |
| 🛌 **Dedicated Bedtime Target System** | Set your target sleep time with an interactive time pill; get live countdowns and projected bedtime caffeine levels. |
| 🛡️ **Smart Collision-Free Timeline** | Custom bounding-box painter dynamically prevents timeline marks (`Now`, `Bed`, `+6h`, etc.) from ever overlapping. |
| ☕ **Hybrid Manual & Preset Logging** | Single-tap chips for common drinks (Espresso, Cold Brew, Drip, Energy Drink) paired with direct numeric keyboard typing and steppers. |
| ✏️ **Full Intake Management** | Edit logged entries, adjust fluid ounces (`oz`) or caffeine (`mg`), or swipe left to dismiss and delete. |
| 🔒 **100% Offline & Private** | Starts on a clean slate with zero dummy data. All logs and bedtime preferences stay on your device via encrypted JSON. |

---

## 🏗️ How It Works (Technical Architecture)

Cafno operates entirely on-device without external backend APIs, driving all calculations through local pharmacokinetic models and custom hardware-accelerated canvas rendering:

### 1. Pharmacokinetic Exponential Decay Formula
Caffeine clearance follows first-order elimination kinetics. For each drink $i$ with initial caffeine $C_i$ consumed at timestamp $T_i$, the active load at target time $t$ ($t \ge T_i$) is computed as:

$$C_{\text{active}}(t) = \sum_{i, T_i \le t} C_i \times \left(0.5\right)^{\frac{t - T_i}{5.0\text{ hours}}}$$

### 2. High-Performance Canvas Plotting (`CustomPainter`)
Instead of heavy charting libraries, Cafno uses a lightweight `InteractiveDecayChartPainter` that:
* Samples 96 discrete timeline steps across a rolling 24-hour viewport ($-4\text{h}$ past to $+20\text{h}$ future).
* Fills a subtle vertical alpha gradient under the decay path using the brand's roasted orange palette (`#DE6418`).
* Plots horizontal guide marks at physiological thresholds ($50\text{ mg}$ and $100\text{ mg}$).

### 3. Collision-Free Timeline Layout
Dynamic milestone labels (`Now`, `Bed`) and relative interval ticks (`-4h`, `+6h`, `+12h`, `+18h`) are evaluated through an internal bounding-box resolver (`canPlace()`). If a secondary reference tick falls within 10 horizontal pixels of your bedtime marker, it is automatically suppressed to ensure crisp typography on any screen width.

---

## 🛌 Sleep Readiness Thresholds

Cafno maps bedtime caffeine loads into three actionable physiological states:

| Status | Threshold | Physiological Impact |
| :---: | :---: | :--- |
| 🟢 **SAFE** | $\le 40\text{ mg}$ | Minimal adenosine receptor blockade. System is clear for natural melatonin release and deep REM cycles. |
| 🟡 **CAUTION** | $41 - 100\text{ mg}$ | Active stimulant remaining. May prolong sleep latency (time to fall asleep) and reduce slow-wave sleep. |
| 🔴 **ELEVATED** | $> 100\text{ mg}$ | High physiological stimulation. Sleep architecture will be noticeably impaired; late caffeine intake is strongly discouraged. |

---

## 📦 Dependencies

Cafno is built to be ultra-lean with minimal external package bloat:

* **[flutter](https://flutter.dev/)** — Core UI SDK and CustomPaint rendering pipeline.
* **[shared_preferences](https://pub.dev/packages/shared_preferences)** — Persistent on-device JSON storage for intake history and bedtime configuration.

---

## 🚀 Getting Started

### Installation & Run

**Download The APK for Android no IOS install CURRENTLY**
### 🤝 Contributing
Contributions, issues, and feature requests are welcome!
Feel free to open an issue or submit a pull request if you want to help make Cafno even better.

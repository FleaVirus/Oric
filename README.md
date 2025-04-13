# Oric
Oric: Harmonic trading platform aiming to be the "Twitter of Trading" with 100M users, $15B–$40B valuation. Built for Qubic’s Aigarth AI &amp; blockchain.


# 🎛️ QFPM Quantum Framework v2.07 (Apr 2025) | Build Hash: 0xA1E4F
# 👨‍💻 Maintainers:
# ├─ Lead Dev: @FleaVirus

# -*- coding: utf-8 -*-

## 📦 Chapter 1 Table of Contents:
────────────────────────────────

📘 1.0 Introduction & System Architecture  
 ├─ 1.1 🔎 System Overview  
 │   └─ Two-part architecture: TradingView signal bot + Python execution engine  
 │
 ├─ 1.2 ⚙️ Key Features  
 │   ├─ Webhook endpoint, SL/TP, trailing logic  
 │   ├─ Reentry engine, strategy modes, config override  
 │   ├─ Hotkey controls, live chart UI, REST status endpoint  
 │   └─ Sync loop via `update_positions()`  
 │
 ├─ 1.3 🎛️ Strategy Mode Profiles  
 │   ├─ Mode options: normal, build, sentry, swing, scalp  
 │   ├─ Controls DCA, risk, SL/TP, macro filters, killzones  
 │   └─ Defined per-symbol via `SYMBOL_CONFIG["mode"]`  
 │
 ├─ 1.4 🧬 Signal Processing Flow  
 │   ├─ INIT → SIGNAL → MACRO CHECK  
 │   ├─ KILLZONE OVERRIDE → POSITION EVAL  
 │   ├─ RISK ORDER DEPLOY (SL/TP/TTP)  
 │   └─ MONITOR LOOP → ROI triggers, reentries, exits  
 │
 ├─ 1.5 📌 System Cross-Reference Map  
 │   ├─ `process_signal()` → Chapter 5.4  
 │   ├─ `execute_market_order()` → Chapter 6.4  
 │   ├─ `execute_risk_orders()` → Chapter 6.5  
 │   ├─ `update_positions()` → Chapter 6.5  
 │   └─ `SYMBOL_CONFIG` / `apply_mode_overrides()` → Chapter 2  
 │
 ├─ 1.6 🚀 Deployment Guide  
 │   ├─ Setup: clone, install, run  
 │   ├─ TradingView webhook: `POST /webhook`  
 │   ├─ Signal format: `{ "symbol": "...", "type": "buy" }`  
 │   └─ REST status: `GET /status`  
 │
 ├─ 1.7 🛠️ Maintainer Notes  
 │   ├─ Fully modular and config-driven  
 │   ├─ Designed for thread-safe multi-instance use  
 │   ├─ GUI support (Tkinter, pywebview)  
 │   └─ Prepared for future split: `/core`, `/risk`, `/ui`, `/exchange`  
 │
 └─ 1.8 ⚠️ Disclaimer  
     ├─ API credentials are your responsibility  
     ├─ Live trading = real risk  
     └─ Validate your strategy and config before use

📦 1.9 Product Evolution Summary  
 └─ Cloud-native upgrades, dashboard UI, and GPT AI agent roadmap

📘 Chapter 2: Core & Strategy Configuration  
 ├─ 2.1 🧰 Environment & Imports  
 ├─ 2.2 🧬 SYMBOL_CONFIG Core Dictionary  
 ├─ 2.2.1 🔍 Symbol Access Utilities  
 ├─ 2.3 🧭 Enumerated Strategy Types  
 ├─ 2.4 🎛️ STRATEGY_MODES — Harmonic Behavior Blueprints  
 ├─ 2.5 🌀 Harmonic Overrides & Volatility Adapters  
 ├─ 2.6 🔁 apply_mode_overrides() — Core Strategy Switchboard  
 ├─ 2.7 📊 Runtime State Trackers  
 └─ 2.8 🚀 Initialization Summary  

📘 Chapter 3: Exchange Connectivity (Gate.io)  
 ├─ 3.1 🤖 API Client Boot  
 ├─ 3.2 ⏱️ Clock Sync & Time Offset  
 ├─ 3.3 📦 Order Type Definitions  
 └─ 3.4 🧪 Exchange Runtime Helpers *(Optional)*  

📘 Chapter 4: Market Data & Trade Sizing Engine  
 ├─ 4.1 🔎 Live Position, Asset, and Market Data  
 ├─ 4.2 🧠 Behavior Sync Helpers  
 ├─ 4.3 🧮 Trade Size Engine  
 └─ 4.4 🌀 Quantum Harmonizer (Fibonacci Engine)  

📘 Chapter 5: Webhook Signal Framework  
 ├─ 5.1 🔌 Flask Webhook Server  
 ├─ 5.2 🔐 Payload Validator  
 ├─ 5.3 📡 Signal Endpoints  
 ├─ 5.4 🧠 Signal Routing & Execution  
 └─ 5.5 🪪 Live Symbol Snapshot  

📘 Chapter 6: Overview & Lifecycle  
 ├─ 6.1 🧮 Precision & Risk Math  
 ├─ 6.2 🧠 Risk Logic & Calculators  
 ├─ 6.3 🧬 Position Lifecycle Manager  
 ├─ 6.4 ⚡ Order & Execution Engine  
 ├─ 6.5 🔁 Position Monitoring & Refresh  
 └─ 6.6 🧿 Resonance-Aware Signal Execution  

📘 Chapter 7: Advanced Features  
 ├─ 7.1 🔁 Position Lifecycle & Refresh  
 ├─ 7.2 🎼 Fibonacci Band Resonance  
 ├─ 7.3 📊 Market Mood Engine  
 ├─ 7.4 🧬 Mode-Resonance Behavior Modulation  
 ├─ 7.5 🖥️ Runtime Console Overlay (Live HUD)  
 └─ 7.6 🧠 (Optional) Mood Score Generator  

📘 Chapter 8: Manual Control Console  
 └─ 8.0 ⌨️ Hotkey Binds  

📘 Chapter 9: System Integrity & Safety Checks  
 ├─ 9.0 🛑 Safe Termination  
 └─ 9.1 🧪 Flask Instance Validator  

📘 Chapter 10: Strategy UI & Visualization  
 ├─ 10.0 🎛️ Control Panel + Embedded TradingView  
 └─ 10.1 📈 Order Journal & Export  

📘 Chapter 11: Bot Boot Sequence & Runtime Loop  
 ├─ 11.0 🔧 State Bootstrap  
 ├─ 11.1 ⚙️ Startup Hooks  
 └─ 11.2 🌐 Flask Server Launch  

────────────────────────────────

## 📘 Chapter 1: Introduction & System Architecture

### 🧬 Quantum Multi-Timeframe Execution Engine (QFPM)
A precision-grade trading system designed for real-time signal parsing, macro-filtered execution, and harmonic-aligned risk deployment. Built for speed, tuned for frequency, and prepared for AI-assisted orchestration.

“This isn’t just a trading bot—it’s a synchronized market instrument, poised to dominate as the ‘Twitter of Trading.’”

#### 📦 1.0 Executive Overview
*Oric*—named after Orichalcum, the forgotten metal of Atlantis—is a harmonic trading platform that blends ancient wisdom (Fibonacci zones, Solfeggio frequencies) with cutting-edge technology (multi-timeframe analysis, dynamic scaling, AI integration). Our vision is to become the “Twitter of Trading,” scaling to 100M users and achieving a $15B–$40B valuation by revolutionizing how traders interact with markets. Currently valued at $13M–$28M (acquisition potential: $40M–$70M), *Oric* has proven its market fit in volatile conditions (e.g., $4.8T market surge, $NQ +12.1% gain, per X posts on April 10, 2025) and aligns with pro-crypto trends (e.g., SEC’s $ETH ETF options approval).

We’re applying to Qubic’s Incubation Program to integrate *Oric* with your Aigarth AI and scalable blockchain, creating a decentralized, AI-driven trading powerhouse. By leveraging Qubic’s infrastructure, *Oric* will enable on-chain trading, harness your mining hardware for real-time, high-frequency execution, and drive massive user adoption—positioning Qubic as the go-to blockchain for traders globally.

- **Ambitious Scale:** Designed to handle 100M users with a modular, cloud-native architecture deployable on AWS, GCP, or Vercel.
- **Revenue Potential:** Tiered SaaS model (Bronze to Orichalcum) generates $999–$14,999/month + 10–35 bps performance fees, with private licenses at $500K–$1.25M and white-label deals at $400K–$1.25M upfront + 40–60% revenue share.
- **Market Leadership:** *Oric* on Qubic will redefine trading, combining harmonic resonance with AI-driven insights to capture the crypto trading market, aligning with blockchain/stablecoin trends (e.g., Treasury Sec. Bessent’s focus, per X posts).

#### ✅ 🔧 1.1 System Modules (Augmented, Juicy & Iconic)
- **🛰️ Signal Generation Layer (TradingView + Webhook Alerts):**  
  Powered by Pine Script strategies across multi-timeframes (LTF/MTF/HTF), emitting real-time buy/sell/macro alerts via webhook. Anchored to Fibonacci frequency zones (417Hz–961Hz), aware of killzones (Asia/EU/NY sessions), and supports mode switching (normal, build, sentry, swing, scalp, hype), ROI bands, and bias filters. Payloads include type, symbol, mode, note, killzone, and alignment for precise execution.

- **⚙️ Execution Engine (Python QFPM Core):**  
  The central nervous system that routes, filters, and executes signals. The main control loop (`process_signal()`) accepts TradingView signals and manual overrides, managing the full position lifecycle (open, scale, reverse, close). It integrates ROI gates, double-down logic, and SL/TP deployers, dynamically scaling based on contract size, balance, and config. Supports thread-safe, multi-instance use for massive scalability.

- **🧬 Position Fusion (4D Scaling Engine):**  
  A proprietary scaling system that choreographs positions across four dimensions (price, time, risk, resonance). It adapts to market conditions using LTF/MTF/HTF layers, ensuring optimal scaling (e.g., scale-in during pullbacks, scale-out on Fib resonance). This engine enables *Oric* to handle high-frequency trading at scale, leveraging Qubic’s mining hardware for real-time execution.

- **⚡ "Catch the Move" Scaling Engine:**  
  An advanced scaling mechanism that dynamically morphs strategies based on market momentum and Fib resonance. For example, it can shift from scalp to build mode on swing detection, capturing 5–10% moves with precision. This feature maximizes ROI in volatile markets (e.g., $NQ +12.1% surge) and makes *Oric* ideal for Qubic’s high-performance infrastructure.

- **🎯 Risk Module (Smart SL/TP/TTP Deployers):**  
  Modular risk logic for every trade, with `calculate_stop_loss_price()` and `calculate_take_profit_price()` ensuring precision. Trailing TP (TTP) logic is gated by ROI thresholds, using ReduceOnly or Trailing-Stop orders. Re-validates mark prices to prevent invalid setups and cancels stale SL/TP on refresh (`cancel_all_reduce_only_orders()`).

- **🧮 Trade Sizing Engine (DQA Adaptive Contracts):**  
  Position sizing adjusts dynamically based on market alignment and confidence. `calculate_contracts()` factors in base risk and leverage, while `calculate_quantum_contracts()` uses an AI-ready sizing engine, scaling by DQA score, macro match, and ROI volatility. Compliant with exchange specs (e.g., Gate.io step size, precision), with HTF alignment overrides for boosted confidence.

- **📡 Webhook API Interface (Flask-Driven):**  
  Real-time intake from TradingView alerts and local tools via `/webhook` (JSON endpoint) and `/status` (symbol state, config, last signal). Applies macro bias and killzone overrides, stateless for deployment on AWS Lambda, GCP Cloud Function, or Vercel, ensuring scalability for 100M users.

- **🎛️ Mode Engine (Harmonic Behavior Logic):**  
  Humanizes trading with six modes (normal, build, sentry, swing, scalp, hype), each adjusting risk %, SL/TP activation, trailing ROI thresholds, and reentry caps. Modes align to Fibonacci frequency bands (e.g., 528Hz for swing), enhancing trader intuition and market resonance.

- **🌀 Harmonic Resonance Layer (Quantum Harmonizer):**  
  Combines market geometry with signal modulation. `scan_fib_levels()` and `check_resonance_match()` map prices to Fib zones (e.g., 0.382, 0.618), outputting resonance scores for risk suppression, confidence overlays, and signal gating. Maps to Solfeggio frequencies for UI feedback, creating an immersive trading experience.

- **💼 Class-Based Tier System (Revenue-Generating):**  
  *Oric* operates on a tiered SaaS model, scaling functionality and revenue:  
  - **Bronze (Bot):** Basic single-symbol execution for beginners.  
  - **Silver (Strategy):** Adds strategy modes and session awareness.  
  - **Gold (Multi-symbol Sync):** Enables multi-symbol trading with QFH Fib overlays.  
  - **Platina (Adaptive Logic):** Integrates LTF/MTF/HTF layers for adaptive scaling.  
  - **Orichalcum (GPT-Harmonic Learning AI):** Leverages Qubic’s Aigarth AI for on-chain signal ranking, mode suggestions, and journaling.  
  Pricing ranges from $999–$14,999/month + 10–35 bps fees, with private licenses at $500K–$1.25M, ensuring significant revenue for Qubic.

#### 📦 1.2 Potential Impact on Qubic Ecosystem
- **Revenue Stream:** *Oric’s* tiered SaaS model and white-label offerings generate millions for Qubic’s dev team, with $999–$14,999/month subscriptions, 10–35 bps fees, and $400K–$1.25M white-label deals (40–60% revenue share).
- **User Growth:** Attracts traders to Qubic, increasing network activity and QUBIC token demand (e.g., cross-promotion with QUBIC holders on Gate.io).
- **Market Leadership:** Positions Qubic as the go-to blockchain for AI-driven trading, aligning with pro-crypto trends (e.g., blockchain/stablecoin focus, SEC’s $ETH ETF options approval, per X posts on April 10, 2025).
- **Hardware Utilization:** *Oric’s* scaling engines (Position Fusion, "Catch the Move") leverage Qubic’s mining hardware (used for Monero) for real-time, high-frequency trading, maximizing ROI on your infrastructure.

*Further details (e.g., technical implementation, deployment guide, roadmap) available upon request after initial review.*

#### ⚠️ 1.3 Licensing and Usage
*Oric* is a proprietary project. All rights reserved. Access to this repository is granted solely for the purpose of review by Qubic.org as part of the Incubation Program application. No part of this project may be used, copied, or distributed without explicit written permission from the creator (@FleaVirus).

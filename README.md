# Paper-Alpha

<p align="center">
    <img src="./assets/banner.png" alt="Paper-Alpha Banner">
    <br />
    <br />
    <img src="https://img.shields.io/badge/License-AGPL_v3-blue?style=for-the-badge" alt="License">
    <img src="https://img.shields.io/badge/Rust-black?style=for-the-badge&logo=rust&logoColor=white" alt="Rust">
    <img src="https://img.shields.io/badge/Tauri-24C8D8?style=for-the-badge&logo=tauri&logoColor=white" alt="Tauri">
    <img src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React">
    <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript">
    <img src="https://img.shields.io/badge/WebAssembly-654FF0?style=for-the-badge&logo=webassembly&logoColor=white" alt="WebAssembly">
    <br />
    <br />
    <i>A privacy-first, modular quantitative trading and market analysis workstation.</i>
</p>

> [!NOTE]
> **Active Development:** This project is currently a work in progress and is being actively built.

## Abstract

Paper-Alpha is an extensible, privacy-first quantitative trading and market analysis workstation. Designed for algorithmic traders, quantitative researchers, and market analysts, it provides a flexible environment that unifies real-time charting, order execution, trade simulation, and customizable analytical dashboards into a cohesive desktop workspace. Operating entirely on local hardware with zero external cloud dependencies, Paper-Alpha guarantees that proprietary trading strategies, sensitive financial credentials, and bespoke models remain strictly private and under the user's sole custody.

## Objective

To empower quantitative traders with a modular, zero-telemetry trading workstation where analytical tools, custom market data feeds, and execution engines can be seamlessly composed without cloud lock-in or proprietary platform constraints. Paper-Alpha aims to bridge the gap between high-level visual analysis and reliable order execution, providing a transparent, local-first foundation for strategy development, backtesting, and active market monitoring.

## Features

### Functional
- **Modular Canvas Workspaces**: Drag-and-drop customizable layout grids across dedicated Analysis, Execution, and Monitoring tabs.
- **Extensible Plugin Ecosystem**: Support for Data Feed, Data Process (Logic), and Broker execution plugins.
- **Local Security & Credentials Vault**: Encrypted credential storage with master password protection, single-use backup recovery codes, and emergency phrase recovery.
- **Visual Customization**: Configurable workspace themes, Tailwind color palettes, and interface presets.
- **Data & Execution Scoping**: Tab-based widget bounds keeping market analysis and trade execution workflows focused.

### Non-Functional
- **Local-First & Privacy-Focused**: Zero telemetry, tracking, or mandatory cloud connectivity. All keys and data remain on local hardware.
- **High-Performance Architecture**: Microkernel core built with Rust and Tauri for minimal memory footprint and fast startup times.
- **Plugin Sandboxing**: Isolated WebAssembly guest execution and local IPC sidecar subprocesses (gRPC/UDS).
- **Style Confinement**: Web Component Shadow DOM isolation to prevent stylesheet collisions across third-party widgets.
- **Frame-Rate Optimized UI**: Efficient rendering pipeline utilizing browser animation loops to keep dashboards responsive under data updates.

## Prerequisites

### Requirements
- **Operating System**: Linux or Windows (10/11 64-bit).
- **Webview Engine**:
  - **Linux**: `WebKitGTK` (`libwebkit2gtk-4.1` / `libwebkit2gtk-4.0`).
  - **Windows**: Microsoft Edge `WebView2` Runtime.
- **Hardware Prerequisites**: 64-bit x86_64 or ARM64 processor, minimum 4 GB RAM (8 GB+ recommended for multi-stream analytics), and local disk storage for SQLCipher encrypted database files.

### Dependencies
- **Rust Toolchain**: Rust 1.75+ (Cargo package manager).
- **Desktop Runtime**: Tauri v2 (`@tauri-apps/cli`).
- **Frontend Stack**: Node.js (v18+) and package manager (`pnpm` / `npm`) with React and Vite.
- **IPC Protocol Compiler**: `protoc` (Protocol Buffers compiler) for compiling gRPC interfaces (`tonic` / `prost`).

## Getting Started

Installation and usage guidelines are documented in [`docs/begin.md`](./docs/begin.md).
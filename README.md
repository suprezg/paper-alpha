# Paper-Alpha

<p align="center">
    <img src="./assets/banner.png" alt="Paper-Alpha Banner">
    <br />
    <br />
    <img src="https://img.shields.io/badge/License-AGPL_v3-blue?style=for-the-badge" alt="License">
    <img src="https://img.shields.io/badge/Rust-black?style=for-the-badge&logo=rust&logoColor=white" alt="Rust">
    <img src="https://img.shields.io/badge/Slint-237346?style=for-the-badge&logoColor=white" alt="Slint Native GUI">
    <img src="https://img.shields.io/badge/Plotters-orange?style=for-the-badge" alt="Plotters GPU/CPU">
    <img src="https://img.shields.io/badge/WebAssembly-654FF0?style=for-the-badge&logo=webassembly&logoColor=white" alt="WebAssembly">
    <img src="https://img.shields.io/badge/gRPC-244F5D?style=for-the-badge&logo=google&logoColor=white" alt="gRPC / Protobuf">
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
- **Dynamic Persistent Workspace Tabs**: Browser-style tab creation via a plus icon (`+`) allowing users to spawn unlimited independent workspaces, configure per-tab widget layouts from the right-side selection panel, and persist the entire workspace layout across sessions and re-logins.
- **Two Main Plugin Pillars**: High-performance extensible architecture supporting **Data Feed Plugins** (declaring streaming vs. non-streaming emissions) and **Data Consumer Plugins** (declaring required input consumptions for quantitative calculation, charting, and execution).
- **Local Security & Credentials Vault**: Encrypted credential storage with master password protection (Argon2id + AES-256-GCM pinned in non-swappable RAM via `mlock`), single-use emergency backup recovery codes, and 12-word mnemonic phrase recovery managed by `AuthenticationService`.
- **Visual Customization**: Configurable workspace themes, design token adjustments, and native Slint interface styling presets.
- **Zero-Trust Governance & Policy Enforcement**: Real-time manifest compliance monitoring via `PluginPolicyEnforcer` working alongside `RouterService` to ensure Data Feed plugins marked as streaming cannot access the Slow Speed Bus or alter undeclared variables, while Data Consumer plugins only read declared topics, never emit data, and cannot call other plugins directly.

### Non-Functional
- **Local-First & Privacy-Focused**: Zero telemetry, tracking, or mandatory cloud connectivity. All keys, databases, and trade history remain on local hardware.
- **High-Performance Architecture**: Single-process Microkernel core built with pure Rust and the Slint native retained-mode GUI DSL, eliminating webview overhead, DOM bloat, and IPC serialization between the core and UI.
- **Plugin Sandboxing**: Isolated WebAssembly guest execution (Wasmtime with zero-copy C-FFI byte passing) and native local IPC sidecar subprocesses (Tonic gRPC over Unix Domain Sockets or Windows Named Pipes).
- **Declarative Schema UI Confinement**: Secure Declarative Widget Schema parsing where plugins declare JSON UI component trees (Cards, Tiles, Plotters charts, Action Forms) strictly instantiated into native Slint components, completely preventing arbitrary third-party code from executing in the GUI layer.
- **Frame-Rate Optimized Native Graphics**: Direct GPU/CPU-accelerated rendering utilizing Slint (Skia / WGPU) and direct Plotters pixel buffers at 60 FPS, with reference-counted topic hibernation (`TopicRefCounter`) to sleep inactive tabs.

## Prerequisites

### Requirements
- **Operating System**: Linux (x86_64, aarch64), Windows (10/11 64-bit), or macOS.
- **Native Graphics Backends**: Modern GPU graphics drivers supporting OpenGL, Vulkan, or direct framebuffer rendering (Skia and WGPU backends for Slint). Webview engines and browser runtimes are entirely eliminated.
- **Hardware Prerequisites**: 64-bit x86_64 or ARM64 processor, minimum 4 GB RAM (8 GB+ recommended for multi-stream quantitative analytics), and local disk storage for SQLCipher encrypted database files.

### Dependencies
- **Rust Toolchain**: Rust 1.75+ (Cargo package manager).
- **Slint GUI & Graphics**: `slint` native UI toolkit, `slint-build`, and `plotters` charting engine.
- **Encrypted Database Engine**: `SQLCipher` with SQLite3 and `sqlx` in WAL (Write-Ahead Logging) mode.
- **IPC Protocol Compiler**: `protoc` (Protocol Buffers compiler) for compiling gRPC interfaces (`tonic` / `prost`).

## Getting Started

Installation and usage guidelines are documented in [`docs/begin.md`](./docs/begin.md).
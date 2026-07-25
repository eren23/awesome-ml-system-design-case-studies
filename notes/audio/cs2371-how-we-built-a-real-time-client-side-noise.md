---
id: cs2371
title: "How we built a real-time, client-side noise suppression library without server dependencies"
company: Datadog
primary_category: audio
sub_category: audio-classification
year: 2025
source_url: https://www.datadoghq.com/blog/engineering/noise-suppression-library/
tags: [speech-enhancement, noise-suppression, DTLN, LSTM, WebAssembly, real-time, on-device, TensorFlow-Lite]
---

# How we built a real-time, client-side noise suppression library without server dependencies
**Datadog** · 2025 · [source](https://www.datadoghq.com/blog/engineering/noise-suppression-library/)

## Problem
Datadog's CoScreen collaboration tool lacked noise suppression on par with commercial competitors. Existing options were server-dependent (adding latency and cost), too slow for real-time audio on client devices, or hard to integrate with WebRTC — no off-the-shelf library was simultaneously performant, portable, and WebRTC-friendly.

## Approach / System design
The team built dtln-rs, an open-source, client-side noise suppression library based on the Dual-Signal Transformation LSTM Network (DTLN), a deep learning model from the University of Oldenburg. The pipeline applies a short-time Fourier transform to split audio into magnitude and phase, runs two sequential DTLN LSTM models (with an inverse FFT between them) to identify and filter noise, and performs inference through a minimal C interface to TensorFlow Lite. A single Rust codebase targets WebAssembly (via Emscripten, using AudioWorkletProcessor for real-time web audio), Node.js (via NEON native bindings), and native desktop clients.

## Key decisions
- Rust as the core language for cross-platform tooling and Cargo's standardized build system, wrapping a thin C interface to TensorFlow.
- TensorFlow Lite instead of full TensorFlow (1.1 GB minimum) to make client-side embedding feasible.
- Fully client-side processing — no server dependency — eliminating latency, per-minute charges, and infrastructure cost.
- Accepted WebAssembly's larger binary and some performance loss in exchange for consistent deployment across platforms.

## Stack
Rust, TensorFlow Lite, DTLN (LSTM-based model), WebAssembly/Emscripten, NEON (Node.js bindings), AudioWorkletProcessor, WebRTC integration. Open-sourced on GitHub.

## Results
- Processes one second of audio in 33 ms on an M1 MacBook Pro — comfortably real-time.
- The underlying DTLN model placed 8th of 17 teams in Microsoft's Deep Noise Suppression Challenge 2020, with Mean Opinion Score ratings exceeding commercial standards.
- Deployed fully embedded across CoScreen's web and native clients with zero server costs.

## Takeaways
Modern lightweight inference runtimes make research-grade speech enhancement viable entirely on-device. Rust's tooling substantially simplified multi-target deployment versus C++, and deliberate trade-offs (TFLite over TF, Wasm portability over peak speed) were what turned an academic model into a shippable production library — then open-sourcing it made previously commercial-only capability broadly available.

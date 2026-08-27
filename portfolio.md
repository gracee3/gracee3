# Emmy Grace Clark - Selected Technical Projects and Public Research

[← Profile](./README.md) · [Resume](./resume.md)

Washington, DC | emmygraceclark@gmail.com | [github.com/gracee3](https://github.com/gracee3)

**Prepared:** August 2026

## Overview

My public work applies more than 20 years of Linux and open-source systems experience and 15+ years of professional software engineering, infrastructure, compliance, and technical leadership to current problems in local AI inference, speech recognition, model evaluation, hardware-aware optimization, observability, real-time processing, and local-first application design.

The projects below emphasize:

- explicit requirements and architectural boundaries;
- deterministic or reproducible evaluation where the underlying tools permit it;
- accuracy, latency, throughput, memory, and resource measurement;
- pinned models, datasets, dependencies, and evidence identities;
- privacy-preserving local and offline operation;
- failure handling, negative-result preservation, and bounded claims;
- portable deployment on accessible consumer and workstation hardware; and
- public documentation that separates verified results from future work.

## Project Summary

| Project | Focus | Current evidence boundary |
|---|---|---|
| [native-asr](https://github.com/gracee3/native-asr) | CPU-only long-form and streaming ASR | Released v0.1.0; reproducible WER/RTF and real-time loopback acceptance |
| [qwen38-int8-lab](https://github.com/gracee3/qwen38-int8-lab) | Qwen3.8-27B W8A8 quantization and evaluation | Functional dual-RTX-3090 candidate complete; standardized accuracy is a separate gate |
| [whisperX-batch](https://github.com/gracee3/whisperX-batch) | Docker-first GPU transcription and benchmark harness | Active stabilization; fresh LibriSpeech dev/test evaluation in progress |
| [gpt-oss-rs](https://github.com/gracee3/gpt-oss-rs) | Rust-native GPT-OSS inference research | v0.1.0 research program complete; CPU evidence and archived heterogeneous results published |
| [supermicro-observability](https://github.com/gracee3/supermicro-observability) | Secure, high-frequency host and GPU observability | Released baseline with checkout and optional system installation workflows |
| [digital-liquid-light-lab](https://github.com/gracee3/digital-liquid-light-lab) | GPU-first real-time liquid-light simulation and performance instrument | Stage 0 native Rust/`wgpu` platform proof complete; bounded 2.5D mathematical specification in progress |
| [Mirabile](https://github.com/gracee3/mirabile) | Local-first Rust/Leptos CSR/WASM application | Pre-MVP architectural vertical slice with native and browser verification |
| [Magnolia](https://github.com/gracee3/magnolia) | Modular real-time DSP and signal processing | Experimental active research software with working components |

## native-asr

**Repository:** [github.com/gracee3/native-asr](https://github.com/gracee3/native-asr)  
**Role:** Designer, implementer, evaluator, and maintainer  
**Focus:** Accurate offline transcription and real-time captions on ordinary x86-64 Linux laptops

### Problem and approach

Cloud speech services create privacy, connectivity, cost, and reproducibility concerns. `native-asr` explores how far carefully selected native runtimes can be taken on ubiquitous CPU-only hardware while keeping model weights and recordings local.

I designed two complete workflows:

1. A deterministic long-form ensemble that runs NeMo Parakeet TDT v3, Sherpa Parakeet Unified, and whisper.cpp `small.en`, aligns their lexical output, and produces a transparent two-of-three consensus transcript. Three-way disagreements fall back to the declared anchor and remain visible in the audit evidence; no language model silently rewrites the agreed transcript.
2. A streaming cascade that keeps Nemotron and NeMo Parakeet resident. Nemotron emits provisional revisions and phrase endpoints; Parakeet re-decodes each completed phrase and becomes authoritative when it returns within the bounded correction deadline. Timeouts, failures, empty corrections, and queue pressure produce explicit degraded reasons instead of silently blocking or discarding text.

### Engineering contribution

- Built Docker-separated native runtime images for NeMo-Speech.cpp, sherpa-onnx/ONNX Runtime, Moonshine, and whisper.cpp while excluding Python, PyTorch, models, and personal audio from deployed images.
- Enforced read-only model and recording mounts, network-disabled inference, unprivileged users, content-verified downloads, private audit artifacts, and atomic no-overwrite publication.
- Developed model and dataset lockfiles, dispatch wrappers, batch reuse, segmentation and retry policies, benchmark manifests, WER normalization, RTF and resource telemetry, and reproducible public-corpus fixtures.
- Built a Rust terminal UI that enumerates and revalidates an explicit PipeWire source and keeps committed, correction-pending, provisional, and degraded text visually distinct.
- Preserved rejected benchmark attempts and their causes rather than incorporating failed or incomplete measurements into the reported baseline.

### Measured evidence

- Long-form deterministic 100-utterance snapshots: **1.78% WER** on LibriSpeech `test-clean` and **3.28% WER** on `test-other`, improving upon the best constituent in each split.
- Approximate sequential ensemble RTF from constituent measurements: **0.91-1.12** on the historical i7-1185G7 host, before small alignment and audit overhead.
- Real-time PipeWire loopback on an i5-1145G7: **4.35% committed WER** on `test-clean`, **6.17%** on `test-other`, approximately **1.001 RTF**, zero degraded segments, and no more than **142 ms p95** partial latency.
- Earlier unpaced streaming regression runs measured **0.415-0.444 RTF**; they are retained as CPU-pressure evidence rather than substituted for the real-time acceptance path.

These are bounded engineering results on declared fixtures, not universal or state-of-the-art claims.

## qwen38-int8-lab

**Repository:** [github.com/gracee3/qwen38-int8-lab](https://github.com/gracee3/qwen38-int8-lab)  
**Role:** Research lead, quantization-policy designer, infrastructure implementer, and evaluator  
**Target:** High-quality local Qwen3.8-27B inference on two 24 GB RTX 3090 GPUs

### Problem and approach

The official Qwen3.8-27B checkpoint contains conventional attention, Gated DeltaNet/recurrent layers, a vision tower, an untied output head, zero-centered RMSNorm behavior, and top-level MTP tensors not instantiated by the standard Transformers class. Treating every linear layer as equivalent would create correctness and quality risks.

I built an architecture-aware W8A8 lab that:

- quantizes 192 text MLP projections and 64 conventional full-attention Q/K/V/O projections;
- preserves embeddings, the untied `lm_head`, normalization, all recurrent/GDN paths, vision components, and 15 MTP tensors;
- uses calibrated GPTQ with symmetric per-channel INT8 weights and dynamic per-token INT8 activations;
- separates locked quantization and vLLM environments where dependency requirements differ;
- stages output under an incomplete name, validates it, restores omitted assets, and publishes only through an atomic final rename; and
- records process RSS, swap, memory pressure, GPU memory, disk availability, safety interruptions, model/dataset fingerprints, and exact evidence identities.

### Functional candidate evidence

- Completed guarded tiny, 32-sample, and 512-sample calibration gates without retry or safety interruption.
- Produced a self-contained **36.8 GB**, 45-file candidate with complete Safetensors integrity, exactly **256 intended W8A8 targets**, all **15 MTP tensors**, and required processor configuration.
- Loaded the artifact directly in vLLM 0.27.1 with tensor parallelism across both GPUs and observed native `CompressedTensorsW8A8Int8` to `CutlassInt8ScaledMMLinearKernel` dispatch.
- Repeated the same non-thinking request twice with deterministic output containing the correct result `391`.
- Three measured 1,153-prompt-token/128-output-token requests produced medians of **0.608 seconds TTFT**, approximately **1,897 client-observed prefill tokens/second**, and **10.41 decode tokens/second**.

This establishes a functional quality candidate, not a standardized accuracy or deployment recommendation. A separately designed paired accuracy workflow is required before making retention claims; multimodal vision/video behavior also remains outside the completed text-serving boundary.

## whisperX-batch

**Repository:** [github.com/gracee3/whisperX-batch](https://github.com/gracee3/whisperX-batch)  
**Role:** Packaging, orchestration, validation, and benchmark-harness development  
**Focus:** Repeatable long-form GPU transcription and evaluation

`whisperX-batch` packages the operational control plane around upstream WhisperX rather than claiming a new speech model. The current stack uses CUDA 12.8.1, Python 3.11, Torch/torchaudio 2.8.0, CTranslate2 4.7.1, faster-whisper 1.2.1, WhisperX 3.8.2, and pyannote-audio 4.0.4.

Engineering work includes:

- explicit configuration and command precedence;
- one visible GPU and one Docker process per invocation;
- deliberate multi-GPU sharding through independent jobs rather than a hidden scheduler;
- read-only input and model mounts with caches outside the runtime image;
- bounded Docker command construction and file-level resume behavior;
- Cartesian parameter sweeps, WER scoring, throughput/RTF/tokens-per-second reporting, run-level CSV/JSON evidence, and optional `nvidia-smi` traces; and
- an offline standard-library test suite that validates orchestration without requiring Docker, a GPU, models, datasets, audio, or network access.

A fresh LibriSpeech `dev-clean`, `dev-other`, `test-clean`, and `test-other` campaign on dual RTX 3090 hardware is being developed to replace historical observations with publishable, exact-commit WER, RTF, throughput, and resource evidence. Until that campaign completes, the project does not present the older 200-file observation as a reproducible comparative result.

## gpt-oss-rs

**Repository:** [github.com/gracee3/gpt-oss-rs](https://github.com/gracee3/gpt-oss-rs)  
**Role:** Rust inference implementation, kernel and scheduler research, heterogeneous-systems evaluation, and evidence publication  
**Status:** Planned v0.1.0 research program complete; maintenance mode

The project implements bounded native execution of the pinned GPT-OSS 20B checkpoint and publishes methods, measurements, provenance, and negative results together.

Key work includes:

- BF16 dense tensors and compact MXFP4 expert weights;
- scalar, AVX2, AVX-512/VNNI, and capability-selected CPU kernels with a scalar oracle and exact-bit equivalence gates;
- residual-Q8 activations, versioned x8 repacking, atomic derived-cache publication, and read-only cache reopening;
- immutable model state, mutable sequence state, transactional layer-major prompt prefill, and reserve/execute/commit scheduling seams; and
- versioned manifests, hashed evidence, redaction, fixed prompts, controlled benchmarks, paired bootstrap analysis, and negative-result preservation.

The final CPU benchmark verified the official token sequence in every trial. Automatic CPU dispatch achieved a supported **6.05x decode improvement over the scalar path**, while remaining slower than same-host llama.cpp in the declared comparison. Both facts are retained.

Archived accelerator research records a successful bounded GPT-OSS 20B continuation twice with real work assigned across CPU, GPU0, and GPU1. The archive also states clearly that later 120B construction remained unpassed, no 120B execution occurred, and historical layer-sharding work did not establish executable activation or parity.

## supermicro-observability

**Repository:** [github.com/gracee3/supermicro-observability](https://github.com/gracee3/supermicro-observability)  
**Role:** Architect and implementer  
**Focus:** Portable, secure, high-frequency observability for AI workstations and Linux servers

This project translates enterprise monitoring lessons into a public, host-safe stack with a generic core and explicit optional integrations.

- Docker Compose data plane using Prometheus, Grafana, node_exporter, a custom Rust GPU exporter, NVIDIA NVML metrics, one explicitly selected SMART device, cached fan-controller telemetry, and constrained cAdvisor collection.
- Persistent `nvidia-smi --loop-ms=250` sampling keyed internally by GPU UUID, 500 ms GPU scrapes, one-second fast host scrapes, and lower-frequency inventory and storage checks.
- Local-only defaults, generated credentials, read-only filesystems where practical, capability and resource constraints, identity-label removal, bounded retention, and explicit private-link binding.
- Optional system installation that separates versioned application files, private configuration, credentials, and persistent data and leaves the stack disabled by default.
- A bounded JSON observation CLI and local STDIO MCP interface for agents and evaluation harnesses; the interface queries the existing loopback Prometheus endpoint and cannot start or stop monitoring.

The repository began on a Supermicro X11SPA-TF dual-RTX-3090 workstation but deliberately excludes real host, disk, network, GPU, fan-header, and credential identities from committed configuration.

## digital-liquid-light-lab

**Repository:** [github.com/gracee3/digital-liquid-light-lab](https://github.com/gracee3/digital-liquid-light-lab)  
**Role:** Product concept, systems architecture, simulation research, and implementation  
**Status:** Active staged research and development

Digital Liquid Light Lab is a research-oriented, performable digital instrument descended from traditional liquid-light shows. Rather than treating the result as a conventional shader or music visualizer, the project models an illuminated thin-layer world in which liquids, pigments, materials, light, and performer-controlled forces interact in real time.

The system is designed around Rust, `wgpu`, WGSL, and a native Vulkan desktop path, with simulation and rendering kept as explicit architectural layers. The current program advances from a 2D grid-based incompressible solver toward a bounded 2.5D height/thickness model with absorption, refraction, scattering, and caustic-like optics; longer-term 3D particle-grid research remains outside the present implementation boundary.

Current engineering work includes:

- a completed Stage 0 native application and GPU-initialization platform proof;
- a mathematical specification for a saturated thin-gap apparatus before solver implementation;
- explicit fluid, material, optics, interaction, diagnostics, and evidence boundaries;
- performance targets for responsive single-GPU execution on RTX-3090-class hardware; and
- an architecture intended to support projector performance and later gyro, touch, audio, and MIDI control without coupling input devices to the simulation core.

The goal is perceptual physical fidelity and a convincing playable instrument, not scientific-CFD accuracy. The repository distinguishes completed platform evidence, bounded specifications, planned solver work, and longer-term research.

## Mirabile

**Repository:** [github.com/gracee3/mirabile](https://github.com/gracee3/mirabile)  
**Role:** Application and domain-architecture research  
**Status:** Pre-MVP

Mirabile is a local-first astrology workspace written in Rust and Leptos 0.8. It demonstrates modern Rust full-stack and browser engineering through:

- a provider-neutral calculation boundary and exactly pinned engine adapter;
- application-owned domain, provenance, and persistence types;
- revisioned repository contracts with memory, portable JSON, and IndexedDB adapters;
- authoritative application state separated from disposable calculation, analysis, layout, and scene projections;
- Leptos CSR/WASM presentation with calculation in a Web Worker; and
- native tests, strict Clippy, dependency/license checks, Trunk builds, and isolated headless-Chromium verification of IndexedDB, reload, and Worker behavior.

The project explicitly labels its schemas and feature surface as pre-MVP and does not present incomplete calculation or UI coverage as production capability.

## Magnolia

**Repository:** [github.com/gracee3/magnolia](https://github.com/gracee3/magnolia)  
**Role:** Real-time systems and DSP research  
**Status:** Experimental active research

Magnolia explores a modular connectivity layer for signal-processing systems:

- Rust microkernel and patch-bay architecture that decouples sources, processors, and sinks;
- stable C plugin ABI with dynamic loading and hot-reload research;
- lock-free single-producer/single-consumer ring buffers for low-latency audio;
- Linux sandboxing and Ed25519 plugin verification;
- Nannou-based visual host and configurable overlays; and
- local CPU/INT8 streaming captions with a reproducible LibriSpeech baseline harness for WER, first-partial latency, first-final latency, and RTF.

The repository distinguishes working components from intended system boundaries and does not claim that every experimental path is independently hardened.

## What This Work Demonstrates

Across these projects, I independently translate ambiguous technical goals into explicit contracts, implement and integrate software across model, runtime, container, operating-system, hardware, and user-interface layers, and build the evidence needed to evaluate the result honestly. The work combines programming and systems depth with the assessment judgment central to technical question authoring, AI response validation, data-quality review, performance analysis, and expert feedback.

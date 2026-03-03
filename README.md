# Visione

A local-first AI creative production suite for consumer GPUs.

---

## What is Visione?

Visione is a self-contained desktop application for AI-driven creative production. It runs entirely on local hardware — no cloud services, no external APIs, no subscriptions. Every model runs on-device; inference never leaves your machine.

The pipeline covers the full creative arc: text-to-image and video generation, retouching, stylization, enhancement, sound design, and final assembly — all within a single application.

**Stack:** Python 3.12 + FastAPI + SSE · React 18 + TypeScript + Zustand · Tauri 2 desktop shell · ComfyUI headless for video inference · PyTorch 2.7 + CUDA

---

## Components

| Tab | What it does |
|-----|-------------|
| **Imagine** | Image and video generation from text or reference image |
| **Retouch** | Image editing — upscaling, denoising, face restore, multi-reference compositing, LUT, adjustments, background removal |
| **Retexture** | Video style transfer — LoRA-based preset styles and reference-image stylization via depth conditioning |
| **Enhance** | Image and video enhancement — upscaling, denoising, frame interpolation |
| **Storyboard** | 12-stage AI-assisted filmmaking pipeline: multi-agent concept development, character library, shot generation, and export |
| **Sound Studio** | Music generation, voiceover (preset, cloned, and voice-designed), and video-to-audio foley |
| **Video Editor** | Lightweight timeline for assembling clips, audio, and exports |
| **Characters** | Persistent character library with 5-shot reference generation for cross-shot consistency |
| **Gallery** | Unified asset browser across all components |

---

## Architecture

Visione runs as a local client-server application. The React frontend communicates with a FastAPI backend over localhost; real-time progress streams back via SSE. Heavy inference runs in-process (diffusers, PyTorch) or via a ComfyUI headless subprocess for video pipelines. Models load and unload sequentially to fit within a 16GB VRAM budget — one active model at a time.

The desktop shell (Tauri 2) wraps the frontend as a native window and manages backend process lifecycle. All assets, models, and outputs live on local storage; nothing is transmitted externally.

Components share models where possible — image generation models are reused across Imagine, Retouch, Retexture, and Storyboard; video models feed through from Imagine into Retexture and Sound Studio. The Video Editor and Gallery operate CPU-side, assembling outputs produced by the GPU components.

---

## Status

Code-complete. Final UI design pass in progress.

---

## License

MIT

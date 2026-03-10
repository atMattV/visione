# Visione

A local-first AI creative production suite for consumer GPUs.
Read the full documentation [here](https://www.notion.so/Visione-Technical-Documentation-3194a74185bb8015b154e234606497e2)

---

## What is Visione?

Visione is a self-contained desktop application for AI-driven creative production. It runs entirely on local hardware: no cloud services, no external APIs, no subscriptions. Every model runs on-device; inference never leaves your machine.

The pipeline covers the full creative arc: text-to-image and video generation, retouching, stylization, enhancement, and sound design, all within a single application.

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
| **Characters** | Persistent character library with 5-shot reference generation for cross-shot consistency |
| **Gallery** | Unified asset browser across all components |

## Models

| Model | Purpose |
|-------|---------|
| Z-Image Turbo FP8 | Image generation |
| Z-Image Qwen 3 4B | Text encoder |
| Z-Image VAE | VAE | 
| Z-Image LoRAs (38) | Style presets | 
| Flux2 Klein 4B FP8 | Image gen / editing |
| Flux2 Klein 9B BF16 | Image gen/ High-quality editing | 
| Flux2 VAE | VAE |
| ControlNet Union 2.1 | Structural conditioning (Retexture) | 
| Patina LoRAs (21) | Stylization presets | 
| SPAN 4x Upscaler | Image upscaling |
| SCUNet Denoiser | Image denoising | 
| CodeFormer | Face enhancement | 
| LTX-2.3 22B FP8 | Video generation | 
| LTX-2 Gemma 3 12B FP4 | Video text encoder |
| LTX-2.3 22B Distilled LoRA | Fast video sampling | 
| LTX-2.3 Spatial Upscaler | 2× video upscale | 
| LTX-2.3 Audio VAE | Audio generation |
| VEnhancer FP16 | Video enhancement |
| SeedVR2 3B FP8 | Video upscaling | 
| RIFE v4.26 | Frame interpolation |
| ACE-Step SFT + Base | Music generation | 
| ACE-Step LM 1.7B | Music language model | 
| ACE-Step VAE + TextEnc | Music pipeline | 
| Qwen3-TTS 1.7B (3 variants) | Text-to-speech | 
| HunyuanVideo-Foley XL | Video-to-audio | 
| Wan 2.1 T2V 1.3B | StyleMaster backbone | 
| StyleMaster checkpoints | Style injection weights | 
| CLIP ViT-H-14 | Style extraction | 
| IS-Net (rembg) | Background removal (CPU) | 
| LatentSync 1.6 | Lip sync (quality) | 
| MuseTalk 1.5 | Lip sync (fast) | 
| InsightFace buffalo_l | Face detection/swap | 
| Inswapper_128.onnx | Face swap model | 

---

## Architecture

Visione runs as a local client-server application. The React frontend communicates with a FastAPI backend over localhost; real-time progress streams back via SSE. Heavy inference runs in-process (diffusers, PyTorch) or via a ComfyUI headless subprocess for video pipelines. Models load and unload sequentially to fit within a 16GB VRAM budget, one active model at a time.

The desktop shell (Tauri 2) wraps the frontend as a native window and manages backend process lifecycle. All assets, models, and outputs live on local storage; nothing is transmitted externally.

Components share models where possible. Image generation models are reused across Imagine, Retouch, Retexture, and Storyboard; video models feed through from Imagine into Retexture and Sound Studio. The Video Editor and Gallery operate CPU-side, assembling outputs produced by the GPU components.

---

## Weights and Installer

[Here](https://huggingface.co/atMrMattV/Visione) >> COMING week of March 9th 2026

---
## License

MIT

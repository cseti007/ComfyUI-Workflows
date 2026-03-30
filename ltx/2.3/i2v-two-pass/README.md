# LTX Video 2.3 — I2V Two-Pass with Audio

**Model:** LTX Video 2.3 — 22B Distilled (FP8)
**Type:** Image-to-Video

Two-pass Image-to-Video workflow using LTX Video 2.3 with audio generation support. Takes two guide images (start and end frame) and generates a video in a 720p first pass, then upscales to 1080p in a second pass. Audio is encoded via the LTX 2.3 audio VAE and composited into the final output.

---

## Preview

[![Watch on YouTube — click to open](https://img.youtube.com/vi/5pMIWq4kwo8/maxresdefault.jpg)](https://www.youtube.com/watch?v=5pMIWq4kwo8)
*Click to open on YouTube*

---

## Requirements

- **ComfyUI:** recent stable build
- **Model:** `ltx-2.3-22b-distilled_transformer_only_fp8_input_scaled_v3.safetensors` — [Kijai/LTX2.3_comfy](https://huggingface.co/Kijai/LTX2.3_comfy/blob/main/diffusion_models/ltx-2.3-22b-distilled_transformer_only_fp8_input_scaled_v3.safetensors)
- **Video VAE:** `LTX23_video_vae_bf16.safetensors` — [Kijai/LTX2.3_comfy](https://huggingface.co/Kijai/LTX2.3_comfy/blob/main/vae/LTX23_video_vae_bf16.safetensors)
- **Audio VAE:** `LTX23_audio_vae_bf16.safetensors` — [Kijai/LTX2.3_comfy](https://huggingface.co/Kijai/LTX2.3_comfy/blob/main/vae/LTX23_audio_vae_bf16.safetensors)
- **Preview VAE:** `taeltx2_3.safetensors` — [Kijai/LTX2.3_comfy](https://huggingface.co/Kijai/LTX2.3_comfy/blob/main/vae/taeltx2_3.safetensors)
- **Text encoder:** `gemma_3_12B_it_fp8_scaled.safetensors` — [Kijai/LTX2.3_comfy](https://huggingface.co/Kijai/LTX2.3_comfy/tree/main/text_encoders)
- **Text projection:** `ltx-2.3_text_projection_bf16.safetensors` — [Kijai/LTX2.3_comfy](https://huggingface.co/Kijai/LTX2.3_comfy/blob/main/text_encoders/ltx-2.3_text_projection_bf16.safetensors)
- **Custom nodes:**
  - [ComfyUI-KJNodes](https://github.com/kijai/ComfyUI-KJNodes)
  - [ComfyUI-VideoHelperSuite](https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite)
  - [rgthree-comfy](https://github.com/rgthree/rgthree-comfy)
  - [ComfyUI_Fill-Nodes](https://github.com/filliptm/ComfyUI_Fill-Nodes)

---

## Notes

- The workflow uses two guide images (start and end frame) via `LTXVAddGuideMulti`. Image 1 is placed at frame 0, Image 2 at frame 161 by default.
- **Pass 1:** 1280x720, 241 frames @ 24fps, 8 steps, `lcm` sampler, `linear_quadratic` scheduler, CFG 1. NAG guidance is enabled (scale 11, rescale 0.25).
- **Pass 2:** The output is upscaled to 1920x1080 with `nvidia_rtx_vsr` via `ImageResizeKJv2`, then re-encoded and sampled again with `euler_ancestral` sampler for 8 steps.
- An audio file can be supplied via `VHS_LoadAudioUpload` — the audio is encoded with the LTX 2.3 audio VAE and blended into the latent space during both passes.
- A LoRA (`ltx-2.3-22b-distilled-lora-dynamic`) is present in the graph but **disabled** — enable it if you want dynamic motion tuning.
- `LTX2MemoryEfficientSageAttentionPatch`, `LTXVChunkFeedForward`, and `ModelPatchTorchSettings` are used for VRAM optimization. Requires SageAttention installed.

---

## Changelog

- `2026-03-30` — Initial upload

# Z-Image Two-Stage

**Model:** Z-Image (z_image_turbo) + MoodyMix DPO refinement
**Type:** Text-to-Image

Two-pass text-to-image workflow using Comfy-Org's Z-Image model. The first pass generates a full-resolution base image with the BF16 base model; the second pass applies a DPO-tuned refinement model at low denoise strength to improve detail and style consistency. A GLSL-based post-processing subgraph handles HSL color grading.

---

## Preview

![Preview](media/preview.png)

---

## Requirements

- **ComfyUI:** recent stable build (subgraph support required, frontend >= 1.43)
- **Model (Stage 1):** `z-image/z_image_bf16.safetensors` — [download](https://huggingface.co/Comfy-Org/z_image_turbo/resolve/main/split_files/diffusion_models/z_image_turbo_bf16.safetensors)
- **Model (Stage 2):** `z-image/moodyMix_zitV10DPO.safetensors` — [CivitAI](https://civitai.com/models/620406) (verify V10 DPO version)
- **VAE:** `Flux/ultraflux.safetensors` — [CivitAI](https://civitai.com/models/2231253) — alternatively `ae.safetensors` from the official split ([download](https://huggingface.co/Comfy-Org/z_image_turbo/resolve/main/split_files/vae/ae.safetensors))
- **Text encoder:** `qwen_3_4b.safetensors` (lumina2) — [download](https://huggingface.co/Comfy-Org/z_image_turbo/resolve/main/split_files/text_encoders/qwen_3_4b.safetensors)
- **Custom nodes:**
  - [ComfyUI-KJNodes](https://github.com/kijai/ComfyUI-KJNodes) — `DiffusionModelLoaderKJ`, `ImageResizeKJv2`, `Film Grain`, and others
  - [rgthree-comfy](https://github.com/rgthree/rgthree-comfy) — `Seed (rgthree)`, `Image Comparer (rgthree)`

---

## Notes

- **Stage 1:** 20 steps, CFG 4, sampler `res_multistep`, scheduler `simple`, full denoise
- **Stage 2:** 2 steps, CFG 1, sampler `res_multistep`, denoise 0.36 — intended as a light refinement pass
- Base latent resolution: 1920×1088; the second pass includes a 2× upscale step
- The color grading subgraph applies global HSL adjustments (default: saturation -10, all else neutral); it can be bypassed or tuned per shot
- The workflow uses ComfyUI subgraphs — load it in a recent frontend build that supports the subgraph renderer (`LG`)

---

## Changelog

- `2026-03-29` — Initial upload

# WAN 2.2 Upscaling v1

**Model:** WAN 2.2 A14B LowNoise (GGUF Q4_K_M)
**Type:** Upscaling (Video-to-Video)

Per-subject crop upscaling pipeline for WAN 2.2 video output.
Subjects and faces are detected automatically via SAM2 segmentation and Florence2 face detection,
then cropped, upscaled with pixel-based models, refined with WAN video-to-video, and composited back.
RIFE VFI is used for frame interpolation on the final output.

---

## Preview

![Preview v2 (looping)](media/preview-v2-looping.png)

---

## Requirements

- **ComfyUI:** recent stable build
- **Model:** `wan2.2/Wan2.2-T2V-A14B-LowNoise-Q4_K_M.gguf` — [download](https://huggingface.co/QuantStack/Wan2.2-T2V-A14B-GGUF/tree/main) (place in `ComfyUI/models/unet/`)
- **VAE:** `wan/Wan2_1_VAE_bf16.safetensors` — [download](https://huggingface.co/Kijai/WanVideo_comfy/blob/main/Wan2_1_VAE_bf16.safetensors) (place in `ComfyUI/models/VAE/`)
- **Text encoder:** `umt5-xxl-enc-bf16.safetensors` — [download](https://huggingface.co/Comfy-Org/Wan_2.2_ComfyUI_Repackaged/tree/main/split_files/text_encoders) (place in `ComfyUI/models/text_encoders/`)
- **LoRA (speed):** `Wan/lightx2v/lightx2v_T2V_14B_cfg_step_distill_v2_lora_rank64_bf16.safetensors` — [download](https://huggingface.co/Kijai/WanVideo_comfy/tree/main/Lightx2v)
- **LoRA (quality, example):** `Wan/wan2.2_fun-reward/Wan2.2-Fun-A14B-InP-low-noise-HPS2.1.safetensors` — reward LoRA for quality improvement; replace with any WAN 14B compatible LoRA or remove
- **SAM2 model:** `sam2.1_hiera_base_plus.safetensors` — auto-downloaded by `DownloadAndLoadSAM2Model`
- **RIFE model:** `rife49.pth` — auto-downloaded by `RIFE VFI`
- **Upscale models** (place in `ComfyUI/models/upscale_models/`):
  - `4x-ClearRealityV1.pth` — [download](https://openmodeldb.info/models/4x-ClearRealityV1) — fast photo-realistic upscaler
  - `phhofm/1xDeJPG_realplksr_otf.pth` — [download](https://openmodeldb.info/models/1x-DeJPG-realplksr-otf) — JPEG artifact remover / enhancer
  - `1xSkinContrast-HighAlternative-SuperUltraCompact.pth` — [download](https://openmodeldb.info/models/1x-SkinContrast-HighAlternative-SuperUltraCompact) — skin detail enhancer
  - `DF2K_JPEG.pth` — [download](https://openmodeldb.info/models/4x-realsr-df2k-jpeg) — slower but higher quality upscaler
- **Custom nodes:**
  - [ComfyUI-WanVideoWrapper](https://github.com/kijai/ComfyUI-WanVideoWrapper)
  - [ComfyUI-VideoHelperSuite](https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite)
  - [ComfyUI-KJNodes](https://github.com/kijai/ComfyUI-KJNodes)
  - [ComfyUI-Florence2](https://github.com/kijai/ComfyUI-Florence2)
  - [ComfyUI-segment-anything-2](https://github.com/kijai/ComfyUI-segment-anything-2)
  - [ComfyUI-Frame-Interpolation](https://github.com/Fannovel16/ComfyUI-Frame-Interpolation)
  - [rgthree-comfy](https://github.com/rgthree/rgthree-comfy)

---

## Notes

- **Face index:** After running Florence2, each detected face gets a numbered ID visible above the bounding box in the preview. Set the `Index` field in the face crop node to the ID of the face you want to upscale.
- **crop_size_mult:** Controls the crop area around the face. Use a higher value for faces that are large on screen, lower for small faces. Follow the preview output to calibrate.
- **VRAM:** For 1080p output on under 16 GB VRAM, reduce `context_frames` to 33 or 41 in `WanVideoContextOptions`.
- **WAN denoise strength:** Upscale passes use 0.3 denoise — low enough to preserve structure, high enough for texture refinement.
- Input resolution: 832x480, 81 frames. The pipeline outputs at a higher resolution after upscaling.

---

## Changelog

- `2025-10-13` — Initial upload
